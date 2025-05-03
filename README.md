# codealpha_task
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>To-Do List App</title>
  <style>
  .intro {
  position: absolute;
  top: 30px;
  left: 50px;
  max-width: 300px;
}

.intro h1 {
  font-size: 1.8rem;
  margin: 0 0 10px;
  color: #333;

}

.intro p {
  font-size: 1rem;
  color: #555;
  line-height: 1.4;
  
}
.top-right-note {
  position: absolute;
  top: 30px;
  right: 30px;
  max-width: 300px;
  text-align: right;
}

.top-right-note h3 {
  margin: 0;
  font-size: 1.1rem;
  color: #333;
}

.top-right-note p {
  font-size: 0.95rem;
  color: #555;
  line-height: 1.4;
}


    body {
  font-family: 'Segoe UI', sans-serif;
  background: #f0f4f8;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.container {
  background: white;
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 5px 15px rgba(0,0,0,0.1);
  width: 100%;
  max-width: 400px;
  margin-top: 200px;
}

h1 {
  text-align: center;
  margin-bottom: 20px;
}

.input-section {
  display: flex;
  gap: 10px;
}

input {
  flex: 1;
  padding: 10px;
  border-radius: 6px;
  border: 1px solid #ccc;
}

button {
  padding: 10px 16px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}

ul {
  list-style: none;
  padding: 0;
  margin-top: 20px;
}

li {
  display: flex;
  justify-content: space-between;
  padding: 10px;
  margin-bottom: 8px;
  background-color: #f9f9f9;
  border-radius: 6px;
  align-items: center;
}

li.completed {
  text-decoration: line-through;
  opacity: 0.6;
}

li span {
  cursor: pointer;
  font-size: 18px;
  color: #ff5c5c;
}
.footer-note {
  position: absolute;
  right: 50px;
  max-width: 300px;
  text-align: right;
  margin-top: 750px;

}

.footer-note h3 {
  margin: 0;
  font-size: 1.1rem;
  color: #333;
  margin-top: 150px;
}

.footer-note p {
  font-size: 0.95rem;
  color: #555;
  line-height: 1.4;
  
}


  </style>
</head>
<body>
  <div class="intro">
    <h1> Organize Your To-Do Lists from Anywhere</h1>
    <p>Create clear, multi-functional to-do lists to easily manage your ideas and work from anywhere so you never forget anything again.</p>
  </div>
  <div class="top-right-note">
    <h1> Organize your work and life, finally.</h1>
    <p>Simplify life for both you and your team with the world’s #1 task manager and to-do list app.</p>
  </div>
  


  <div class="container">
    <h1>📝 To-Do List</h1>
    <div class="input-section">
      <input type="text" id="taskInput" placeholder="Enter your task...">
      <button onclick="addTask()">Add</button>
    </div>
    <ul id="taskList"></ul>
  </div>
  <div class="footer-note">
  <h1> Manage your to-do's from anywhere.</h1>
    <p>Create and access your to-do lists from anywhere: desktop, mobile phone, or browser tab. Now you'll never miss an idea or forget what you need to do next.</p>
  </div>

  <script>
    // Load tasks from localStorage
window.onload = () => {
  const savedTasks = JSON.parse(localStorage.getItem("tasks")) || [];
  savedTasks.forEach(task => renderTask(task.text, task.completed));
};

function addTask() {
  const taskInput = document.getElementById("taskInput");
  const taskText = taskInput.value.trim();

  if (taskText) {
    renderTask(taskText);
    saveTasks();
    taskInput.value = "";
  }
}

function renderTask(text, completed = false) {
  const li = document.createElement("li");
  li.className = completed ? "completed" : "";

  li.innerHTML = `
    <span onclick="toggleComplete(this)">${text}</span>
    <span onclick="deleteTask(this)">🗑️</span>
  `;

  document.getElementById("taskList").appendChild(li);
  saveTasks();
}

function toggleComplete(element) {
  element.parentElement.classList.toggle("completed");
  saveTasks();
}

function deleteTask(element) {
  element.parentElement.remove();
  saveTasks();
}

function saveTasks() {
  const tasks = [];
  document.querySelectorAll("#taskList li").forEach(li => {
    tasks.push({
      text: li.innerText.replace("🗑️", "").trim(),
      completed: li.classList.contains("completed")
    });
  });
  localStorage.setItem("tasks", JSON.stringify(tasks));
}

  </script>
</body>
</html>
