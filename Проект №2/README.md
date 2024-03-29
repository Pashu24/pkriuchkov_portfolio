# **Проект "Перспективный тариф сотовой связи"**

### Цель:
- показать, какой тариф выгоднее для оператора - "Смарт" или "Ультра";
- какой регион выгоднее для оператора - Москва или другие регионы. 

### **Результаты:** <br/>
Гипотезы проверялись статистическими методами по t-критерию Стьюдента на основе поведения 500 пользователей в течение года.<br/>

- Средняя выручка тарифа "Смарт" больше чем тарифа "Ультра". По t-критерию Стьюдента значение p-value получилось меньше порога статистической значимости в 0.01. Данные выдают очень маловероятный результат в отношении нулевой гипотезы. Таким образом, принимаем альтернативную гипотезу: "Выручки различаются"

- Средняя выручка для Москвы и регионов не отличается. В результате теста мы получили данные, которые не противоречат нулевой гипотезе - p-value=54 %, что существенно больше порога статистической значимости 0.01.

### Стек - Python, Pandas.

### Статус - Завершён.


<!---
**Ход решения:**
- Имеются данные об объёме звонков, СМС, трафика для 500 пользователей за год. Для каждой услуги данные представлены отдельными таблицами;
- Данные были объединены в одну таблицу. Для проведения аналитики для каждого пользователя были рассчитаны:
    - объём услуг по месяцам;
    - помесячную выручку с каждого пользователя.
- Дополнительно посчитаны среднее количество, дисперсия и стандартное отклонение для звонков, СМС и трафика.
- С использованием t-критерия Стьюдента проверены гипотезы
    - об отличии средней выручки пользователей тарифов «Ультра» и «Смарт»;
    - об отличии средней выручки пользователей из Москвы и из других регионов.
--->

# Описание данных
**Таблица users** (информация о пользователях):<br />
`user_id` — уникальный идентификатор пользователя <br />
`first_name` — имя пользователя<br />
`last_name` — фамилия пользователя <br />
`age` — возраст пользователя (годы) <br />
`reg_date` — дата подключения тарифа (день, месяц, год) <br />
`churn_date` — дата прекращения пользования тарифом (если значение пропущено, то тариф ещё действовал на момент выгрузки данных) <br />
`city` — город проживания пользователя <br />
`tariff` — название тарифного плана <br />


**Таблица calls** (информация о звонках): <br />
`id` — уникальный номер звонка <br />
`call_date` — дата звонка <br />
`duration` — длительность звонка в минутах <br />
`user_id` — идентификатор пользователя, сделавшего звонок <br />


**Таблица messages** (информация о сообщениях): <br />
`id` — уникальный номер сообщения <br />
`message_date` — дата сообщения <br />
`user_id` — идентификатор пользователя, отправившего сообщение <br />


**Таблица internet** (информация об интернет-сессиях): <br />
`id` — уникальный номер сессии <br />
`mb_used` — объём потраченного за сессию интернет-трафика (в мегабайтах) <br />
`session_date` — дата интернет-сессии <br />
`user_id` — идентификатор пользователя <br />


**Таблица tariffs** (информация о тарифах): <br />
`tariff_name` — название тарифа <br />
`rub_monthly_fee` — ежемесячная абонентская плата в рублях <br />
`minutes_included` — количество минут разговора в месяц, включённых в абонентскую плату <br />
`messages_included` — количество сообщений в месяц, включённых в абонентскую плату <br />
`mb_per_month_included` — объём интернет-трафика, включённого в абонентскую плату (в мегабайтах) <br />
`rub_per_minute` — стоимость минуты разговора сверх тарифного пакета (например, если в тарифе 100 минут разговора в месяц, то со 101 минуты будет взиматься плата) <br />
`rub_per_message` — стоимость отправки сообщения сверх тарифного пакета <br />
`rub_per_gb` — стоимость дополнительного гигабайта интернет-трафика сверх тарифного пакета (1 гигабайт = 1024 мегабайта) <br />

**Примечание:** <br />
«Мегалайн» всегда округляет секунды до минут, а мегабайты — до гигабайт. <br />
Каждый звонок округляется отдельно: даже если он длился всего 1 секунду, будет засчитан как 1 минута. <br />
Для веб-трафика отдельные сессии не считаются. Вместо этого общая сумма за месяц округляется в бо́льшую сторону. Если абонент использует 1025 мегабайт в этом месяце, с него возьмут плату за 2 гигабайта.
