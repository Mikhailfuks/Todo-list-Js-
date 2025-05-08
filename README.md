<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Todo List</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <h1>Todo List</h1>
        <div class="input-section">
            <input type="text" id="taskInput" placeholder="Добавьте новую задачу">
            <button id="addButton">Добавить</button>
        </div>
        <ul id="taskList">
            <!-- Элементы списка будут добавляться здесь -->
        </ul>
    </div>
    <script src="script.js"></script>
</body>
</html>


body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
}

.container {
    background-color: #fff;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    width: 400px;
}

h1 {
    text-align: center;
    color: #333;
}

.input-section {
    display: flex;
    margin-bottom: 10px;
}

input[type="text"] {
    flex: 1;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
    margin-right: 10px;
}

button {
    background-color: #4CAF50;
    color: white;
    padding: 10px 15px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

button:hover {
    background-color: #3e8e41;
}

ul {
    list-style: none;
    padding: 0;
}

li {
    padding: 10px;
    border-bottom: 1px solid #ddd;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

li span {
    flex: 1;
}

li .delete-button {
    background-color: #f44336;
    color: white;
    border: none;
    padding: 5px 10px;
    border-radius: 5px;
    cursor: pointer;
}

li .delete-button:hover {
    background-color: #da190b;
}

li.completed span {
    text-decoration: line-through;
    color: #aaa;
}




// Получаем элементы DOM
const taskInput = document.getElementById('taskInput');
const addButton = document.getElementById('addButton');
const taskList = document.getElementById('taskList');

// Функция для добавления новой задачи
function addTask() {
    const taskText = taskInput.value.trim(); // Убираем лишние пробелы

    if (taskText !== "") {
        // Создаем элемент списка (li)
        const listItem = document.createElement('li');

        // Создаем span для текста задачи
        const taskSpan = document.createElement('span');
        taskSpan.textContent = taskText;
        listItem.appendChild(taskSpan);

        // Создаем кнопку "Удалить"
        const deleteButton = document.createElement('button');
        deleteButton.textContent = 'Удалить';
        deleteButton.classList.add('delete-button');  // добавляем класс для стилизации
        listItem.appendChild(deleteButton);

        // Добавляем обработчик события на кнопку "Удалить"
        deleteButton.addEventListener('click', function() {
            listItem.remove(); // Удаляем элемент списка
        });

        // Добавляем обработчик события на элемент списка (для отметки как выполненного)
        listItem.addEventListener('click', function(event) {
            if (event.target === taskSpan) {
                listItem.classList.toggle('completed'); // Переключаем класс "completed"
            }

        });

        // Добавляем элемент списка в список задач
        taskList.appendChild(listItem);

        // Очищаем поле ввода
        taskInput.value = "";
    }
}

// Добавляем обработчик события на кнопку "Добавить"
addButton.addEventListener('click', addTask);

// Добавляем обработчик события на поле ввода (для добавления задачи по нажатию Enter)
taskInput.addEventListener('keypress', function(event) {
    if (event.key === 'Enter') {
        addTask();
    }
});
