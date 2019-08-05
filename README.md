## 1. Используйте === вместо ==.
В JavaScript существует два разных типа операций сравния: === / !== и == / !=. Считается хорошим тоном всегда использовать первую пару для сравнения. Если два операнда одного типа и значения, то === вернет true, а !== false.

***

## 2. Избегайте использования eval().
Для тех кто не знаком, функция «eval» дает нам доступ к компилятору JavaScript. Т.е. мы можем выполнить команду записанную в строковой переменной, которую передадим в качестве параметра в eval.
Это не только замедлит вашу программу, но еще и предполагает возниковение огромной дыры безопасности вашего приложения. Это плохо. По возможности избегайте этого.
***

## 3. Переместите скрипты вниз страницы.
Основная цель этого совета — заставить страницу грузиться как можно быстрее. Когда браузер грузит скрипт он не продолжит рендеринг пока весь файл не будет загружен. Таким образом пользователю придется ждать дольше.
Если ваши JS скрипты служать для добавления функционала — например, обработки кликов кнопки то вам стоит перенести скрипты вниз поставив их перед закрывающимся тегом body. 
```
<p>And now you know my favorite kinds of corn. </p>  
<script type="text/javascript" src="path/to/file.js"></script>  
<script type="text/javascript" src="path/to/anotherFile.js"></script>  
</body>  
</html>
```
***

## 4. Комментарии.
**Должен быть минимум комментариев, которые отвечают на вопрос "что происходит в коде?"**

Хороший код и так понятен.

Об этом замечательно выразился Р.Мартин в книге «Чистый код»: «Если вам кажется, что нужно добавить комментарий для улучшения понимания, это значит, что ваш код недостаточно прост, и, может, стоит переписать его».

Если у вас образовалась длинная «простыня», то, возможно, стоит разбить её на отдельные функции, и тогда из их названий будет понятно, что делает тот или иной фрагмент.

Да, конечно, бывают сложные алгоритмы, хитрые решения для оптимизации, поэтому нельзя такие комментарии просто запретить. Но перед тем, как писать подобное – подумайте: «Нельзя ли сделать код понятным и без них?»

А какие комментарии полезны и приветствуются?

**Архитектурный комментарий – «как оно, вообще, устроено».**

Какие компоненты есть, какие технологии использованы, поток взаимодействия. О чём и зачем этот скрипт. Взгляд с высоты птичьего полёта. Эти комментарии особенно нужны, если вы не один, а проект большой.

Для описания архитектуры, кстати, создан специальный язык UML, красивые диаграммы, но можно и без этого. Главное – чтобы понятно.

**Справочный комментарий перед функцией – о том, что именно она делает, какие параметры принимает и что возвращает.**
**…Но куда более важными могут быть комментарии, которые объясняют не что, а почему в коде происходит именно это!**

Как правило, из кода можно понять, что он делает. Бывает, конечно, всякое, но, в конце концов, вы этот код видите. Однако гораздо важнее может быть то, чего вы не видите!

Почему это сделано именно так? На это сам код ответа не даёт.

*Один из показателей хорошего разработчика – качество комментариев, которые позволяют эффективно поддерживать код, возвращаться к нему после любой паузы и легко вносить изменения.*
***

## 5. Всегда, всегда используйте точку с запятой.
Технически, большинство браузеров позволят вам не использовать их.
``` js
var someItem = 'some string'  
function doSomething() {  
  return 'something'  
}  
```


Но использование подобную практики потенциально может привести к гораздо более большим и что еще хуже плохо отлавливаемым проблемам.
``` js
var someItem = 'some string';  
function doSomething() {  
  return 'something';  
}  
```
***

## 6. Уменьшите количество глобальных переменных.
Сведением количества глобальных переменных к одному, вы значительно снижаете шансы нежелательного взаимодействия с другими приложениями, виджетами или библиотеками.
``` js
var name = 'Jeffrey';  
var lastName = 'Way';  
  
function doSomething() {...}  
  
console.log(name); // Jeffrey -- or window.name  
```
``` js
var DudeNameSpace = {  
   name : 'Jeffrey',  
   lastName : 'Way',  
   doSomething : function() {...}  
}  
console.log(DudeNameSpace.name); // Jeffrey  
```
Мы уменьшили количество глобальных переменных до одного, странным образом названного, обьекта «DudeNameSpace».
***

## 7.  Не передавайте строку в «SetInterval» или «SetTimeOut».
Рассмотрим следующий код:
``` js
setInterval(  
"document.getElementById('container').innerHTML += 'My new number: ' + i", 3000  
);  
```
Он не только неэффективен, но еще и работает так же как и «eval». Результаты будут такие-же. Вместо этого передавайте функцию в качестве аргумента
``` js
setInterval(someFunction, 3000);  
```
***

## 8. Используйте {} вместо New Object().
Есть несколько путей для создания объектов в JavaScript. Возможно наиболее традиционный это использование конструктора «new», например
``` js
var o = new Object();  
o.name = 'Jeffrey';  
o.lastName = 'Way';  
o.someFunction = function() {  
   console.log(this.name);  
}  
```
Хотя этот метод получил штамп «плохой практики» он таковой не является. Вместо него, я рекомендую использовать более надежный метод c литералом обьекта
``` js
var o = {  
   name: 'Jeffrey',  
   lastName = 'Way',  
   someFunction : function() {  
      console.log(this.name);  
   }  
};  
```
Заметка — если вы хотите создать пустой обьект, то {} сделает это
``` js
var o = {};  
```
Литералы обьектов позволят нам писат код, который поддерживает кучу функционала все еще сохраняя относительную непосредственность. Не нужно больше вызывать конструкторы напрямую или корректировать порядок аргументов переданных в функцию.
***

## 9. Не используйте короткую запись.
Технически можно писать код без фигурных скобок и точек с запятой. Большинство браузеров корректно воспримет следующий код:
``` js
if(someVariableExists)  
   x = false
```
Как насчет этого?
``` js
if(someVariableExists)  
   x = false  
   anotherFunctionCall();  
```
Кто-то может посчитать что это эквивалентно следующему
``` js
if(someVariableExists) {  
   x = false;  
   anotherFunctionCall();  
}  
```
И он будет неправ. Потому что на самом деле для компилятора это выглядит так:
``` js
if(someVariableExists) {  
   x = false;  
}  
anotherFunctionCall();  
```
Как вы заметили отступ маскирует функционал фигурных скобок. Излишне говорить, что это ужасная практика, которую следует избегать любой ценой. Единственное где вы можете опустить использование скобок это в однострочных выражениях, но даже это вызывает кучу споров.
``` js
if(2 + 2 === 4) return 'nicely done';  
```
***

## 10. Автоматизированные средства проверки.
Существуют средства, проверяющие стиль кода.

Самые известные – это:

**JSLint** – проверяет код на соответствие стилю JSLint, в онлайн-интерфейсе вверху можно ввести код, а внизу различные настройки проверки, чтобы сделать её более мягкой.
**JSHint** – вариант JSLint с большим количеством настроек.
В частности, JSLint и JSHint интегрированы с большинством редакторов, они гибко настраиваются под нужный стиль и совершенно незаметно улучшают разработку, подсказывая, где и что поправить.

Побочный эффект – они видят некоторые ошибки, например необъявленные переменные. У меня это обычно результат опечатки, которые таким образом сразу отлавливаются.
***
