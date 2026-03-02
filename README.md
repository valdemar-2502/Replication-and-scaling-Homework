# Домашнее задание к занятию «Репликация и масштабирование. Часть 1» -Kadancev Vladimir

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
6. Любые вопросы задавайте в разделе «Вопросы по заданию» в личном кабинете.

Желаем успехов в выполнении домашнего задания.

---

### Задание 1

На лекции рассматривались режимы репликации master-slave, master-master, опишите их различия.

*Ответить в свободной форме.*

---
### Ответ:
---

`
### Master-Slave (ведущий-ведомый)

Архитектура: Один основной сервер (Master) и один или несколько подчиненных (Slave) .

Запись (Write): Только на Master .

Чтение (Read): На любом сервере (Master и всех Slave), что позволяет распределять нагрузку .

### Плюсы:

Простая настройка и администрирование .

Отсутствие конфликтов данных, так как запись идет только в одну точку .

Идеально подходит для масштабирования операций чтения (например, отчеты, аналитика выносятся на Slave) .

### Минусы:

Единая точка отказа для операций записи (если Master выходит из строя, запись данных становится невозможна до его восстановления) .

Возможна задержка данных на Slave (replication lag) .

### Master-Master (ведущий-ведущий)

Архитектура: Два или более сервера, каждый из которых является и мастером, и слейвом для другого .

Запись (Write): На любом из серверов .

Чтение (Read): На любом сервере .

### Плюсы:

Высокая отказоустойчивость. При отказе одного узла запись можно продолжать на другой .

Возможность распределения нагрузки по записи (хотя на практике это требует очень аккуратной архитектуры) .

Позволяет организовать географически распределенные кластеры .

### Минусы:

Сложность настройки и поддержки .

Главный недостаток: конфликты данных. Если изменять одну и ту же запись на разных серверах одновременно, данные могут быть повреждены или потеряны . Для критичных транзакционных систем это может быть неприемлемо.

Требует продуманной схемы разрешения конфликтов (например, использование разных автоинкрементов для разных серверов) .

### Вывод: Master-Slave — это стандарт для большинства веб-приложений, где важно отделить чтение от записи и иметь простую архитектуру. Master-Master используется там, где критически важна отказоустойчивость записи и есть возможность контролировать или избегать конфликтов на уровне приложения.
`

### Задание 2

Выполните конфигурацию master-slave репликации, примером можно пользоваться из лекции.

*Приложите скриншоты конфигурации, выполнения работы: состояния и режимы работы серверов.*

---
### Решение
---
При выполнении задания использовалась docker compose конфигурация
![config-docker-compose.yml-1](https://github.com/valdemar-2502/Replication-and-scaling-Homework/blob/main/docker-compose.yml-1)

---
![database](https://github.com/valdemar-2502/Replication-and-scaling-Homework/blob/main/Screenshots/install.png)
![database](https://github.com/valdemar-2502/Replication-and-scaling-Homework/blob/main/Screenshots/master.png)
![database](https://github.com/valdemar-2502/Replication-and-scaling-Homework/blob/main/Screenshots/master-base.png)
![database](https://github.com/valdemar-2502/Replication-and-scaling-Homework/blob/main/Screenshots/slave.png)
![database](https://github.com/valdemar-2502/Replication-and-scaling-Homework/blob/main/Screenshots/slave-base.png)

---
## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

---

### Задание 3* 

Выполните конфигурацию master-master репликации. Произведите проверку.

*Приложите скриншоты конфигурации, выполнения работы: состояния и режимы работы серверов.*

---
### Решение
---
![database](https://github.com/valdemar-2502/Replication-and-scaling-Homework/blob/main/Screenshots/master-slave3.png)
![database](https://github.com/valdemar-2502/Replication-and-scaling-Homework/blob/main/Screenshots/slave-master3.png)
![database](https://github.com/valdemar-2502/Replication-and-scaling-Homework/blob/main/Screenshots/status%20slave-master3.png)
![database](https://github.com/valdemar-2502/Replication-and-scaling-Homework/blob/main/Screenshots/slave%20master-master3.png)
![database](https://github.com/valdemar-2502/Replication-and-scaling-Homework/blob/main/Screenshots/master-finish.png)
![database](https://github.com/valdemar-2502/Replication-and-scaling-Homework/blob/main/Screenshots/slave-finish.png)
