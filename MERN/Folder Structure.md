# **<span style="color: orange;">Top-Level Files and Folders</span>**

- ## **<span style="color: skyblue;">backend</span>**
  - **<span style="color: LightPink;">Description:</span>** The main folder for your backend code. Contains everything related to your server-side logic.

    ```
    backend/ 
    ├── config/ 
    ├── controllers/ 
    ├── middleware/ 
    ├── models/ 
    ├── routes/ 
    ├── utils/ 
    └── server.js
    ```


- ## **<span style="color: skyblue;">node_modules</span>**
  - **<span style="color: LightPink;">Description:</span>** Stores all the dependencies (libraries and packages) required by your project. Managed by `npm`, so you don't need to worry about this folder.

- ## **<span style="color: skyblue;">.env</span>**
  - **<span style="color: LightPink;">Description:</span>** Holds environment variables such as database connection strings, API keys, and other configuration settings.
  - **<span style="color: LightPink;">Purpose:</span>** Keeps sensitive information outside of the code for enhanced security and flexibility.
    ```json
	DB_CONNECTION_STRING=mongodb://localhost:27017/myapp
	JWT_SECRET=myverysecuresecret
    ```

- ## **<span style="color: skyblue;">package.json</span>**
  - **<span style="color: LightPink;">Description:</span>** Contains metadata about your project and lists all the dependencies.
  - **<span style="color: LightPink;">Purpose:</span>** Includes scripts to run tasks like starting the server.

    ```json
    {
      "name": "myapp",
      "version": "1.0.0",
      "scripts": {
        "start": "node server.js",
        "dev": "nodemon server.js"
      },
      "dependencies": {
        "express": "^4.17.1",
        "mongoose": "^5.11.15"
      }
    }
    ```

- ## **<span style="color: skyblue;">package-lock.json</span>**
  - **<span style="color: LightPink;">Description:</span>** Locks the versions of your dependencies.
  - **<span style="color: LightPink;">Purpose:</span>** Ensures consistent dependency versions are used when the project is reinstalled.

- ## **<span style="color: skyblue;">server.js</span>**
  - **<span style="color: LightPink;">Description:</span>** The entry point of your backend application.
  - **<span style="color: LightPink;">Purpose:</span>** Sets up the server, connects to the database, and starts listening for requests.
    ```js
		const express = require('express');
		const connectDB = require('./config/db'); // Import function to connect to MongoDB
		const authRoutes = require('./routes/authRoutes'); // Import authentication routes
		const protectedRoutes = require('./routes/protectedRoutes'); // Import protected routes
		const errorHandler = require('./middleware/errorHandler'); // Import error handling middleware
		
		const app = express();
		
		// Connect to MongoDB
		connectDB();
		
		// Middleware to parse JSON bodies
		app.use(express.json());
		
		// Routes
		app.use('/api/auth', authRoutes); // Authentication routes
		app.use('/api/protected', protectedRoutes); // Protected routes
		
		// Error handling middleware (must be registered after routes)
		app.use(errorHandler);
		
		// Start the server
		const PORT = process.env.PORT || 5000;
		app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
    ```






# **<span style="color: orange;">Inside the backend/ Folder</span>**

- ## **<span style="color: skyblue;">config/db.js</span>**
  - **<span style="color: LightPink;">Description:</span>** Contains the configuration for connecting to your MongoDB database.
  - **<span style="color: LightPink;">Purpose:</span>** Typically exports a function to establish the connection.

    ```js
		// Import the mongoose library
		const mongoose = require('mongoose');
		
		// Define the connection function
		const connectDB = async () => {
		  try {
			// Connect to the MongoDB database
			// Replace '<your_mongodb_uri>' with your actual MongoDB connection string
			await mongoose.connect('<your_mongodb_uri>', {
			  useNewUrlParser: true,   // Use the new MongoDB connection string parser
			  useUnifiedTopology: true // Use the new server discovery and monitoring engine
			});
		
			// If connection is successful, log this message
			console.log('MongoDB connected successfully!');
		  } catch (error) {
			// If there is an error connecting to the database, log the error
			console.error('Error connecting to MongoDB:', error.message);
			process.exit(1); // Exit the process with a failure code
		  }
		};
		
		// Export the connection function so it can be used in other files
		module.exports = connectDB;

    ```
- ## **<span style="color: skyblue;">controllers/authController.js</span>**
  - **<span style="color: LightPink;">Description:</span>** Handles the business logic for different routes.
  - **<span style="color: LightPink;">Purpose:</span>** Specifically manages authentication-related logic such as logging in and signing up.
    ```js
		// Import the User model
		const User = require('../models/User');
		
		// Import bcrypt for password hashing
		const bcrypt = require('bcryptjs');
		
		// Import jsonwebtoken for creating tokens
		const jwt = require('jsonwebtoken');
		
		// Secret key for JWT (in a real application, store this in an environment variable)
		const JWT_SECRET = 'your_jwt_secret_key';
		
		// Controller function for user registration
		const register = async (req, res) => {
		  // Get user details from request body
		  const { username, email, password } = req.body;
		
		  // Check if user already exists
		  let user = await User.findOne({ email });
		  if (user) {
		    return res.status(400).send('User already exists');
		  }
		
		  // Create a new user
		  user = new User({ username, email, password });
		
		  // Hash the password before saving the user
		  const salt = await bcrypt.genSalt(10);
		  user.password = await bcrypt.hash(password, salt);
		
		  // Save the user to the database
		  await user.save();
		
		  // Create and return a token
		  const token = jwt.sign({ id: user.id }, JWT_SECRET, { expiresIn: '1h' });
		  res.status(201).send({ token });
		};
		
		// Controller function for user login
		const login = async (req, res) => {
		  // Get login details from request body
		  const { email, password } = req.body;
		
		  // Check if the user exists
		  const user = await User.findOne({ email });
		  if (!user) {
		    return res.status(400).send('Invalid credentials');
		  }
		
		  // Check if password is correct
		  const isMatch = await bcrypt.compare(password, user.password);
		  if (!isMatch) {
		    return res.status(400).send('Invalid credentials');
		  }
		
		  // Create and return a token
		  const token = jwt.sign({ id: user.id }, JWT_SECRET, { expiresIn: '1h' });
		  res.send({ token });
		};
		
		// Export the functions
		module.exports = { register, login };

    ```
- ## **<span style="color: skyblue;">middleware/authMiddleware.js</span>**
  - **<span style="color: LightPink;">Description:</span>** Processes requests before they reach the controller.
  - **<span style="color: LightPink;">Purpose:</span>** Likely contains functions to check if a user is authenticated before accessing certain routes.

    ```js
		const jwt = require('jsonwebtoken');
		const config = require('../config/default'); // Assuming you have a config file for JWT secret and other configurations
		
		// Middleware function to authenticate JWT token
		const authMiddleware = (req, res, next) => {
		  // Get token from header
		  const token = req.header('x-auth-token');
		
		  // Check if token does not exist
		  if (!token) {
		    return res.status(401).json({ msg: 'No token, authorization denied' });
		  }
		
		  try {
		    // Verify token
		    const decoded = jwt.verify(token, config.JWT_SECRET);
		
		    // Add user from payload
		    req.user = decoded;
		    next();
		  } catch (e) {
		    res.status(400).json({ msg: 'Token is not valid' });
		  }
		};
		
		module.exports = authMiddleware;

    ```
- ## **<span style="color: skyblue;">models/User.js</span>**
  - **<span style="color: LightPink;">Description:</span>** Defines the schema for your database collections.
  - **<span style="color: LightPink;">Purpose:</span>** Specifies the structure of user documents in your MongoDB database.

    ```js
		const mongoose = require('mongoose');
		
		// Define the User schema
		const UserSchema = new mongoose.Schema({
		  username: {
		    type: String,
		    required: true
		  },
		  email: {
		    type: String,
		    required: true,
		    unique: true
		  },
		  password: {
		    type: String,
		    required: true
		  },
		  date: {
		    type: Date,
		    default: Date.now
		  }
		});
		
		// Create and export the User model
		module.exports = mongoose.model('User', UserSchema);
    ```
- ## **<span style="color: skyblue;">routes/authRoutes.js</span>**
  - **<span style="color: LightPink;">Description:</span>** Defines the routes related to authentication (e.g., login, signup).
  - **<span style="color: LightPink;">Purpose:</span>** Maps HTTP requests to the appropriate controller functions.
    ```js
		const express = require('express');
		const router = express.Router();
		const { register, login } = require('../controllers/authController');
		
		// Route: POST /api/auth/register
		// Description: Register a new user
		router.post('/register', register);
		
		// Route: POST /api/auth/login
		// Description: Login user
		router.post('/login', login);
		
		module.exports = router;
		
	
    ```
- ## **<span style="color: skyblue;">utils/</span>**
  - **<span style="color: LightPink;">Description:</span>** Used for utility functions or helpers that can be reused across your application.
  - **<span style="color: LightPink;">Purpose:</span>** Provides common functionality that doesn't fit into controllers, models, or middleware.


    ```js
		// Function to generate a random alphanumeric string of given length
		const generateRandomString = (length) => {
		  let result = '';
		  const characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
		  const charactersLength = characters.length;
		  for (let i = 0; i < length; i++) {
		    result += characters.charAt(Math.floor(Math.random() * charactersLength));
		  }
		  return result;
		};
		
		module.exports = generateRandomString;
    ```




# **<span style="color: orange;">Summary for Easy Remembering</span>**

- **<span style="color: yellow;">config/</span>**: Database connection setup.
- **<span style="color: yellow;">controllers/</span>**: Handles business logic.
- **<span style="color: yellow;">middleware/</span>**: Processes requests (e.g., authentication checks) before reaching controllers.
- **<span style="color: yellow;">models/</span>**: Defines the structure of your database entries.
- **<span style="color: yellow;">routes/</span>**: Maps URLs to controller functions.
- **<span style="color: yellow;">utils/</span>**: Reusable helper functions.
- **<span style="color: yellow;">.env</span>**:Configuration settings and sensitive information.
- **<span style="color: yellow;">package.json</span>**:Project metadata and dependency management.
- **<span style="color: yellow;">package-lock.json</span>**: Ensures consistent dependency versions.
- **<span style="color: yellow;">server.js</span>**:Starts the server and connects to the database.

![[MERN Stack/Back end/Pasted image 20240613210845.png]]
