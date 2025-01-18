# project-manager-18.01.25
Readme

класс task
Свойства
$title: Название задачи.
$description: Описание задачи.
$status: Статус задачи (по умолчанию "Не выполнено").
Конструктор
public function __construct($title, $description)
Инициализирует свойства $title и $description, устанавливая статус по умолчанию.
Деструктор
public function __destruct()
Выводит сообщение о том, что задача удалена из памяти.
Магический метод __call
public function __call($method, $args)
Параметры метода
$method: Имя вызываемого метода (строка). Это имя метода, который был вызван, но не существует в классе.
$args: Массив аргументов, переданных в метод. Это позволяет передавать значения при вызове методов set и get.
Действия в методе
1.	Извлечение имени свойства:
$property = strtolower(substr($method, 3));
substr($method, 3): Извлекает подстроку из имени метода, начиная с четвёртого символа (индекс 3). Это необходимо, чтобы убрать префикс set или get.
strtolower(...): Приводит полученную подстроку к нижнему регистру. Это позволяет работать с именами свойств независимо от регистра.
Например, если был вызван метод setStatus, то переменная $property будет содержать строку status.
2.	Установка значения свойства:
if (strpos($method, 'set') === 0) $this->$property = $args[0];
strpos($method, 'set') === 0: Проверяет, начинается ли имя метода с set. Если да, это означает, что вызывается метод для установки значения свойства.
$this->$property = $args: Устанавливает значение свойства на основе первого аргумента, переданного в метод. Например, если вызван setStatus('Выполнено'), то статус задачи будет установлен на "Выполнено".
3.	Получение значения свойства:
if (strpos($method, 'get') === 0) return $this->$property ?? null;
strpos($method, 'get') === 0: Проверяет, начинается ли имя метода с get. Если да, это означает, что вызывается метод для получения значения свойства.
return $this->$property ?? null: Возвращает текущее значение свойства. Оператор ?? (null coalescing operator) возвращает значение свойства $this->$property, если оно существует; в противном случае возвращает null.
Магический метод __toString
public function __toString()
Возвращает строковое представление задачи в формате "Задача: <название> — <статус>".









Класс project
Свойства класса
$name: строка, представляющая название проекта.
$tasks: массив, содержащий задачи, связанные с проектом. Инициализируется пустым массивом.
Конструктор
public function __construct($name)
$name: Название проекта (строка).
При создании нового объекта Project конструктор инициализирует свойство $name, устанавливая название проекта.
Деструктор
public function __destruct()
Деструктор вызывается при уничтожении объекта. Он выводит сообщение о завершении проекта, включая название проекта.
Метод addTask
public function addTask(Task $task)
$task: Объект класса Task, который нужно добавить в проект.
Этот метод добавляет задачу в массив $tasks. Задачи могут быть добавлены в любой момент после создания объекта проекта.
Магический метод __toString
public function __toString()
Действие: Этот метод возвращает строковое представление объекта. В данном случае он формирует строку вида "Проект: <название> , Задач: <количество задач>", что позволяет удобно выводить информацию о проекте при использовании функции echo.


Index php 
Объяснение кода
1.	Подключение классов:
require 'Project.php';
require 'Task.php';
Подключает файлы с определениями классов Project и Task.
2.	Создание проекта:
$project = new Project("Проект");
Создаёт новый объект Project с названием "Проект".
3.	Создание задач:
$task1 = new Task("Задача 1", "Описание 1");
$task2 = new Task("Задача 2", "Описание 2");
Создаёт два объекта Task с названиями и описаниями.
4.	Добавление задач в проект:
$project->addTask($task1);
$project->addTask($task2);
Добавляет задачи в массив задач проекта.
5.	Вывод информации о проекте:
echo $project . "\n";
Выводит название проекта и количество задач.
6.	Вывод информации о первой задаче:
echo $task1 . "\n";
Выводит информацию о задаче $task1.
7.	Изменение статуса задачи:
$task1->setStatus("Выполнено");
Устанавливает статус задачи $task1 на "Выполнено".
8.	Вывод обновлённой информации о задаче:
echo $task1 . "\n";
Снова выводит информацию о задаче, теперь со статусом "Выполнено".


