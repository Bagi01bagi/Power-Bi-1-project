# Power-Bi-1-project

-1 шаг из сайта www.cbr.ru -> "Menu" ->Операции Банка России->Статистика->Внутридневные кредиты-> фильтр меняем  на начало самое м до сегоднящего дня -> https://www.cbr.ru/hd_base/dv/?UniDbQuery.Posted=True&UniDbQuery.From=29.06.2007&UniDbQuery.To=30.09.2024&UniDbQuery.P1=1
->копируем ссылку 

-2 шаг идем на power Bi и Получить данные -> Интернет - Вставляяем сслыку -> Выбераем 3 таблицу -> переименуем название таблицы "Объем внутредневных таблиц" и поле всего на "сумма млрд, руб"
-3 шаг нам нужна календарь - для этого  я написала в гугл "power bi calendar"->https://powerbi.tips/2017/11/creating-a-dax-calendar/ -> ГОтовый код скапировали  потом идем на POWER BI на представление отчета - Моделирование- Создать таблицу и Скапиранный код вставлем сюда

Вот этот код кстати-

Dates  = 
  GENERATE ( 
    CALENDAR ( DATE ( 2017, 1, 1 ), DATE ( 2017, 12, 31 ) ), 
    VAR currentDay = [Date]
    VAR day = DAY( currentDay )
    VAR month =  MONTH ( currentDay ) 
    VAR year =  YEAR ( currentDay )
  RETURN   ROW ( 
    "day", day, 
    "month", month, 
    "year", year )
  )
Меняем чуть чуть
Календарь = 
  GENERATE ( 
    CALENDAR ( MIN( 'Объем Внутредневные кредиты банка Россий'[Дата]), TODAY()  ), 
    VAR currentDay = [Date]
    VAR day = DAY( currentDay )
    VAR month =  MONTH ( currentDay ) 
    VAR year =  YEAR ( currentDay )
  RETURN   ROW ( 
    "День", day, 
    "Месяц", month, 
    "Год", year )
  )
4 Шаг идем на преставление отчета  выбераем на визуализацие - гистограмму с накоплением- Появляется окно где наши данные отображаеются - Выбераем что у нас будет по осьи х и по осьи у  - Например по х вставим год а по у сумму млрд руб и мы получили отчет наш первый
5 шаг Создадим ирархию для этого месяц перетаскиваем и на год тогда создается ирархия и туда же день и группируем чтоб было год , месяц ,день
6 шаг Теперь идем в наш отчет  и ось х меняем на ирархию
7 шаг ВиДЕМ ЧТо сортированы по выданным кредитам а нам надо изменить это -ДЛЯ ЭТОГО ИДЕМ  НА ...(ТРИ ТОЧКИ) И СОРТИРОВКА ПО ГРУППЕ ОСЬ 'ГОД Месяц День'
8 шаг добавим простой фильр по годам для этого идем на визуализацию и срез и на поле перетягивем год
Вот что получилось
![screnshot](https://github.com/Bagi01bagi/Power-Bi-1-project/blob/main/Внутредневные%20кредиты.png)
