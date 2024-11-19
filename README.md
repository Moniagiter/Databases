1. Предметна область
Предметна область цієї бази даних охоплює облік співробітників, їх посад, відділів, проектів та участі у проектах. База даних призначена для автоматизації управління даними про персонал, відділи, посадові обов'язки та проекти.

2. Модель предметної області
База даних моделює такі процеси:

Управління інформацією про відділи, посади та співробітників.
Реєстрація участі співробітників у проектах з описом їх ролей.
Облік сімейних даних співробітників (діти).
Ведення інформації про проекти: назви, терміни виконання.
Основні компоненти:
Відділи:

Зберігають назви відділів.
Пов'язані зі співробітниками (один відділ може мати багато співробітників).
Посади:

Описують назви посад та оклад.
Пов'язані зі співробітниками (одна посада може бути закріплена за багатьма співробітниками).
Співробітники:

Містять особисті дані, відділ, посаду та досвід роботи.
Пов'язані з дітьми (один співробітник може мати кілька дітей).
Пов'язані з проектами через таблицю "Участь_у_проєктах".
Діти:

Інформація про дітей співробітників.
Пов'язані зі співробітниками (один батько може мати кількох дітей).
Проєкти:

Містять інформацію про назви проектів та їх терміни.
Пов'язані з участю співробітників.
Участь у проєктах:

Реалізує зв'язок багато-до-багатьох між співробітниками та проектами.
3. Логічна модель (ER-модель)
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
4. Обмеження
a. Цілісність сутностей:
Поля PRIMARY KEY в кожній таблиці забезпечують унікальність кожного запису (наприклад, Id у таблиці "Відділи").
Поля, що не можуть бути порожніми (NOT NULL), гарантують наявність важливих даних (наприклад, Назва_відділу у таблиці "Відділи").
b. Цілісність посилань:
Встановлені зовнішні ключі (FOREIGN KEY) забезпечують зв’язок між таблицями. Наприклад:
Відділ_Id у таблиці "Співробітники" пов’язаний із Id у таблиці "Відділи".
Табельний_номер у таблиці "Діти" пов’язаний із Табельний_номер у таблиці "Співробітники".
c. Семантична цілісність:
Обмеження CHECK перевіряють правильність даних:
Поле Оклад у таблиці "Посади" має бути більше нуля.
Поле Стать_співробітника обмежене значеннями "м" або "ж".
Поле Стать_дитини у таблиці "Діти" також обмежене значеннями "м" або "ж".

```plaintext
+----------------+          +----------------+          +--------------------+
|    Відділи     |          |    Посади      |          |     Проєкти        |
+----------------+          +----------------+          +--------------------+
| Id             |<---------| Назва_посади   |<---------| Id                 |
| Назва_відділу  |          | Оклад          |          | Назва_проєкту      |
+----------------+          +----------------+          | Дата_початку       |
        |                                              | Дата_завершення    |
        |                                              +--------------------+
        |                                              ^
        |                                              |
        v                                              |
+----------------+          +----------------+          |
|  Співробітники |----------| Участь_у_проєктах |-------+
+----------------+          +----------------+         
| Табельний_номер|          | Табельний_номер |         
| ПІБ_співробітника|        | Проєкт_Id       |         
| ІПН            |          | Роль            |         
| Стать          |          | Дата_призначення|         
| Дата_народження|          +----------------+         
| Відділ_Id      |                                      
| Назва_посади   |                                      
+----------------+                                      
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
