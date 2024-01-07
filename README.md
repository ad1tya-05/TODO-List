<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Task Management</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css">
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.9.3/dist/umd/popper.min.js"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/js/bootstrap.min.js"></script>
</head>
<body>
//This part sets up the basic structure of the HTML page. It includes references to Bootstrap CSS and JavaScript libraries for styling and functionality.//
    <div class="container">
        <h1 class="text-center">Task Management</h1>
        <div class="form-group">
            <label for="task-input">Task</label>
            <input type="text" class="form-control" id="task-input" placeholder="Enter Task">
        </div>
        <button class="btn btn-primary" id="add-task-btn">Add Task</button>
        <table class="table mt-3">
            <thead>
                <tr>
                    <th>Task</th>
                    <th>Action</th>
                </tr>
            </thead>
            <tbody id="task-list">
            </tbody>
        </table>
    </div>

  
  ///Within the <body> tag, this section creates the main content of the page:

A container <div> that holds the page content.
An input field (<input>) for users to enter a task.
An "Add Task" button (<button>) to add the task.
A table (<table>) with a header row (<thead>) and a body (<tbody>) where the tasks will be displayed. Initially, this area is empty (id="task-list").///
  
    
    <script>
        // JavaScript code
    </script>
</body>
</html>


//The JavaScript section handles the functionality of the page. It consists of three main functions: loadTasks(), addTask(), and event listeners.//


function loadTasks() {
    // Connect to the backend API to fetch the list of tasks
    fetch('https://api.example.com/tasks')
        .then(response => response.json())
        .then(data => {
            // Loop through the retrieved data and create table rows for each task
            data.forEach(task => {
                let row = document.createElement('tr');
                row.innerHTML = `
                    <td>${task.title}</td>
                    <td>
                        <button class="btn btn-primary">Edit</button>
                        <button class="btn btn-danger">Delete</button>
                    </td>
                `;
                // Append the table row to the task list table body
                document.getElementById('task-list').appendChild(row);
            });
        });
}

//This function loads tasks by making a GET request to the specified API endpoint. Upon receiving the data, it creates table rows for each task and appends them to the table body.//

function addTask() {
    // Get the task input value
    let task = document.getElementById('task-input').value;
    // Connect to the backend API to add a new task
    fetch('https://api.example.com/tasks', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({ title: task })
    })
    .then(response => response.json())
    .then(data => {
        // Log success message and reload tasks to update the list
        console.log('Task added successfully:', data);
        loadTasks();
    });
}

// Event listener for the "Add Task" button click
document.getElementById('add-task-btn').addEventListener('click', addTask);

// Initially load tasks when the page loads
loadTasks();


//This addTask() function handles adding new tasks. It takes the value entered in the input field, sends a POST request to the API with the task title in JSON format, and upon success, reloads the tasks to update the displayed list.

The addEventListener method attaches a click event listener to the "Add Task" button, so when it's clicked, the addTask() function is called.

Lastly, loadTasks() is called at the end to initially load tasks when the page loads.//





