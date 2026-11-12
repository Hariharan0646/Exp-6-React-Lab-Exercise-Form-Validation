# Exp 6 – React Lab Exercise: Form Validation

## NAME : Hariharan S
## REG NO : 2305001009

## Aim
To create a React form with validation for required fields, email, and password, and display appropriate error messages.

## Objectives
- To create a form using React.
- To manage form data using `useState()`.
- To validate required fields.
- To validate an email address.
- To validate password length.
- To display error messages dynamically.

## Program

### Step 1 – Create React Project

```bash
npm create vite@latest form-validation
cd form-validation
npm install
npm run dev
```

Select React as the framework and JavaScript as the variant.

### Step 2 – App.jsx

```jsx

import { useState } from "react";
import "./App.css";

function App() {
  const [formData, setFormData] = useState({
    name: "",
    email: "",
    password: "",
    phone: "",
    age: "",
    confirmPassword: ""
  });

  const [errors, setErrors] = useState({});

  const handleChange = (e) => {
    setFormData({
      ...formData,
      [e.target.name]: e.target.value
    });
  };

  const validate = () => {
    let newErrors = {};

    // Name validation
    if (formData.name.trim() === "") {
      newErrors.name = "Name is required";
    }

    // Email validation
    if (formData.email.trim() === "") {
      newErrors.email = "Email is required";
    } else if (
      !/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(formData.email)
    ) {
      newErrors.email = "Enter a valid email";
    }

    // Password validation
    if (formData.password === "") {
      newErrors.password = "Password is required";
    } else if (formData.password.length < 6) {
      newErrors.password =
        "Password must contain at least 6 characters";
    }

    // Phone validation
    if (formData.phone === "") {
      newErrors.phone = "Phone number is required";
    } else if (!/^\d{10}$/.test(formData.phone)) {
      newErrors.phone =
        "Phone number must contain exactly 10 digits";
    }

    // Age validation
    if (formData.age === "") {
      newErrors.age = "Age is required";
    } else if (Number(formData.age) < 18) {
      newErrors.age = "Age must be at least 18";
    }

    // Confirm password validation
    if (formData.confirmPassword === "") {
      newErrors.confirmPassword =
        "Confirm password is required";
    } else if (
      formData.confirmPassword !== formData.password
    ) {
      newErrors.confirmPassword = "Passwords do not match";
    }

    return newErrors;
  };

  const handleSubmit = (e) => {
    e.preventDefault();

    const validationErrors = validate();
    setErrors(validationErrors);

    if (Object.keys(validationErrors).length === 0) {
      alert("Form submitted successfully!");
    }
  };

  return (
    <div className="container">
      <h1>Registration Form</h1>

      <form onSubmit={handleSubmit}>
        <label>Name:</label>
        <input
          type="text"
          name="name"
          value={formData.name}
          onChange={handleChange}
        />
        {errors.name && <p>{errors.name}</p>}

        <label>Email:</label>
        <input
          type="text"
          name="email"
          value={formData.email}
          onChange={handleChange}
        />
        {errors.email && <p>{errors.email}</p>}

        <label>Password:</label>
        <input
          type="password"
          name="password"
          value={formData.password}
          onChange={handleChange}
        />
        {errors.password && <p>{errors.password}</p>}

        <label>Phone Number:</label>
        <input
          type="text"
          name="phone"
          value={formData.phone}
          onChange={handleChange}
        />
        {errors.phone && <p>{errors.phone}</p>}

        <label>Age:</label>
        <input
          type="number"
          name="age"
          value={formData.age}
          onChange={handleChange}
        />
        {errors.age && <p>{errors.age}</p>}

        <label>Confirm Password:</label>
        <input
          type="password"
          name="confirmPassword"
          value={formData.confirmPassword}
          onChange={handleChange}
        />
        {errors.confirmPassword && (
          <p>{errors.confirmPassword}</p>
        )}

        <button type="submit">Register</button>
      </form>
    </div>
  );
}

export default App;
```

### Step 3 – App.css

```css

.container {
  width: 350px;
  margin: 30px auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 10px;
}

h1 {
  text-align: center;
}

label {
  display: block;
  margin-top: 15px;
  font-weight: bold;
}

input {
  width: 100%;
  padding: 8px;
  margin-top: 5px;
  box-sizing: border-box;
}

p {
  color: red;
  font-size: 13px;
}

button {
  margin-top: 20px;
  padding: 10px 20px;
  width: 100%;
  background-color: blue;
  color: white;
  border: none;
  cursor: pointer;
}
```

## Output

<img width="816" height="824" alt="image" src="https://github.com/user-attachments/assets/685d2e40-6103-40b0-9f81-1d5809ca18c3" />


## Result

Thus, a React Registration Form was successfully created with form validation using the `useState()` Hook. Required fields, email format, and password length were validated, and appropriate error messages were displayed dynamically. The form was successfully submitted when all the entered details were valid.
