Описание источников данные
==========================

1. [Бухгалтерская (финансовая) отчетность предприятий и организаций за 2013 год](http://www.gks.ru/opendata/dataset/7708234640-bdboo2013)
2. [Описание столбцов CSV файла](http://www.gks.ru/opendata/storage/7708234640-bdboo2013/structure-20131231t000000.TTL)
3. [Машиночитаемая форма бухгалтерской отчетности](http://www.consultant.ru/document/cons_doc_LAW_32453/58684ab73dd1585821052f9b58c59ef96b907f8a/)
4. [О предоставлении государственной услуги](https://rg.ru/2013/11/15/buhotchet-dok.html)

Наборы данных
=============

###Гененрируются программно (Python 3.5/Anaconda):
[reader.py](https://github.com/epogrebnyak/data-rosstat-boo-2013/blob/master/reader.py) - исходные наборы данных, 
соотвестствующие файлу Росстата (265 показателей * 1,7 млн строк):
  - all2013.csv
  - all2012.csv

[slicer.py](https://github.com/epogrebnyak/data-rosstat-boo-2013/blob/master/slicer.py) - файл с ограниченным 
набором показателей (27 показателей * 1,7 млн строк):
  - merged.csv 

 
###Сохранены:
Папка [data](https://github.com/epogrebnyak/data-rosstat-boo-2013/tree/master/data), для скачивания нажать "View raw"

Предприятия с выручкой более 5 млн руб. в месяц или основными фондами более 10 млн руб. (27 показателей * 427 тыс. строк):
- main.csv  
- main.rar - (заархивированный main.csv)


Предприятия с выручкой более 1 млрд. руб. в год (27 показателей * 15,5 тыс. строк):
- bln.xls 
- bln.csv 

Переменные
==========

###Характеристики компании
- *inn*
- *year*
- *okved1*
- *region*
- *title*

###Активы
- *of* - основные средства
- *of_prev* - основные средства на конец предыдущего периода 
- *ta_fix* - внеоборотные активы
- *ta_nonfix* - оборотные активы
- *ta* - активы всего

###Пассивы
- *tp_cap* - капитал
- *debt_long* - долгосрочные займы
- *tp_long* - долгосрочные обязательства
- *debt_short* - кракосрочные займы
- *tp_short* - краткосрочные обязательства 
- *tp* - пассивы всего 

###Отчет о прибыли и убытках 
- *sales* - выручка
- *sales_prev* - выручка прошлого года
- *exp_interest* - процентные платежи 
- *profit_operational* - прибыль от продаж
- *profit_before_tax* - прибыль до налогообложения
 
###Движение денежных средств
- *cash_oper_inflow* - вcего операционные поступления
- *cash_oper_inflow_sales* - поступления от продаж
- *paid_to_supplier* - платежи поставщикам
- *paid_to_worker* - платежи работникам
- *cash_interest* - процентные платежи 
- *cash_investment_of* - создание внеоборотных активов

[Определения переменных в коде программы](https://github.com/epogrebnyak/data-rosstat-boo-2013/blob/master/column_names.py#L328-L444)

Возможные расчеты
=================

### 1. Подготовительные оценки
- Проверка целостности данных (балансовые соотношения)
- Правильность отбора переменных (приближения):
  - доля кратко/долгосрочных займов в обязательствах
  - поступления от продаж/всего операционные поступления
  - основные средства/внеоборотные активы
- Оценить отсутствующие показатели (например, EBITDA)
- Дескриптивная статистика

### 2. Круг предприятий
Выявите:
  - предприятия-банкроты 
  - предприятия-инвестицонные SPV
  - малые и средние предприятия  

### 3. Связь с макроданными
####3.1 
Просуммировать макроэкономические переменные по выбранному набору данных:
  - выпуск
  - произведенная добавленная стоимость (ВВП) 
  - инвестиции
  - оплата труда
  - основные фонды
  - кредиты, в том числе долгосрочные 

####3.2. 
Cравнить с отчетными макропоказателями, определить охват используемого набора данных. 
  
### 4. Анализ по отдельным маропоказателям
- Выпуск
  - Фондоотдача. На сколько может вырасти выпуск на незагруженных мощностях?

- Инвестиции
  - Прирост основных средств равен расходам на инвестиции?
  - За счет чего финансировались инвестиции: долгосрочный кредит?
  - Какие предприятия  инвестируют: с наибольшей прибылью, с максимальным ростом продаж? с другими параметрами?

- Оплата труда   
```
  salary = 29792 # средняя месячная зарплата в 2013 году
  employed = 71391.46 #количество занятых в экономике
```

- Производственная функция: 
  - Предположим, выпуск зависит от основных фондов и труда: ```X = A * of^a * w^b```.   
  - Оцените и интерпретируйте параметры производственной функции. 
  - Проделайте задание в разрезе по отраслям. 
    
### 5. Проектное финансирование   
- Что определяет среднюю процентную ставку предприятия по кредитам?
- Оцените условия окупаемости инвестиций в разрезе отраслей (средний срок окупаемости).  

### Прочие вопросы
- Анализ финансового состояния 
- Показатели в отраслевом / региональном разрезе 
- Малые предприятия
- Неравномерность и концентрация в отрасли
  - Неравномерность выборки (пример, суммарный финансовый результат - как складывается) 
  - Уровень концентарции в отрасли, чем объясняется (капиталоемкость?)
