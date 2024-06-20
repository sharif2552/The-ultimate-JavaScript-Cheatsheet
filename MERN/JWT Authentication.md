# **<span style="color: orange;">How the Flow of Code Works</span>**

## **<font color="skyblue">Backend Setup</font>**
### **<span style="color: LightPink;">Overview</span>**
- **<span style="color: LightPink;">Description:</span>** This guide explains how to set up authentication in a MERN stack application using JWT tokens. It includes steps for user registration, login, and token verification.

### **<span style="color: LightPink;">Step 1: Setting Up Your Project</span>**
- **<span style="color: LightPink;">Description:</span>** Initialize your project and install necessary dependencies.

    ```sh
    # Initialize a new Node.js project
    npm init -y

    # Install Express, Mongoose, Bcrypt, JWT, and dotenv
    npm install express mongoose bcryptjs jsonwebtoken dotenv
    ```

### **<span style="color: LightPink;">Step 2: Setting Up Mongoose</span>**
- **<span style="color: LightPink;">Description:</span>** Mongoose is used to interact with MongoDB.

    ```js
    // Import Mongoose
    const mongoose = require('mongoose');

    // Connect to MongoDB
    mongoose.connect('mongodb://localhost:27017/yourdbname', {
        useNewUrlParser: true,
        useUnifiedTopology: true
    });

    // Create a User schema
    const userSchema = new mongoose.Schema({
        username: { type: String, required: true },
        password: { type: String, required: true }
    });

    // Create a User model
    const User = mongoose.model('User', userSchema);
    ```

### **<span style="color: LightPink;">Step 3: Setting Up Express</span>**
- **<span style="color: LightPink;">Description:</span>** Set up an Express server to handle HTTP requests.

    ```js
    // Import Express and other dependencies
    const express = require('express');
    const bcrypt = require('bcryptjs');
    const jwt = require('jsonwebtoken');
    const dotenv = require('dotenv');

    // Load environment variables
    dotenv.config();

    const app = express();

    // Middleware to parse JSON bodies
    app.use(express.json());
    ```

### **<span style="color: LightPink;">Step 4: Creating User Registration Route</span>**
- **<span style="color: LightPink;">Description:</span>** Create a route for user registration.

    ```js
    // Route to register a new user
    app.post('/register', async (req, res) => {
        try {
            const { username, password } = req.body;

            // Check if the user already exists
            const existingUser = await User.findOne({ username });
            if (existingUser) {
                return res.status(400).send('User already exists');
            }

            // Hash the password
            const hashedPassword = await bcrypt.hash(password, 10);

            // Create a new user
            const newUser = new User({ username, password: hashedPassword });
            await newUser.save();

            res.send('User registered successfully');
        } catch (err) {
            res.status(500).send('Error registering user');
        }
    });
    ```

### **<span style="color: LightPink;">Step 5: Creating User Login Route</span>**
- **<span style="color: LightPink;">Description:</span>** Create a route for user login and JWT token generation.

    ```js
    // Route to log in a user
    app.post('/login', async (req, res) => {
        try {
            const { username, password } = req.body;

            // Find the user by username
            const user = await User.findOne({ username });
            if (!user) {
                return res.status(400).send('Invalid credentials');
            }

            // Check if the password is correct
            const isMatch = await bcrypt.compare(password, user.password);
            if (!isMatch) {
                return res.status(400).send('Invalid credentials');
            }

            // Generate a JWT token
            const token = jwt.sign({ userId: user._id }, process.env.JWT_SECRET, {
                expiresIn: '1h'
            });

            res.json({ token });
        } catch (err) {
            res.status(500).send('Error logging in');
        }
    });
    ```

### **<span style="color: LightPink;">Step 6: Creating Middleware to Verify Token</span>**
- **<span style="color: LightPink;">Description:</span>** Create middleware to protect routes by verifying the JWT token.

    ```js
    // Middleware to verify JWT token
    const auth = (req, res, next) => {
        const token = req.header('Authorization').replace('Bearer ', '');
        if (!token) {
            return res.status(401).send('Access denied');
        }

        try {
            const decoded = jwt.verify(token, process.env.JWT_SECRET);
            req.user = decoded;
            next();
        } catch (err) {
            res.status(400).send('Invalid token');
        }
    };
    ```

### **<span style="color: LightPink;">Step 7: Creating a Protected Route</span>**
- **<span style="color: LightPink;">Description:</span>** Create a protected route that only accessible with a valid token.

    ```js
    // Protected route example
    app.get('/protected', auth, (req, res) => {
        res.send('This is a protected route');
    });

    // Start the server
    app.listen(3000, () => {
        console.log('Server is running on port 3000');
    });
    ```

### **<span style="color: LightPink;">Step 8: Summary</span>**
- **<span style="color: LightPink;">Description:</span>** To set up authentication in a MERN stack application using JWT tokens, follow these steps:
    1. **Set up your project**: Initialize a Node.js project and install necessary dependencies.
    2. **Configure Mongoose**: Set up Mongoose to interact with MongoDB.
    3. **Set up Express**: Create an Express server to handle HTTP requests.
    4. **Create registration route**: Implement a route to register new users with hashed passwords.
    5. **Create login route**: Implement a route to authenticate users and generate JWT tokens.
    6. **Create auth middleware**: Set up middleware to protect routes by verifying JWT tokens.
    7. **Create protected route**: Implement a protected route that requires a valid token to access.

This process ensures that your application has secure authentication with protected routes.

## **<font color="skyblue">Frontend Setup with React</font>**
### **<span style="color: LightPink;">Overview</span>**
- **<span style="color: LightPink;">Description:</span>** This guide explains how to create a React frontend for user authentication using JWT tokens. It includes steps for user registration, login, and accessing protected routes.

### **<span style="color: LightPink;">Step 1: Setting Up Your React Project</span>**
- **<span style="color: LightPink;">Description:</span>** Initialize your React project and install necessary dependencies.

    ```sh
    npx create-react-app auth-client
    cd auth-client
    npm install axios
    ```

### **<span style="color: LightPink;">Step 2: Creating Registration and Login Forms</span>**
- **<span style="color: LightPink;">Description:</span>** Create components for user registration and login.

    ```jsx
    // src/components/Register.js
    import React, { useState } from 'react';
    import axios from 'axios';

    const Register = () => {
        const [username, setUsername] = useState('');
        const [password, setPassword] = useState('');

        const handleSubmit = async (e) => {
            e.preventDefault();
            try {
                await axios.post('http://localhost:3000/register', { username, password });
                alert('User registered successfully');
            } catch (error) {
                alert('Error registering user');
            }
        };

        return (
            <form onSubmit={handleSubmit}>
                <h2>Register</h2>
                <input
                    type="text"
                    placeholder="Username"
                    value={username}
                    onChange={(e) => setUsername(e.target.value)}
                />
                <input
                    type="password"
                    placeholder="Password"
                    value={password}
                    onChange={(e) => setPassword(e.target.value)}
                />
                <button type="submit">Register</button>
            </form>
        );
    };

    export default Register;
    ```

    ```jsx
    // src/components/Login.js
    import React, { useState } from 'react';
    import axios from 'axios';

    const Login = () => {
        const [username, setUsername] = useState('');
        const [password, setPassword] = useState('');

        const handleSubmit = async (e) => {
            e.preventDefault();
            try {
                const response = await axios.post('http://localhost:3000/login', { username, password });
                localStorage.setItem('token', response.data.token);
                alert('User logged in successfully');
            } catch (error) {
                alert('Error logging in');
            }
        };

        return (
            <form onSubmit={handleSubmit}>
                <h2>Login</h2>
                <input
                    type="text"
                    placeholder="Username"
                    value={username}
                    onChange={(e) => setUsername(e.target.value)}
                />
                <input
                    type="password"
                    placeholder="Password"
                    value={password}
                    onChange={(e) => setPassword(e.target.value)}
                />
                <button type="submit">Login</button>
            </form>
        );
    };

    export default Login;
    ```

### **<span style="color: LightPink;">Step 3: Creating a Protected Component</span>**
- **<span style="color: LightPink;">Description:</span>** Create a component that fetches data from a protected route.

    ```jsx
    // src/components/Protected.js
    import React, { useEffect, useState } from 'react';
    import axios from 'axios';

    const Protected = () => {
        const [message, setMessage] = useState('');

        useEffect(() => {
            const fetchData = async () => {
                try {
                    const token = localStorage.getItem('token');
                    const response = await axios.get('http://localhost:3000/protected', {
                        headers: {
                            'Authorization': `Bearer ${token}`
                        }
                    });
                    setMessage(response.data);
                } catch (error) {
                    setMessage('Error accessing protected route');
                }
            };

            fetchData();
        }, []);

        return <h2>{message}</h2>;
    };

    export default Protected;
    ```

### **<span style="color: LightPink;">Step 4: Creating a Higher-Order Component for Protected Routes</span>**
- **<span style="color: LightPink;">Description:</span>** Create a higher-order component to wrap protected components and check if the user is authenticated.

    ```jsx
    // src/components/ProtectedRoute.js
    import React from 'react';
    import { Route, Redirect } from 'react-router-dom';

    const ProtectedRoute = ({ component: Component, ...rest }) => {
        return (
            <Route
                {...rest}
                render={props => {
                    const token = localStorage.getItem('token');
                    if (token) {
                        return <Component {...props} />;
                    } else {
                        return <Redirect to="/login" />;
                    }
                }}
            />
        );
    };

    export default ProtectedRoute;
    ```

### **<span style="color: LightPink;">Step 5: Setting Up Routing</span>**
- **<span style="color: LightPink;">Description:</span>** Set up routing to navigate between registration, login, and protected components.

    ```jsx
    // src/App.js
    import React from 'react';
    import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
    import Register from './components/Register';
    import Login from './components/Login';
    import Protected from './components/Protected';
    import ProtectedRoute from './components/ProtectedRoute';

    const App = () => {
        return (
            <Router>
                <Switch>
                    <Route path="/register" component={Register} />
                    <Route path="/login" component={Login} />
                    <ProtectedRoute path="/protected" component={Protected} />
                </Switch>
            </Router>
        );
    };

    export default App;
    ```

### **<span style="color: LightPink;">Step 6: Summary</span>**
- **<span style="color: LightPink;">Description:</span>** To set up a React frontend for user authentication using JWT tokens, follow these steps:
    1. **Set up your React project**: Initialize a React project and install Axios for making HTTP requests.
    2. **Create registration and login forms**: Implement components for user registration and login.
    3. **Create a protected component**: Implement a component that accesses a protected route using the JWT token.
    4. **Create a higher-order component for protected routes**: Implement a higher-order component to check if the user is authenticated.
    5. **Set up routing**: Configure routing to navigate between the registration, login, and protected components.

This process ensures that your React frontend can handle user authentication, registration, login, and access to protected routes using JWT tokens.
