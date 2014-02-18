AutoFilter-V1
=============

A new branch of MODX Evolution extras
трацией ресурсов для MODX Evolution / Clipper CMS

Описание
----------------
Расширение AutoFilter V1 является частью библиотеки x-evo. Задача данного расширения - дать возможность быстрого создания формы фильтрации ресурсов либо по полям документов, либо по значениям TV. Существует возможность создавать собственные типы фильтрации по произвольным таблицам в БД путем написания моделей данных.


Принцип работы
----------------
После установки сниппета, требуется создать 2 чанка: для формы фильтрации и для вывода результатов. В форме фильтрации обязательным является скрытое поле с id вызова сниппета. Остальные поля задаются в виде плейсхолдеров. Пример:

//test.form.tpl//

```
<form name="form" id="form" method="get" action="">
    <input type="hidden" name="afid" value="[+test.id+]" />
    Заголовок: [+test.optpagetitle_select:pt+] <br>
    Шаблон: [+test.opttemplate_select:tpl+]<br>
    TV1: [+test.opt1_select:tv1+]<br>
    <input type="submit" name="go" value="Показать" />
    <input type="submit" name="Reset" value="Сбросить" />
</form>

```

В плейсхолдерах задаются источники данных (optparent - поле parent у документа, optN - значение TV с ID=N), внешний вид поля фильтрации (select - выпадающий список). Если после двоеточия есть строка, переменная в форме будет называться, как эта строка. Если нет, то название переменной будет вида opttemplate_select.

Пример чанка с обработкой результатов:

//test.ditto.tpl//

```
Найдены [+test.items_show_count+] товаров из [+test.items_count+]: ids = [+1test.items+]

<br>
[[Ditto? &paginate=`1` &display=`6` &documents=`[+test.items+]` ]]
[+pages+]
```

Вызов AutoFilter:

```
[!autoFilter?
&id=`test`
&parents=`0`
&formTpl=`test.form.tpl`
&parseTpl=`test.ditto.tpl`
!]
[+test.form+]
[+test.result+]
```

Результатом работы сниппета будет вывод формы в плейсхолдер [+test.form+], вывод результатов в плейсхолдер [+test.result+]. 

Подробнее параметры сниппета и его возможности описаны в разделе Помощь в админ-панели MODX/Clipper