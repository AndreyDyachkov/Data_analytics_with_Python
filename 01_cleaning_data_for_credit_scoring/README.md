## Cleaning data for credit scoring. Creditworthiness analysis
### Task:
Clean  a set of banking data and make assumptions about how different features impact the delinquency rate.

### Tools:
Python, Pandas, Numpy, Matplotlib

### Methods:
- Fixing data type
- Removing duplicates, wrong values
- Fixing structural errors
- Filling missing values with mean and median by categories
- Processing string values, grouping string values into categories 
- Converting continuous variables to categorical variables
- EDA  

### Data description:
The data contain following information:
children — number of children
days_employed — total work experience in days
dob_years — age
education
education_id
family_status
family_status_id
gender
income_type
debt — (1 / 0)
total_income - monthly income
purpose — purpose for a loan

### Stages:
#### 1. Missing and wrong values processing
- children - we found wrong values(-1 and 20), changed to 1 and 20 respectively, assuming that there were misprints.
- days_employed - We found out that pensioners and the unemployed have positive values, while the others have negative ones. Work experience in those groups is shown in hours. We converted all values into years (years_employed) and filled missing values with median by income_type.
- dob_years. We changed zero values with mean by income_type.
- education, education_id - we converted string values into lower case and decreased the number of unique values to 5.
- family_status, family_status_id - we converted values into lower case.
- gender - we found a misprint and changed it to the most popular gender (F).
- total_income - we filled missing values with median by income_type.
- purpose - we found duplicates to deal with on the next stage.

#### 2. Categorization
- We grouped purpose, total_income, years_employed, and dob_years into categories. It seems to be a correlation between those variables and the delinquency rate.

#### 3. Answering questions
- Children increase the risk of delinquency (there is growth from 7 to 9% between 0 and 1 child). Among borrowers with children, the delinquency rate fluctuates. Families with 3 children are the most reliable borrowers (apart from child-free families).
- The highest risk of not paying off on time is among common-law partners and single borrowers. However, there could be an influence of age: married or divorced people are usually older than unmarried borrowers.
- There is a relationship between the delinquency rate and income: middle and upper-middle levels (120 000 - 160 000) show the highest delinquency rate, while the lowest risk is among high income borrowers.
- The past-due rate is higher for auto and education loans, whereas mortgages and wedding loans show a lower rate of delinquency.

#### 4. Conclusion
- We can assume a relationship between the number of children and the delinquency rate, having children increases the risk of delinquency.
- Marital status also affects the delinquency rate. Unmarried borrowers have the highest risk, while widowed borrowers show the lowest risk. However, it could be influenced by age (unmarried clients are younger, whereas widowed borrowers are older).
- Income also affects the probability of paying off on time: middle and upper-middle levels show the highest delinquency rate, whereas the borrowers with high income are the most reliable ones.
- Loan purposes also affect the delinquency rate, marriage loans, and mortgages are paid off on time more frequently than education and auto loans.
- 
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
