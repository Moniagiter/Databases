# Завдання до РГР
```
Для БД, що створена у лабораторних роботах 1-4, визначити
наступне: 1. Визначити предметну область.
2. Описати модель предметної області.
3. Побудувати логічну модель БД (ER-модель). Якщо необхідно, модель предметної
області треба ускладнити так, щоб у логічній моделі БД був хоча б один зв’язок
між сутностями типу багато-до-багатьох.
4. Описати обмеження, що накладаються на БД щодо підтримки:
a. цілісності сутностей;
b. цілісності посилань;
c. семантичної цілісност
```
## 1. Предметна область
База даних "Бухгалтерія" використовується для обліку співробітників, їх посад, відділів, проектів та участі у проектах. Основна мета БД — автоматизація управління інформацією про персонал, відділи, посадові обов'язки та проекти.

## 2. Модель предметної області
### Основні компоненти моделі:
#### Відділи:
Зберігають назви відділів.  
Пов'язані зі співробітниками (зв’язок "один-до-багатьох").
#### Посади:
Містять назви посад та оклади.  
Пов'язані зі співробітниками (зв’язок "один-до-багатьох").
#### Співробітники:
Містять особисті дані, відділ, посаду та досвід роботи.  
Пов'язані з дітьми (зв’язок "один-до-багатьох").  
Пов'язані з проектами через таблицю "Участь у проєктах" (зв’язок "багато-до-багатьох").
#### Діти:
Інформація про дітей співробітників.  
Пов'язані зі співробітниками (зв’язок "один-до-багатьох").
#### Проєкти:
Містять інформацію про назви проектів та терміни.  
Пов'язані з участю співробітників.
#### Участь у проєктах:
Реалізує зв’язок "багато-до-багатьох" між співробітниками та проектами.
## 3. ER-Модель

ER-модель описує взаємозв’язки між сутностями бази даних:  

Відділи – до – Співробітники: зв’язок "один-до-багатьох".  
Посади – до – Співробітники: зв’язок "один-до-багатьох".  
Співробітники – до – Діти: зв’язок "один-до-багатьох".  
Співробітники – до – Проєкти через Участь у проєктах: зв’язок "багато-до-багатьох".  
Для зв’язку "багато-до-багатьох" створено таблицю Участь_у_проєктах, яка містить атрибути:  

Табельний_номер (ідентифікатор співробітника).  
Проєкт_Id (ідентифікатор проекту).  
Роль (роль співробітника у проекті).  
Дата_призначення (дата приєднання до проекту).

```plaintext
+----------------+          +----------------+          +--------------------+
|    Відділи     |          |    Посади      |          |     Проєкти        |
+----------------+          +----------------+          +--------------------+
| Id             |<---------| Назва_посади   |<---------| Id                 |
| Назва_відділу  |          | Оклад          |          | Назва_проєкту      |
+----------------+          +----------------+          | Дата_початку       |
        |                                               | Дата_завершення    |
        |                                               +--------------------+
        |                                               ^
        |                                               |
        v                                               |
+-----------------+         +-----------------+         |
|  Співробітники  |---------|Участь_у_проєктах|---------+
+-----------------+         +-----------------+         
| Табельний_номер |         | Табельний_номер |         
|ПІБ_співробітника|         | Проєкт_Id       |         
| ІПН             |         | Роль            |         
| Стать           |         | Дата_призначення|         
| Дата_народження |         +-----------------+         
| Відділ_Id       |                                      
| Назва_посади    |                                      
+-----------------+                                      
        |                                              
        v                                              
+----------------+                                      
|     Діти       |                                      
+----------------+                                      
| Id             |                                      
| Табельний_номер|                                      
| ПІБ_дитини     |                                      
| Стать_дитини   |                                      
| Дата_народження|                                      
+----------------+

```                                
## 4. Обмеження
#### a. Цілісність сутностей:
Використання PRIMARY KEY для забезпечення унікальності записів (наприклад, Id у таблиці "Відділи").  
Поля з NOT NULL гарантують наявність важливих даних (наприклад, Назва_відділу у таблиці "Відділи").  
#### b. Цілісність посилань:
Зовнішні ключі (FOREIGN KEY) забезпечують зв’язки між таблицями:  
Відділ_Id у таблиці "Співробітники" пов’язаний із Id у таблиці "Відділи".  
Табельний_номер у таблиці "Діти" пов’язаний із Табельний_номер у таблиці "Співробітники".  
#### c. Семантична цілісність:
Обмеження CHECK забезпечують правильність даних:  
Поле Оклад у таблиці "Посади" має бути більше нуля.  
Поле Стать_співробітника обмежене значеннями "м" або "ж".  
Поле Стать_дитини у таблиці "Діти" також обмежене значеннями "м" або "ж".
