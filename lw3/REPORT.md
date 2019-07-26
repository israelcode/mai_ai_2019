# Отчет по лабораторной работе
## по курсу "Искусственный интеллект"

### Студенты: 

| ФИО       | Роль в проекте                     | Оценка       |
|-----------|------------------------------------|--------------|
| Чекушкин Д.И. | механизм вывода, заполнение базы знаний, сплочение команды |  4        |
| Шевчук П.В. | описание предметной области, заполнение базы знаний, тестирование и отладка | 4      |
| Григорьева М.А.| задание и сохранение вопросов, отчет, заполнение базы знаний |   4   |
| Лукашкин К.В.   | механизм извлечения данных, заполнение базы знаний, графическая иллюстрация |   4       |

## Результат проверки

| Преподаватель     | Дата         |  Оценка       |
|-------------------|--------------|---------------|
| Сошников Д.В. |   15.05.2019           |   4            |

> Выбрана недостаточно актуальная тема работы, система скорее похожа на квест (отгадай игрока), чем на реальную помощь эксперта. Использованное представление знаний в системе не-иерархично, а по сути дела представляет собой таблицу (каждый игрок характеризуется определенным набором фиксированных признаков). В реальности знания в голове человека устроены сильно сложнее.

## Тема работы

Школы скаутов не существует. Должен быть футбольный опыт, а лучше – футбольные связи, чтобы о твоем опыте кто-то узнал. Связи – ракета, которая выносит тебя наверх. Обычно в эту профессию идут завязавшие футболисты, неудавшиеся тренеры или везунчики, которые любят смотреть футбол и делать выводы.
Чтобы использовать нашу экспертную систему, не нужно быть везунчиком. Достаточно уметь пользоваться компьютером, запустить программу и ввести нужные характеристики.
Если вдруг эта система так и не дойдет до мировых скаутов, то ее смогут использовать просто киберспортсмены боготворящие Фифу.

## Концептуализация предметной области

Результаты концептуализации предметной области:
 - выделенные понятия: Футболист, Позиция, Физические характеристики, Общие навыки, Особые навыки
 - тип получившейся онтологии - иерархия
 - Физические характеристики, Общие навыки, Особые навыки - знания  динамические; Футболист, Позиция - статические
 - Из предметной области было выбрано 100 более-менее известных футболистов и, соответственно, разделены на между участниками работы (25 на каждого).
   Каждый участник в равной степени провел исследовательскую работу своих футболистов, чтоб определить их способности и заполнить базу знаний.
 
 
Приведите графические иллюстрации:
![1](https://github.com/israelcode/mai_ai_2019/blob/master/lw3/img/%D0%B3%D1%80%D0%B0%D1%84.PNG)


## Принцип реализации системы
Для решения поставленной задачи используется система программирования SWI Prolog.
Он сосредоточен вокруг небольшого набора основных механизмов, включая сопоставление с образцом, древовидного представления структур данных и автоматического перебора с возвратами. Хорошо подходит для решения задач, где рассматриваются объекты (в частности структурированные объекты) и отношения между ними. SWI-Prolog позволяет разрабатывать приложения любой направленности, включая Web-приложения и параллельные вычисления, но основным направлением использования является разработка экспертных систем, программ обработки естественного языка, обучающих программ, интеллектуальных игр и т.п.

## Механизм вывода

Механизм вывода работает таким образом:
Пользователю задаются вопросы, в базу знаний с помощью предиката assert подгружаются новые факты (ответы пользователя),когда какое-либо решение было найдено система отвечает на вопрос.
Вывод вопросов:
```answers([], _).
answers([First|Rest], Index) :-
write(Index), write(' '), answer(First), nl,
NextIndex is Index + 1,
answers(Rest, NextIndex).
```
Первым аргументом answers - это список из идентификаторов вопросов. Например   
[goalkeeper, defender, midfielder, forward].   
Второй аргумент – номер для ввода после вопроса для идентификации выбора пользователя.   
Проходя по списку идентификаторов программа выводит номер вопроса   
(write(Index)), пробел (write(' ')), а затем сам вопрос (answer(First)).   
Здесь First – голова списка. Для каждого члена списка, который передается в answers прописаны answer(…):
```answer(tall_strong) :-
write('tall, strong').

answer(fast) :-
write('fast').

answer(no_matter) :-
write('no matter').
```
## Извлечение знаний и база знаний

Извлечение данных происходила путем восстановления  воспоминаний событий чемпионата мира 2018, ведь именно тогда большая часть населения России открыла для себя новые фамилии футболистов.
К тому же Шевчук П.В. каждый день просматривает футбольные новости и обсуждает их с Чекушкиным Д.И.
В коде за извлечение знаний отвечает это правило
```
% Находит ответ из Choices
parse(0, [First|_], First).
parse(Index, [First|Rest], Response) :-
Index > 0,
NextIndex is Index - 1,
parse(NextIndex, Rest, Response).
```
Возвращает элемент списка с заданным индексом.
## Протокол работы системы

Приведите несколько примеров работы системы, проиллюстрируйте их фрагментами деревьев вывода.
![1](https://github.com/israelcode/mai_ai_2019/blob/master/lw3/img/test1.PNG)

![2](https://github.com/israelcode/mai_ai_2019/blob/master/lw3/img/test2.PNG)

![3](https://github.com/israelcode/mai_ai_2019/blob/master/lw3/img/test3.PNG)

## Выводы

Экспертная система - это компьютерная программа, которая в некоторой области проявляет степень
 познаний равнозначную степени познания человека-эксперта (что очень удобно, ведь всем нам не 
 нравится разговаривать с консультантами в магазине).
Данная лабораторная работа помогла освежить знания курса Логическое программирование и научила работать в команде. Для повышения эффективности и скорости связи между участниками была создана беседа в Вконтакте "Foodball", куда писали только по делу.
Искренне надеемся, что это система все-таки дойдет до мировых скаутах и весь футбольный мир скоро узнает наши фамилии...