# Mission 2
## Part 0
https://drive.google.com/file/d/1AzZhoCVwkffIoDeO80iMLuK8FicQwfIW/view?usp=sharing
## Part1
Вопрос 1. 
SSH – сетевой протокол для безопасного удаленного доступа к различным операционным системам. Используется в основном для удаленного управления данными пользователя на сервере.

Вопрос 2. 
Ключ можно добавить через текстовый редактор nano в командной строке.
С помощью команды nano необходимо открыть файл authorized_keys в папке home/user1/.ssh и добавить ключ

Вопрос 3. 
В случае с long polling – нам необходимо постоянно делать запросы к серверу Tg чтобы выяснить появились ли новые сообщения. По умолчанию запрос открыт 30 секунд,
 после чего его необходимо повторить. 
В случае с webhooks сервер сам направит сообщение на заранее указанный URL. Лучше чем long polling, т.к. нет необходимости спамить запросами. Из минусов: необходимо создавать публичный URL. 

Вопрос 4.
Issues на гитхабе используются для работы с ошибками, улучшениями и другими задачами, которые связаны с проектами. Каждый issue представляет ветку обсуждения, 
в которой разработчики могут декомпозировать задачу на более мелкие составляющие. Issue позволяют командам разработчиков эффективнее общаться и работать над проектами.
https://github.com/bitcoinbook/bitcoinbook/issues/1100
https://github.com/SigNoz/signoz/issues/6053

Вопрос 5. 
Необходимо создать папку и добавить в неё пустой файл. Обычно используют файл под названием. gitkeep или любым другим именем

# Mission 3
## Parts 1,2,3
https://drive.google.com/file/d/1EbCEF0kedcZmsk4QrNc8Q2vYvhXBO-Cm/view?usp=sharing
## Part 3
1. Получить список юзернеймов пользователей
```sql
SELECT username FROM users
```
2. получить кол-во отправленных сообщений каждым пользователем: username - number of sent messages
```sql
SELECT u.username, COUNT(m.text) AS number_of_sent_messages
FROM messages m
JOIN users u ON m.from = u.id
GROUP BY m.from, u.username
```
3. Получить пользователя с самым большим кол-вом полученных сообщений и само количество. username - number of received messages
```sql
SELECT u.username, COUNT(m.text) AS number_of_recieved_messages
FROM messages m
JOIN users u ON m.to = u.id
GROUP BY u.username
ORDER BY number_of_recieved_messages DESC
LIMIT 1;
```
4. Получить среднее кол-во сообщений, отправленное каждым пользователем
```sql
SELECT ROUND(AVG(number_of_sent_messages),2) 
FROM  
(SELECT u.username, COUNT(m.text) AS number_of_sent_messages 
  FROM messages m
  JOIN users u ON m.from = u.id
  GROUP BY u.username
) AS subquery;
```
