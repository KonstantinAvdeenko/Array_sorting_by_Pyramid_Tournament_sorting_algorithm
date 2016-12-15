﻿Данная программа на языке программирования C#, 
производит сортировку массива алгоритмом пирамидально-турнирной сортировки, 
которая имеет два основных этапа – первый этап преобразование массива к первичной пирамидальной куче/ двоичному дереву, 
где основным действием является выбор наименьшего элемента массива на вершину составленной пирамиды и 
формирование турнирных листьев бинарного дерева; второй этап сортировка массива в три действия, 
где первым этапом находятся наименьшие элементы массива и переносятся на высшие уровни пирамиды с верхних 50%
всех элементов составленного двоичного дерева, следующими двумя действиями обрабатываются по 25% 
всех элементов составленного двоичного дерева. 
Данный метод хорошо сочетается с кэшированнием и подкачкой памяти выполняя сортировку в три действия, 
хоть и не имеет доказанную оценку худшего случая работы.

Основной модуль PiramidalnoTurnirnayaSortirovka содержит основную функцию: 
main – выполняющую задачу показа элементов массива до сортировки, 
данные о котором берутся из метода Vvod и передаются для сортировки в метод Tourn. 
Данный метод берет данные об отсортированном массиве из метода Tourn, 
а также производит консольный вывод уже сортированного массива из метода Vyvod.

Данная программа имеет следующие взаимодействующие между собой классы:
1)	Program – содержащий основную функцию main;
2)	Consts – статичный класс содержащий константой количество элементов массива для сортировки; 
3)	 Sort – содержит методы для сортировки массива алгоритмом пирамидально-турнирной сортировки.

Методы с которыми работает основная функция:
1)	считывание константы количества элементов массива методом А[];
2)	построение пирамидальной кучи/бинарного дерева из исходного массива методом Initialize – 
выполняет два первых действия для постройки 75% пирамидальной кучи/бинарного дерева из исходного массива, 
определяя меньший элемент в каждой турнирной паре одинакового уровня, 
тем самым оставляя не просеянным самый нижний уровень пирамидальной кучи/бинарного дерева. 
Для постройки пирамидальной кучи берутся данные листьев и их индексы узлов, 
необходимых в полном бинарном деpеве из метода Tourn. 
Этот метод передает данные о новом местоположении элементов массива в метод Readjust, 
а также вместе с данные о новом местоположении элементов массива число листьев, 
необходимых в полном бинаpном деpеве в метод Tourn;
3)	достраивание пирамидальной кучи/бинарного дерева из исходного массива методом Readjust –  
выполняет последнее действие для достройки пирамидальной кучи/бинарного дерева из исходного массива. 
Для достраивания пирамидальной кучи берутся данные листьев и их индексы узлов, 
необходимых в полном бинарном деpеве из метода Tourn, а передаются в метод Tourn 
данные о новом местоположении элементов массива;
4)	сортировка построенной пирамидальной кучи/бинарного дерева методом пирамидально-турнирной сортировки 
Tourn - сортирует построенную пирамидальную кучу методом пирамидально-турнирной сортировки, 
повтоpяет опеpации пеpемещения элементов, пpедставленных коpнем массива, 
в следующую позицию с меньшим индексом в массиве и пеpеупоpядочивает бинарное деpево. 
Передает отсортированный массив в главную функцию main;
5)	метод Vvod – создает исходный массив и присваивает ему рандомные значения, 
передает данные об исходном массиве главной функции main;
6)	метод Vyvod – берет данные об отсортированном массиве из метода Tourn и показывает отсортированный массив. 