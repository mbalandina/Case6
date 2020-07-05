# Case6 
import json
file_path = 'case6.json'
with open(file_path, 'rb') as f:
    data = json.load(f)
users=[]
#Создадим пустой список users, в который мы будем записывать всех пользователей.
#Для этого пройдемся по каждому словарю из списка словарей data, 
#вытащим значение по ключу user_id, после чего добавим его в массив users с помощью функции append():
for event in data:
            users.append(event['user_id'])
users_count = len(users)
set_users = set(users)
set_users_count=len(set_users)


users_target = [event['user_id'] for event in data if event['event_type'] == 'target_event']
set_users_target = set(users_target)
users_target_count = len(set_users_target)
#print(users_target) 
from collections import Counter
users_target_counter = Counter(users_target)
#print(users_target_counter)
#Cчетчик users_target_counter, где для каждого пользователя указано количество совершенных им целевых действий, например Counter({301: 9, 355: 9,)

count_of_target_values_by_users=users_target_counter.values()
#print('список count_of_target_values_by_users',count_of_target_values_by_users)
#список count_of_target_values_by_users, в котором будет количество целевых действий, 
#совершенных каждым пользователем (сделать это можно с помощью функции .values(), 


counter_of_events_by_users = Counter(count_of_target_values_by_users)
#print(counter_of_events_by_users)
# Cчетчик counter_of_events_by_users, 
#где в качестве ключа - число целевых действий, а значения - количество пользователей,
#совершивших определенное число целевых действий.


def getEventsStats(users_list):
    user_counter = Counter(users_list)
    all_target_values=sum(users_target_counter.values())
    for user_type in counter_of_events_by_users:
        users_count = user_counter[user_type]
        users_count_share = users_count*user_type/all_target_values
        target_event_share_for_user=users_count/users_target_count
        print ('Количество пользователей, совершивших {} заказ: {}'.format(user_type,users_count))
        print ('Процент покупок от общего числа покупок : {:.2%}'.format(users_count_share))
        print ('Доля таких пользователей от общего числа пользователей, совершивших целевые действия: {:.2%}'.format(target_event_share_for_user))
        print ()
getEventsStats(counter_of_events_by_users)

print('Процент заказов, совершенных пользователями с одним заказом: 52.37%')
print('Процент пользователей, совершивших один заказ: 82.45% ')
print('Процент заказов,, совершенных пользователями с более, чем одним заказом: 47.63%')
print('Процент пользователей, совершивших более одного заказа: 17.55%')

## Чаще всего по несколько раз фильмы/сериалы покупают одни и те же 17,5% пользователей. Небольшой процент пользователей обеспечивает 52% всех целевых действий. 82% пользователей делают только один заказ. Необхидимо разработать комплекс мер по стимулирванию повторных покупок и удержанию клиентов.
