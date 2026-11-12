# React Lab Exercise 14: Fetch Student Details Using an API in React

## Name: Aravindan T

## Roll no: 2305001003

## Department: CSE

## AIM

To develop a React application in which a student clicks the View Details button, the application fetches student data from an API using fetch(), receives the response in JSON format, and displays the details on the screen using React Hooks.

## PROGRAM

### i) App.jsx

```javascript
import { useState } from "react";
import "./App.css";

function App() {
  const [student, setStudent] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState("");

  async function getStudentDetails() {
    setLoading(true);
    setError("");
    setStudent(null);

    try {
      const response = await fetch(
        "https://jsonplaceholder.typicode.com/users/1"
      );

      if (!response.ok) {
        throw new Error("Failed to fetch student details");
      }

      const data = await response.json();
      setStudent(data);
    } catch (err) {
      setError("Unable to load details. Please try again.");
    } finally {
      setLoading(false);
    }
  }

  return (
    <div className="container">
      <h1>Student Management System</h1>
      <p>Click the button to fetch student details from an API.</p>

      <button onClick={getStudentDetails} disabled={loading}>
        {loading ? "Loading..." : "View Details"}
      </button>

      {loading && <p>Fetching data from the API...</p>}

      {error && <p className="error">{error}</p>}

      {student && (
        <div className="student-card">
          <h2>Student Details</h2>
          <p><strong>ID:</strong> {student.id}</p>
          <p><strong>Name:</strong> {student.name}</p>
          <p><strong>Email:</strong> {student.email}</p>
          <p><strong>City:</strong> {student.address.city}</p>
        </div>
      )}
    </div>
  );
}

export default App;
```

### ii) App.css

```css
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f1f5f9;
}

.container {
  max-width: 600px;
  margin: 60px auto;
  padding: 25px;
  text-align: center;
  background: white;
  border-radius: 12px;
}

h1 {
  color: #1d4ed8;
}

button {
  background: #2563eb;
  color: white;
  border: none;
  padding: 12px 22px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 16px;
}

button:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.student-card {
  margin-top: 25px;
  padding: 20px;
  background: #dbeafe;
  border-radius: 8px;
  text-align: left;
}

.error {
  color: #dc2626;
}
```

## OUTPUT
<img width="1125" height="616" alt="image" src="https://github.com/user-attachments/assets/06f35a31-adee-419f-b94c-19b17a7f3a92" />

## RESULT

Thus, a React application was developed successfully to fetch student details from a REST API using fetch() and React Hooks. The application handles loading and error states and displays the retrieved JSON data on the screen.
