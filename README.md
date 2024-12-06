<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do List</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="todo-container">
        <h1>To-Do List</h1>
        <input type="text" id="task-input" placeholder="Add a new task...">
        <button id="add-btn">Add Task</button>
        <ul id="todo-list"></ul>
    </div>
    <script src="script.js"></script>
</body>
</html>

body {
    font-family: Arial, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
    background-color: #f4f4f4;
}

.todo-container {
    background-color: white;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    width: 300px;
    text-align: center;
}

h1 {
    margin-bottom: 20px;
}

input {
    width: 80%;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
    margin-right: 10px;
}

button {
    padding: 10px;
    border: none;
    background-color: #4CAF50;
    color: white;
    border-radius: 5px;
    cursor: pointer;
}

button:hover {
    background-color: #45a049;
}

ul {
    list-style-type: none;
    padding: 0;
    margin-top: 20px;
}

li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #f9f9f9;
    margin-bottom: 10px;
    padding: 10px;
    border-radius: 5px;
}

li.completed {
    text-decoration: line-through;
    color: #888;
}

li button {
    background-color: red;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

li button:hover {
    background-color: darkred;
}


// Get references to the input field, button, and list
const taskInput = document.getElementById('task-input');
const addButton = document.getElementById('add-btn');
const todoList = document.getElementById('todo-list');

// Function to add a new task to the list
function addTask() {
    const taskText = taskInput.value.trim();
    
    if (taskText === '') {
        alert('Please enter a task!');
        return;
    }

    // Create new list item
    const li = document.createElement('li');
    
    // Create span for task text
    const span = document.createElement('span');
    span.textContent = taskText;
    li.appendChild(span);
    
    // Create the "Complete" button
    const completeButton = document.createElement('button');
    completeButton.textContent = 'Complete';
    completeButton.onclick = function() {
        li.classList.toggle('completed');
        completeButton.textContent = li.classList.contains('completed') ? 'Undo' : 'Complete';
    };
    li.appendChild(completeButton);
    
    // Create the "Delete" button
    const deleteButton = document.createElement('button');
    deleteButton.textContent = 'Delete';
    deleteButton.onclick = function() {
        todoList.removeChild(li);
    };
    li.appendChild(deleteButton);

    // Append the new task to the list
    todoList.appendChild(li);

    // Clear the input field
    taskInput.value = '';
}

// Add event listener to add button
addButton.addEventListener('click', addTask);

// Allow pressing "Enter" to add task
taskInput.addEventListener('keypress', function(event) {
    if (event.key === 'Enter') {
        addTask();
    }
});
