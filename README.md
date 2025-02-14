# Травицкий Сергей
# Домашнее задание к занятию «Кеширование Redis/memcached»

### Инструкция по выполнению домашнего задания

1. Сделайте fork [репозитория c шаблоном решения](https://github.com/netology-code/sys-pattern-homework) к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
2. Выполните клонирование этого репозитория к себе на ПК с помощью команды `git clone`.
3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
   - впишите вверху название занятия и ваши фамилию и имя;
   - в каждом задании добавьте решение в требуемом виде: текст/код/скриншоты/ссылка;
   - для корректного добавления скриншотов воспользуйтесь инструкцией [«Как вставить скриншот в шаблон с решением»](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md);
   - при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в [инструкции по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md).
4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`).
5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
6. Любые вопросы задавайте в чате учебной группы и/или в разделе «Вопросы по заданию» в личном кабинете.

Желаем успехов в выполнении домашнего задания.

---

### Задание 1. Кеширование 

Приведите примеры проблем, которые может решить кеширование. 

*Приведите ответ в свободной форме.*

#### Производительности системы может не хватать для быстрой обработки большого количества запросов к БД, кэширование решает эту проблемму

- В кэше сохраняются данные к которым обращаются чаще всего.  
- Оптимизируется работа во время пиковых нагрузок.   
- Кэш может писать информацию в файл если нехватает памяти, тем самым снижая нагрузку на БД  
---

### Задание 2. Memcached

Установите и запустите memcached.

*Приведите скриншот systemctl status memcached, где будет видно, что memcached запущен.*

```
sudo apt update && sudo apt install memcached
memcached -V
sudo systemctl status memcached

```
*Скрин*

![image](https://github.com/travickiy67/Redis-Memcached/blob/main/img/img1.1.png)
---

#### Задание 3. Удаление по TTL в Memcached

Запишите в memcached несколько ключей с любыми именами и значениями, для которых выставлен TTL 5.   

*Приведите скриншот, на котором видно, что спустя 5 секунд ключи удалились из базы.*  

### Записано три ключа 2 ключа с TTL 100, третий 5. При проверке третий ключь удалился первым, первый и второй удалились через 100 секунд.  
```
telnet localhost 11211
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
add key1 1 100 4
test
add key2 1 100 4
test
add key3 1 5 4
test
get key3
get key1
get key2
get key1
get key2
get key3
quit
```
*Скрин*  

![image](https://github.com/travickiy67/Redis-Memcached/blob/main/img/img2.1.png)

#### Через docker, первый ключ с ttl 0
*Скрин 1*

![image](https://github.com/travickiy67/Redis-Memcached/blob/main/img/img3.2.png)

*Скрин 2*

![image](https://github.com/travickiy67/Redis-Memcached/blob/main/img/img3.3.png)

---


### Задание 4. Запись данных в Redis

Запишите в Redis несколько ключей с любыми именами и значениями. 

*Через redis-cli достаньте все записанные ключи и значения из базы, приведите скриншот этой операции.*
#### Установка redis
```
sudo apt install redis
sudo systemctl status redis
```
*Cкрин*  
![image](https://github.com/travickiy67/Redis-Memcached/blob/main/img/img3.1.png)

#### Комманды
```
redis-cli
scan 0
set test1 100
set test2 1000
scan 0
get test1
get test2
exit
```
*Скрин*  

![image](https://github.com/travickiy67/Redis-Memcached/blob/main/img/img4.2.png)

#### Через docker

*Скрин 1*

![image](https://github.com/travickiy67/Redis-Memcached/blob/main/img/img4.3.png)

*Скрин 2*

![image](https://github.com/travickiy67/Redis-Memcached/blob/main/img/img4.4.png)

## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже разобраться в материале.

### Задание 5*. Работа с числами 

Запишите в Redis ключ key5 со значением типа "int" равным числу 5. Увеличьте его на 5, чтобы в итоге в значении лежало число 10.  

*Приведите скриншот, где будут проделаны все операции и будет видно, что значение key5 стало равно 10.*

#### Листинг

```
redis-cli
scan 0
set test 5
exists test
get test
incrby test 5
get test
type test
ttl test
flushall
exit
```
*Скриншот результата*

![image](https://github.com/travickiy67/Redis-Memcached/blob/main/img/img4.1.png)

