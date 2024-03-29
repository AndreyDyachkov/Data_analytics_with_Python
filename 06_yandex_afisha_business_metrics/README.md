## Оптимизация маркетинговых затрат в Яндекс.Афише
## Cohort analysis and business metrics calculation: DAU, WAU, MAU; AOV; LTV; retention; CAC; ROMI. (Yandex_practicum_eng)
### Задача:
Проанализировать бизнес-показатели сервиса Яндекс.Афиши. На основе данных о посещениях сайта изучить, как люди пользуются продуктом, когда они начинают покупать, сколько денег приносит каждый клиент, когда он окупается. По итогам анализа предложить пути оптимизации маркетинговых расходов, выявить невыгодных источников трафика и перераспределить бюджет.

### Инструменты:
Python, Pandas, Numpy, Matplotlob

### Методики и метрики:
EDA, когортный анализ, retention, LTV, DAU, WAU, MAY, AOL, ROMI, CAC 

### Описание данных:
Данные Яндекс.Афиши с июня 2017 по конец мая 2018 года:
1. visits_log.csv - лог сервера с данными о посещениях сайта Яндекс.Афиши,
    - Uid — уникальный идентификатор пользователя,
    - Device — категория устройства пользователя,
    - Start Ts — дата и время начала сессии,
    - End Ts — дата и время окончания сессии,
    - Source Id — идентификатор источника перехода на сайт.
2. orders_log.csv - выгрузка всех заказов за этот период
    - Uid — уникальный идентификатор пользователя,
    - Buy Ts — дата и время заказа,
    - Revenue — сумма заказа.
3. costs.csv - статистика рекламных расходов.
    - source_id — идентификатор рекламного источника,
    - dt — дата проведения рекламной кампании,
    - costs — расходы на эту кампанию.

### Анализ:
#### 1. Провели обработку данных и EDA. Получили следующие результаты:
- Посещения: у нас всего две категории устройств пользователя; 9 источников перехода на сайт с большим разбросом по популярности, при этом 8 источника нет, а по 6 и 7 очень мало визитов. 
- Заказы: огромный разброс по выручке (стандартное отклонение значительно больше среднего). По boxplot видно что это выбросы.
- Расходы: распределение не нормальное, есть выбросы

#### 2. Рассчитали DAU, WAU, MAU (средние за отчетный период и динамику по дням, неделям и месяцам соответственно.
  ![DAU, WAU, MAU](https://github.com/AndreyDyachkov/Portfolio_RU/blob/main/06_yandex_afisha_business_metrics/images/dau_wau_mau.png)
<b>Вывод по DAU, WAU, MAU</b><br>
- Были очевидные тренды: рост недельного и месячного кол-ва уникальных пользователей с начала осени до декабря 2017. В декабре 2017 началось плавное снижение до конца отчетного периода. В целом сравнив конец с началом периода можно предположить что число  уникальных пользователей имеет тенденцию к росту.
- Возможные причины такого тренда: сезонность (для подтверждения нужны данные за несколько лет); активность маркетологов; внешние факторы (изменение интереса пользователей к контенту сайта с течением времени)
- Выявлены аномально высокие и низкие показатели DAU. Возможные причины: активность Яндекс Афишы; внешнее событие; ошибка в данных. Аномальное падение возможно из-за внутренней технической ошибки или внешних причин ограничивающих доступ к сайту.

#### 3. Определили частоту посещения сайта и среднюю продолжительность сессии.
<br>Среднее число посещение: 1.1. Выявлено аномально высокое число посещений на одного пользователя 24 и 28 ноября 2017 (24 также было высокое DAU) и аномально низкая активность 31.03.2018, что совпадает с минимальным DAU. Причины очевидно такие же как и для выбросов в DAU: Яндекс Афиша что-то сделала для привлечения пользователей включая повторные визиты; внешняя причина: случилось событие которое как-то привело пользователей на страницу; ошибка в данных. Аномальное падение 31.03.2018 возможно из-за внутренней технической ошибки или внешних причин ограничивающих доступ к сайту. Мода продолжительности сессии 60 секунд.

#### 4. Рассчитали Retention Rate, применяя когортный анализ.
  ![Retention rate by cohorts](https://github.com/AndreyDyachkov/Portfolio_RU/blob/main/06_yandex_afisha_business_metrics/images/retention_by_cohorts.png)
<b>Вывод Retention rate</b><br>
Retention rate низкий (хотя тут нужно сравнивать с аналогичными продуктами - может это и нормально) и в целом имеет тенденцию к  снижению с ростом времени жизни когорты (что в принципе нормально)

#### 5. Определили среднее время между первым посещением сайта и совершением покупки.

#### 6. Применяя когортный анализ рассчитали среднее количество покупок на одного покупателя за 6 месяцев.
#### 7. Рассчитали Average Order Value (средний чек) за отчетный период и динамику по месяцам.
  ![AOL](https://github.com/AndreyDyachkov/Portfolio_RU/blob/main/06_yandex_afisha_business_metrics/images/aol.png)
  <b>Вывод по среднему чеку</b><br>
Средний чек за весь период равен 5. При оценке по месяцам видны колебания с минимальными значениями в июне 2017 и январе 2018. Максимальный средний чек был в декабре 2017. Возможно в периоды с минимальным значеним действовали скидки, хотя на число заказов они подействовали.
#### 8. Рассчитали LTV по когортам.
  ![LTV](https://github.com/AndreyDyachkov/Portfolio_RU/blob/main/06_yandex_afisha_business_metrics/images/ltv_by_cohorts.png)
  <b>Вывод по LTV</b><br>
Средний LTV за 6 месяцев по когортам с lifetime не моложе 5 месяцев 7.97. При оценке по месяцам видно что основную ценность клиент создает в первый месяц, а в дальнейшие месяцы прирост LTV небольшой. При этом разные когорты немного отличаются по LTV. Выделяется когорта начавшаяся в сентябре 2017: максимальное LTV за 6 мес за счет большого прироста в декабре 2017.
#### 9. Посчитали общую сумму расходов на маркетинг и в разбивке по источникам.
 ![Costs](https://github.com/AndreyDyachkov/Portfolio_RU/blob/main/06_yandex_afisha_business_metrics/images/costs_by_channels.png)
<b>Вывод по расходам на маркетинг</b><br>
Всего за период потратили 329 тысяч. Месячные траты росли во второй половине 2017 года и снижались в первой половине 2018. Вероятно это имело прямое влияние на MAU - графики практически совпадают. В разбивке по источникам трафика видно что больше всего тратили на источник 3 и именно его изменение определяет общую динамику расходов.
#### 10. Рассчитали customer acquisition cost(CAC) (общий и по источникам трафика)
 ![CAC](https://github.com/AndreyDyachkov/Portfolio_RU/blob/main/06_yandex_afisha_business_metrics/images/cac.png)
 <b>Вывод по CAC</b><br>
Средняя стоимость привлечения клиента за весь период равна 9.01. В разбивке по источникам трафика от 4.4 до 13.5. Выделяются два источника 2 и 3 с наибольшей CAC. 

#### 11. Рассчитали ROMI по когортам в разрезе источников. Сравнили окупаемость за одинаковые периоды жизни когорт.
  ![ROMI](https://github.com/AndreyDyachkov/Portfolio_RU/blob/main/06_yandex_afisha_business_metrics/images/romi.png)
<b>Вывод по ROMI</b><br>
Сравним по ROMI на 6 месяц (age 5 на графиках). 
- В первом источнике (source_id = 1) в самой старой когорте (июнь 2017) ROMI высокий (3.7). Но показатель устойчиво снижается с увеличением first_order_month и в декабрьской когорте становится меньше 1 (т.е. уже работаем в убыток)
- По второму источнику(source_id = 2) ROMI по всем когортам ниже 1 кроме стартовавших в сентябре и декабре 2017
- Третий источник (source_id = 3): ROMI во всех когортах ниже 1
- В 4 источнике ROMI также низкий кроме когорты начавшейся в ноябре 2017
- 5 источник: интересная когорта сентября 2017 с ROMI 3.9 (рост с декабря 2017) остальные когорты в основном ниже 1
- 9 источник: ROMI в среднем выше 1 кроме последней когороты от января 2018
- 10 источник: ROMI ниже 1 и данные фрагментарные - мало продаж(?)


### Выводы и рекомендации
#### Источники трафика, требующие внимания.
По итогам анализа посещений сайта Яндекс.Афиши с июня 2017 по май 2018, выгрузки заказов за этот период и рекламных расходов за тот же период выводы следующие:
##### 1. Срочно обратить внимание на три источника трафика с большим потоком покупателей и проблемами с прибыльностью:
- Источник трафика 3: убыточный канал с ROMI ниже 1, при этом расходы на него максимальные. Маркетинговая активность приводит к значительному росту посещаемости, более того сумма расходов в течении отчетного периода коррелирует с MAU. Однако высокая посещаемость не достаточно эффективно конвертируется в заказы. Кол-во покупателей высокое, но за счет больших расходов CAC также максимальное в этом источнике. Рекомендация: не расходовать деньги на привлечение из этого источника.
- Источник трафика 4: в целом также убыточный канал продаж. Расходы на аквизицию высокие, но за счет большого числа покупателей CAC низкий. При этом одна когорта начавшаяся в ноябре 2017 имеет ROMI выше 1. Рекомендация: проанализировать прибыльную когороту и более точно таргетировать маркетинговую активность по этому источнику. Второй вариант: не расходовать деньги на привлечение из этого источника.
- Источник трафика 5: ROMI ниже 1 в половине когорт, при этом есть интересная когорта от сентября 2017 с ROMI 3.9. Рекомендация: проанализировать прибыльную когороту и более точно таргетировать маркетинговую активность по этому источнику.
##### 2. Источники трафика которые по которым также желательно откорректировать маркетинг:
- Источник 9: В целом прибыльный, ROMI в среднем выше 1 кроме последней когороты от января 2018. Расходы низкие, CAC низкий. Кол-во покупателей также низкое. Рекомендация: имеет смысл увеличить активность по этому источнику
- Источник 1: Высокий ROMI в когортах начавшихся в июне-июле 2017.При расходы на аквизицию низкие относительно других источников. Но ROMI устойчиво снижался в последующих когортах  и достиг уровня ниже 1 в когорте от декабря 2017. Так как CAC сильно не росли, то причина в снижение LTV. Рекомендации: проанализировать что поменялось в клиентах в этом источнике и возможно прекратить расходовать на него деньги. 
- Источник 2: две когороты (стартовавшие в сентябре и декабре 2017) показывают неплохой ROMI, остальный - плохой. Также стоимость аквизиции (CAC) в этом канале высокая. Рекомендации: выяснить кого мы привлекли в эти прибыльные когорты и ставить целью именно эти целевые группы. Расходы сократить за счет таргетирования.
- Источник 10: ROMI ниже 1 и данные фрагментарные - мало продаж(?). Рекомендации: не тратить ресурсы на этот источник

#### Выводы после подсчёта метрик каждого вида: маркетинговых, продуктовых и метрик электронной коммерции.
##### 1. Маркетинговые
- Всего за период потратили 329 тысяч. Месячные траты росли во второй половине 2017 года и снижались в первой половине 2018. В разбивке по источникам трафика видно что больше всего тратили на источник 3 и именно его изменение определяет общую динамику расходов. Изменение в уровне расходах отражалось на MAU, графики практически совпадают.
- Средняя стоимость привлечения клиента за весь период равна 9.01. В разбивке по источникам трафика от 4.4 до 13.5. Выделяются два источника 2 и 3 с наибольшей CAC.
- По источникам трафика: больше всего израсходовали на источник 3, не очень эффективно. Вторые по расходам источники 4, 5, также требуют коррекции. Минимальные расходы на источники 9 и 10. Источник 9 прибыльный, расходы на него можно увеличить.
##### 2. Продуктовые:
- Выявлены тренды: рост недельного и месячного кол-ва уникальных пользователей с начала осени до декабря 2017. В декабре 2017 началось плавное снижение до конца отчетного периода. В целом сравнив конец с началом периода можно предположить что число  уникальных пользователей имеет тенденцию к росту. Причины: маркетинговая активность, хотя нельзя исключать и сезонность или внешиен факторы. 
- Выявлены аномально высокие и низкие показатели DAU. Возможные причины: активность Яндекс Афишы; внешнее событие; ошибка в данных. Аномальное падение возможно из-за внутренней технической ошибки или внешних причин ограничивающих доступ к сайту.
- Среднее число посещений: 1.1 .Выявлено аномально высокое число посещений на одного пользователя 24 и 28 ноября 2017 (24 также было высокое DAU) и аномально низкая активность 31.03.2018, что совпадает с минимальным DAU. Причины очевидно такие же как и для выбросов в DAU: Яндекс Афиша что-то сделала для привлечения пользователей включая повторные визиты; внешняя причина: случилось событие которое как-то привело пользователей на страницу; ошибка в данных. Аномальное падение 31.03.2018 возможно из-за внутренней технической ошибки или внешних причин ограничивающих доступ к сайту.
- Типичная продолжительности сессии (по моде) крайне небольшая: 60 секунд.
- Retention rate низкий (хотя тут нужно сравнивать с аналогичными продуктами - может и нормальный) и в целом имеет тенденцию к снижению с ростом времени жизни когорты (что в принципе нормально)
##### 3. Метрики электронной коммерции
- Среднее время между первым посещением сайта и первой покупкой составляет 16 дней, однако распределение ненормальное и минимум 50% процентов заказов (медиана) совершается в день первого посещения.
- Среднее количество покупок на одного покупателя за 6 месяцев: 1.24
- Средний чек за весь период равен 5. При оценке по месяцам видны колебания с минимальными значениями в июне 2017 и январе 2018. Максимальный средний чек был в декабре 2017.
- Средний LTV за 6 месяцев по когортам с lifetime не моложе 5 месяцев 7.97. При оценке по месяцам видно что основную ценность клиент создает в первый месяц, а в дальнейшие месяцы прирост LTV небольшой. При этом разные когорты немного отличаются по LTV. Выделяется когорта начавшаяся в сентябре 2017: максимальное LTV за 6 мес за счет большого прироста в декабре 2017.

#### Итоги когортного анализа. Перспективные для компании когорты клиентов.
Прибыльные когорты, в которых нужно удержать или повысить retention
- источник_трафика 4, дата начала: ноябрь 2017
- источник 5, сентябрь 2017
- источник 9, все даты
- источник 1, июнь-июль 2017
- источник 2, сентябре 2017 и декабре 2017 
