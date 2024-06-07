# Task CLI

Task CLI — это простой менеджер задач в командной строке, написанный на Go. Он использует библиотеку `github.com/spf13/cobra` для обработки команд CLI и BoltDB для постоянного хранения данных.

## Функциональность

- Добавление задач в список задач
- Отметка задач как выполненных
- Просмотр всех задач

## Установка

Для установки Task CLI необходимо иметь установленный Go. Выполните следующие команды:

```sh
git clone github.com/nemopss/task
cd task
go install .
```
## Использование
После установки можно использовать команду task для управления задачами. Ниже приведены доступные команды:

### Добавить задачу
Для добавления задачи используйте команду add с описанием задачи:

```sh
task add "Buy groceries"
```
или
```sh
task add Buy groceries
```
### Список задач
Для вывода всех задач используйте команду list:

```sh
task list
```
### Отметить задачу как выполненную
Для отметки задачи как выполненной используйте команду do с номером задачи:

```sh
task do 1
```
## Структура проекта
Проект состоит из следующих файлов:

- main.go: Точка входа в приложение
- cmd/: Содержит команды CLI
  - add.go: Команда для добавления задач
  - do.go: Команда для отметки задач как выполненных
  - list.go: Команда для вывода списка задач
  - root.go: Корневая команда
- db/: Содержит логику взаимодействия с базой данных
  - tasks.go: Функции для работы с базой данных задач
## Обзор кода
```main.go```  
Этот файл инициализирует базу данных и выполняет корневую команду:
- Определяет домашнюю директорию пользователя.
- Устанавливает путь к файлу базы данных.
- Инициализирует базу данных.
- Выполняет корневую команду.

```cmd/add.go```  
Определяет команду add для добавления новой задачи:
- Парсит аргументы командной строки для получения названия задачи.
- Объединяет аргументы в одну строку.
- Создает задачу в базе данных.
- Выводит сообщение о добавлении задачи.
  
```cmd/do.go```  
Определяет команду do для отметки задач как выполненных:
- Парсит аргументы командной строки для получения номеров задач.
- Получает все задачи из базы данных.
- Удаляет задачи, отмеченные как выполненные.
- Выводит сообщения о выполнении задач.

```cmd/list.go```  
Определяет команду list для вывода всех задач:
- Получает все задачи из базы данных.
- Выводит список задач, если они существуют.
- Выводит сообщение о том, что нет задач для выполнения, если список пуст.

```cmd/root.go```  
Определяет корневую команду:
- Содержит основную информацию о приложении.
  
```db/tasks.go```  
Содержит функции для работы с базой данных:

- Init: Инициализирует базу данных, создает bucket для задач, если его нет.
- CreateTask: Создает новую задачу и сохраняет её в базе данных.
- AllTasks: Получает все задачи из базы данных.
- DeleteTask: Удаляет задачу из базы данных по её ключу.
- itob и btoi: Вспомогательные функции для преобразования между целыми числами и байтами.