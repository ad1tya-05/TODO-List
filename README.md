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

  
    
    <script>
        // JavaScript code
    </script>
</body>
</html>




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






