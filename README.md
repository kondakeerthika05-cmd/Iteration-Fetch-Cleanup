# Iteration-Fetch-Cleanup
Iteration + Fetch + Cleanup — Todo List with Unmount Button
📁 File Structure
src/
 ├─ components/
 │   ├─ TodoCard.jsx
 │   └─ TodosList.jsx
 ├─ App.jsx
 └─ main.jsx

✅ Step 1: Create TodoCard Component

📁 src/components/TodoCard.jsx

function TodoCard({ userId, title, completed }) {
  return (
    <div style={{ border: "1px solid #ccc", margin: "8px", padding: "8px" }}>
      <p><strong>User ID:</strong> {userId}</p>
      <p><strong>Title:</strong> {title}</p>
      <p>
        <strong>Status:</strong>{" "}
        {completed ? "Completed ✅" : "Pending ❌"}
      </p>
    </div>
  );
}

export default TodoCard;


✔ Separate component
✔ Uses props correctly

✅ Step 2: Create TodosList Component (Fetch + Cleanup)

📁 src/components/TodosList.jsx

import { useEffect, useState } from "react";
import TodoCard from "./TodoCard";

function TodosList() {
  const [todos, setTodos] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/todos")
      .then((res) => res.json())
      .then((data) => {
        setTodos(data.slice(0, 15)); // first 15 todos
      });

    // cleanup function
    return () => {
      alert("cleanup worked");
    };
  }, []);

  return (
    <div>
      <h2>Todo List</h2>
      {todos.map((todo) => (
        <TodoCard
          key={todo.id}
          userId={todo.userId}
          title={todo.title}
          completed={todo.completed}
        />
      ))}
    </div>
  );
}

export default TodosList;


✔ useEffect on mount
✔ .slice(0, 15)
✔ .map() iteration
✔ Cleanup function with alert

✅ Step 3: Handle Unmount in App.jsx

📁 src/App.jsx

import { useState } from "react";
import TodosList from "./components/TodosList";

function App() {
  const [showTodos, setShowTodos] = useState(true);

  return (
    <div>
      <button onClick={() => setShowTodos(false)}>
        Unmount Todos
      </button>

      {showTodos && <TodosList />}
    </div>
  );
}

export default App;


✔ Button unmounts component
✔ Cleanup runs automatically

✅ Step 4: Run the App
npm run dev

✔ Expected Behavior

Todos load on page load

15 todo cards rendered

Click Unmount Todos

TodosList unmounts

Alert shows:

cleanup worked

✅ Step 5: Push to GitHub
git init
git add .
git commit -m "Todo list fetch with cleanup on unmount"
git branch -M main
git remote add origin <YOUR_GITHUB_REPO_URL>
git push -u origin main
