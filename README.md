# Командная строка списка дел (To Do List)

(!) прежде чем начать убедитесь что вы уже сделали [Парсинг данных: из CSV в JS в CSV](../../../parsing-data-1-csv-in-csv-out-challenge/) и вы понимаете как работает библиотека `json2csv` и `fs`

## Введение
Мы собираемся создать приложение списка дел. Наше приложение будет создаваться пошагово. Мы начнем с отображения списка элементов и будем продолжать шаг за шагом, пока не закончим добавлять все необходимые нам функции. Когда наше приложение будет готово, то в нем пользователь сможет отображать нужные ему элементы, добавлять или удалять их, а также отмечать элементы как завершенные.

По мере того, как мы создаем наше приложение, его дизайн должен соответствовать основным объектно-ориентированным принципам. Продумайте каждое решение, соблюдая [принцип единой ответственности][wikipedia srp], [разделение проблем][wikipedia soc] и другие принципы проектирования.

Во время работы над каждым выпуском, рекомендуем особенно обратить внимание на то, как *изменения* влияют на работу нашего приложения. Сколько файлов мы должны изменить при добавлении новой функции? Насколько неудобно для нас вносить каждое изменение? Были ли наши предыдущие проектные решения проще или сложнее в случаях, когда нам требовалось произвести те или иные изменения?


## Releases
### Release 0: Отображение элементов to-do листа
У нас есть файл CSV, который содержит описание некоторых элементов to-do листа (списка дел) (см. `Todo_list_data.csv`). Мы хотим начать наше приложение с отображения списка элементов (см. Рис. 1).

Прежде чем начать писать код, обязательно продумайте процесс, необходимый для отображения списка. Что нам требуется сделать? Например, нам нужно прочитать содержимое файла данных, представить список дел в JavaScript, представить каждый элемент списка в JavaScript, форматировать список для отображения и т. д. Какие еще функции здесь следует упомянуть?

После того, как мы определили функции нашего приложения, определите, какие объекты нам нужны для их выполнения, не забывая при этом применять объектно-ориентированные принципы проектирования. Затем протестируйте и разработайте эти объекты, затем выполните эти команды.

```
$ node todo_list_runner.js
- Walk the cat.
- Go to the gym.
- Buy groceries for the week.
- Call Penelope.
```
*Рисунок 1*. Пример отображения списка задач.



### Release 1: Добавление новых элементов в список
Добавьте в приложение новую функцию: пользователи должны иметь возможность добавлять новые элементы в список. При запуске приложения пользователям теперь нужно будет указать, что они хотят сделать; пользователи передадут параметры командной строки, чтобы отобразить существующий список дел или добавить новый элемент (см. Рис. 2).

При добавлении этой функции наше приложение будет обладать дополнительными функциями. Нам нужно проанализировать аргументы командной строки и записать их в файл. Для этого используйте -> `process.argv.slice(2)`.

Требуется ли нам сделать что-то ещё? Какой объект должен отвечать за эти новые функции? Было бы ли уместно сделать так, чтобы наши существующие объекты отвечали за их выполнение? Нужно ли нам создавать новые объекты?


```
$ node todo_list_runner.js list
- Walk the cat.
- Go to the gym.

$ node todo_list_runner.js add "Finish code challenge."
Appended "Finish code challenge." to the list.

$ node todo_list_runner.js list
- Walk the cat.
- Go to the gym.
- Finish code challenge.
```
*Рисунок 2*. Использование параметров командной строки для отображения списка задач или добавления сюда нового элемента.


### Release 2: Удаление элементов из списка
О, самые лучшие планы ... Иногда мы добавляем элемент в список, но по прошествии времени мы больше не хотим или больше не должны его выполнять. Вместо того, чтобы такие элементы всегда оставались в списке, добавьте функцию, которая позволит пользователям удалять элементы (см. Рис. 3).

```
$ node todo_list_runner.js list
- Walk the cat.
- Go to the gym.

$ node todo_list_runner.js remove "gym"
Removed "Go to the gym." from the list.

$ node todo_list_runner.js list
- Walk the cat.
```
*Рисунок 3*. Удаление элемента из списка.


### Release 3: Пометка элементов списка в качестве завершенных задач
Что нам следует сделать, когда мы завершаем какое-нибудь дело из нашего списка? Учитывая текущий набор функций, нам пришлось бы удалить его из списка элементов; в другом случае, нам, похоже, все равно нужно принимать дополнительные меры. Добавьте функцию, которая позволяет помечать в приложении выполненные задания (см. Рис. 4).

Завершение этой функции будет связано с рядом изменений. Нам нужно будет обновить наш файл данных, чтобы сохранить в нем информацию о том, будет ли каждый элемент списка завершен. Нам нужно будет  также изменить способ представления элемента в JavaScript; в его состоянии необходимо будет отразить опцию возможности его завершения. Дополнительно нам нужно будет изменить способ отображения списка, а также обновить наши тесты. Какие еще изменения нам понадобятся? По мере добавления этой опции, помните о том, как наши дизайнерские решения облегчают и/или препятствуют происходящим изменениям.

```
$ node todo_list_runner.js list
[ ] Walk the cat.
[ ] Go to the gym.

$ node todo_list_runner.js complete "walk the cat"
Marked "Walk the cat." as complete.

$ node todo_list_runner.js list
[X] Walk the cat.
[ ] Go to the gym.
```
*Рисунок 4*. Пометка элемента в качестве завершенного задания

### Релиз 4: Изменение хранилища данных
Наше приложение списка дел отлично работает, однако оно ограничивается терминалом. Без удобных для них компьютеров пользователи не смогут получить доступ к своим спискам. Но что если бы пользователи могли распечатывать свои списки, прежде чем отправляться на работу или начинать что-то делать? Чтобы облегчить печать списка дел, мы отформатируем наш файл данных для придания ему более читабельного вида.

Обновите файл хранилища данных, в котором мы храним данные элемента. Мы перейдем от использования CSV-файла к использованию текстового файла формата (.txt), отформатированного так, как это показано на Рисунке 5.

Мы осуществляем изменения в файле хранилища данных. Обратите внимание на эффект, который это изменение оказывает на наше приложение. Например, мы больше не будем использовать библиотеку JavaScript `CSV`, поэтому нам нужно будет обновить способ чтения и записи данных элемента. В каких объектах мы ожидаем, что произойдут изменения? Какие объекты действительно оказались затронуты?



```text
[X] Walk the cat.
[ ] Go to the gym.
[X] Buy groceries for the week.
[ ] Call Penelope.
[ ] Finish code challenge.
[ ] Book hotel for vacation.
```
*Рисунок 5*. Формат для нового файла данных.


## Заключение
Подумайте о функциях нашего приложения. В нем имеются четыре функции, имеющие наибольшую приоритетность.

1. Манипулирование объектами JavaScript, находящимися в памяти, которые моделируют реальный список дел (Модель).
2. Форматирование информации и ее отображение пользователю (Вид).
3. Интерпретация пользовательского ввода информации и последующее выполнение соответствующего действия (Контроллер).
4. Чтение и запись данных из файла данных .

Model-View-Controller - это шаблон проектирования, который мы будем использовать для проектирования почти всех наших приложений - как наших приложений с командной строкой, так и наших веб-приложений в Elbrus Coding Bootcamp. Чуть позже мы узнаем больше об этом шаблоне проектирования. Какие части нашего списка задач представляют собой модель, вид и контроллер?

[wikipedia soc]: http://en.wikipedia.org/wiki/Separation_of_concerns
[wikipedia srp]: http://en.wikipedia.org/wiki/Single_responsibility_principle
# JS-todoList-Node
# JS-todoList-Node
