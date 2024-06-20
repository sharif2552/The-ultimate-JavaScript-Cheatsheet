# **<span style="color: orange;">How Google Authentication Works</span>**

## **<font color="skyblue">Backend Setup</font>**

### **<span style="color: LightPink;">Overview</span>**
- **<span style="color: LightPink;">Description:</span>** This guide explains how to integrate Google OAuth authentication into a Node.js backend using Passport.js. Users will be able to log in to your application using their Google accounts.

### **<span style="color: LightPink;">Step 1: Setting Up Your Project</span>**
- **<span style="color: LightPink;">Description:</span>** Initialize your Node.js project and install necessary dependencies.

    ```sh
    # Initialize a new Node.js project
    npm init -y

    # Install required packages: Express, Passport, Passport-Google-OAuth, and dotenv
    npm install express passport passport-google-oauth20 dotenv
    ```

### **<span style="color: LightPink;">Step 2: Configuring Google OAuth Credentials</span>**
- **<span style="color: LightPink;">Description:</span>** Obtain Google OAuth credentials from the Google Developer Console.

    ```dotenv
    # .env file
    GOOGLE_CLIENT_ID=your_google_client_id
    GOOGLE_CLIENT_SECRET=your_google_client_secret
    ```

### **<span style="color: LightPink;">Step 3: Setting Up Passport.js</span>**
- **<span style="color: LightPink;">Description:</span>** Configure Passport.js with the Google OAuth strategy.

    ```js
    // Import necessary modules
    const passport = require('passport');
    const GoogleStrategy = require('passport-google-oauth20').Strategy;
    const User = require('../models/User'); // Adjust path as needed
    const dotenv = require('dotenv');
    dotenv.config();

    // Configure Passport with Google OAuth
    passport.use(new GoogleStrategy({
        clientID: process.env.GOOGLE_CLIENT_ID,
        clientSecret: process.env.GOOGLE_CLIENT_SECRET,
        callbackURL: '/api/auth/google/callback' // Adjust callback URL as per your setup
      },
      async (accessToken, refreshToken, profile, done) => {
        try {
          // Check if user already exists in database
          let user = await User.findOne({ googleId: profile.id });

          if (!user) {
            // Create new user if not found
            user = new User({
              googleId: profile.id,
              displayName: profile.displayName,
              email: profile.emails[0].value // Assuming email is required
            });
            await user.save();
          }

          return done(null, user); // Pass the user data to Passport
        } catch (err) {
          return done(err, null); // Handle errors
        }
      }
    ));

    // Serialize and deserialize user for session management
    passport.serializeUser((user, done) => {
      done(null, user.id);
    });

    passport.deserializeUser((id, done) => {
      User.findById(id, (err, user) => {
        done(err, user);
      });
    });
    ```

### **<span style="color: LightPink;">Step 4: Setting Up Express Server</span>**
- **<span style="color: LightPink;">Description:</span>** Initialize an Express server to handle Google OAuth authentication.

    ```js
    // Import necessary modules
    const express = require('express');
    const passport = require('passport');
    const session = require('express-session');
    const dotenv = require('dotenv');
    const connectDB = require('../config/db'); // Adjust path as needed

    // Load environment variables from .env file
    dotenv.config();

    // Connect to MongoDB database
    connectDB();

    // Initialize Express app
    const app = express();

    // Middleware to parse JSON bodies
    app.use(express.json());

    // Middleware for session management
    app.use(session({
      secret: process.env.SESSION_SECRET,
      resave: false,
      saveUninitialized: false
    }));

    // Initialize Passport middleware
    app.use(passport.initialize());
    app.use(passport.session());

    // Configure routes for Google OAuth
    app.get('/api/auth/google', passport.authenticate('google', {
      scope: ['profile', 'email'] // Adjust scope as needed
    }));

    app.get('/api/auth/google/callback',
      passport.authenticate('google', { failureRedirect: '/' }),
      (req, res) => {
        res.redirect('http://localhost:3000/'); // Redirect URL after successful login
      }
    );

    // Define port on which the server will listen
    const PORT = process.env.PORT || 5000;

    // Start the server
    app.listen(PORT, () => {
      console.log(`Server is running on port ${PORT}`);
    });
    ```

### **<span style="color: LightPink;">Step 5: Summary</span>**
- **<span style="color: LightPink;">Description:</span>** Integrating Google OAuth authentication involves:
    1. **Setting up your project**: Initialize a Node.js project and install necessary packages.
    2. **Configuring Google OAuth credentials**: Obtain credentials from Google Developer Console and store them in a `.env` file.
    3. **Setting up Passport.js**: Configure Passport.js with the Google OAuth strategy, serialize, and deserialize user data.
    4. **Setting up Express server**: Initialize an Express server, configure session middleware, and define routes for Google OAuth authentication.

This setup enables users to log in to your application securely using their Google accounts.

## **<font color="skyblue">Frontend Integration with React</font>**

### **<span style="color: LightPink;">Overview</span>**
- **<span style="color: LightPink;">Description:</span>** This guide explains how to integrate Google OAuth authentication into a React frontend using `react-google-login` library.

### **<span style="color: LightPink;">Step 1: Setting Up Your React Project</span>**
- **<span style="color: LightPink;">Description:</span>** Initialize your React project and install necessary dependencies.

    ```sh
    npx create-react-app google-auth-react
    cd google-auth-react
    npm install react-google-login
    ```

### **<span style="color: LightPink;">Step 2: Creating the Google Login Component</span>**
- **<span style="color: LightPink;">Description:</span>** Implement a React component to handle Google OAuth login.

    ```jsx
    // Import necessary modules
    import React from 'react';
    import { GoogleLogin } from 'react-google-login';

    // Define Google Login component
    const GoogleLoginComponent = () => {
      const responseGoogle = (response) => {
        console.log(response); // Handle Google OAuth response
      };

      return (
        <div>
          <GoogleLogin
            clientId="your_google_client_id"
            buttonText="Login with Google"
            onSuccess={responseGoogle}
            onFailure={responseGoogle}
            cookiePolicy={'single_host_origin'}
          />
        </div>
      );
    };

    export default GoogleLoginComponent;
    ```

### **<span style="color: LightPink;">Step 3: Integrating Google Login Component</span>**
- **<span style="color: LightPink;">Description:</span>** Use the Google Login component in your application.

    ```jsx
    // Import necessary modules
    import React from 'react';
    import GoogleLoginComponent from './GoogleLoginComponent'; // Adjust path as needed

    // App component
    const App = () => {
      return (
        <div>
          <h1>Google OAuth Authentication</h1>
          <GoogleLoginComponent />
        </div>
      );
    };

    export default App;
    ```

### **<span style="color: LightPink;">Step 4: Summary</span>**
- **<span style="color: LightPink;">Description:</span>** Integrating Google OAuth authentication into a React frontend involves:
    1. **Setting up your React project**: Initialize a React project and install necessary dependencies.
    2. **Creating the Google Login component**: Implement a component using `react-google-login` library to handle Google OAuth login.
    3. **Integrating the component**: Use the Google Login component in your React application to enable users to log in with their Google accounts.

This setup allows users to authenticate securely using Google OAuth in your React application.
