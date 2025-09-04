# SCT_WD_4
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>To-Do Web App</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f4f9;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      margin: 0;
    }
    .container {
      background: #fff;
      padding: 20px;
      border-radius: 12px;
      width: 400px;
      box-shadow: 0px 4px 8px rgba(0,0,0,0.1);
    }
    h2 {
      text-align: center;
      margin-bottom: 20px;
    }
    .input-group {
      display: flex;
      gap: 5px;
      margin-bottom: 15px;
      flex-wrap: wrap;
    }
    input, button {
      padding: 8px;
      font-size: 14px;
    }
    input[type="text"], input[type="datetime-local"] {
      flex: 1;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
    button {
      cursor: pointer;
      border: none;
      border-radius: 5px;
      background: #4CAF50;
      color: white;
      transition: 0.3s;
    }
    button:hover {
      background: #45a049;
    }
    ul {
      list-style: none;
      padding: 0;
    }
    li {
      background: #f9f9f9;
      margin-bottom: 10px;
      padding: 10px;
      border-radius: 8px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .completed {
      text-decoration: line-through;
      color: gray;
    }
    .actions button {
      margin-left: 5px;
      padding: 5px 8px;
      font-size: 12px;
    }
    .date {
      font-size: 12px;
      color: #666;
      margin-left: 8px;
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>To-Do App</h2>
    <div class="input-group">
      <input type="text" id="taskInput" placeholder="Enter task">
      <input type="datetime-local" id="dateTimeInput">
      <button onclick="addTask()">Add</button>
    </div>
    <ul id="taskList"></ul>
  </div>

  <script>
    function addTask() {
      const taskInput = document.getElementById("taskInput");
      const dateTimeInput = document.getElementById("dateTimeInput");
      const taskList = document.getElementById("taskList");

      const taskText = taskInput.value.trim();
      const taskDate = dateTimeInput.value;

      if (taskText === "") {
        alert("Please enter a task!");
        return;
      }

      const li = document.createElement("li");
      const span = document.createElement("span");
      span.textContent = taskText;

      if (taskDate) {
        const dateSpan = document.createElement("span");
        dateSpan.textContent = " (" + new Date(taskDate).toLocaleString() + ")";
        dateSpan.classList.add("date");
        span.appendChild(dateSpan);
      }

      li.appendChild(span);

      const actions = document.createElement("div");
      actions.classList.add("actions");

      // Complete Button
      const completeBtn = document.createElement("button");
      completeBtn.textContent = "✓";
      completeBtn.onclick = () => {
        span.classList.toggle("completed");
      };

      // Edit Button
      const editBtn = document.createElement("button");
      editBtn.textContent = "Edit";
      editBtn.onclick = () => {
        const newTask = prompt("Edit task:", taskText);
        if (newTask !== null && newTask.trim() !== "") {
          span.firstChild.textContent = newTask;
        }
      };

      // Delete Button
      const deleteBtn = document.createElement("button");
      deleteBtn.textContent = "✗";
      deleteBtn.onclick = () => li.remove();

      actions.appendChild(completeBtn);
      actions.appendChild(editBtn);
      actions.appendChild(deleteBtn);

      li.appendChild(actions);
      taskList.appendChild(li);

      // Clear input
      taskInput.value = "";
      dateTimeInput.value = "";
    }
  </script>
</body>
</html>
