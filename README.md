
# Bookstore E-commerce App

This is a full-stack Bookstore E-commerce application built using the MERN (MongoDB, Express.js, React, Node.js) stack. The project demonstrates a comprehensive understanding of full-stack development by showcasing how to set up a web application where users can view, filter, and purchase various books.

## Table of Contents

- [Preview](#preview)
- [Prerequisites](#prerequisites)
- [Approach](#approach)
- [Backend Setup](#backend-setup)
- [Frontend Setup](#frontend-setup)
- [Running the Application](#running-the-application)
- [Deployment](#deployment)
- [License](#license)

## Preview

Here is a screenshot of the final output of the application:

![Final Project Output](https://github.com/shyamjee1645/bookstore/assets/93826494/35f32f4e-fb64-4fe5-b762-5c60ec8ff26f)

## Prerequisites

- React JS and Context API
- MongoDB and Mongoose
- Express.js
- Node.js
- MERN Stack knowledge

## Approach

1. List all the requirements for the project and structure the project accordingly.
2. Choose the required dependencies and configurations suitable for the project.
3. Create custom components like `ProductList` and `Header` in the `./components` directory.
4. Use a custom context provider, `CustomItemContext`, to manage state.

## Backend Setup

### Step 1: Create a Directory for the Project

```bash
mkdir server
cd server
```

### Step 2: Initialize the Express App and Install Required Packages

```bash
npm init -y
npm install express mongoose cors
```

### Project Structure

```
server/
│
├── server.js
├── package.json
└── ...
```

### server.js

```javascript
const express = require('express');
const mongoose = require('mongoose');
const cors = require('cors');
const app = express();
const PORT = process.env.PORT || 5000;

mongoose.connect('<Your connection string>', { useNewUrlParser: true, useUnifiedTopology: true });

app.use(express.json());
app.use(cors());

const bookSchema = new mongoose.Schema({
    title: String,
    author: String,
    genre: String,
    description: String,
    price: Number,
    image: String,
});

const Book = mongoose.model('Book', bookSchema);

// Function to seed initial data into the database
const seedDatabase = async () => {
    try {
        await Book.deleteMany(); // Clear existing data

        const books = [
            { title: 'The Great Gatsby', author: 'F. Scott Fitzgerald', genre: 'Fiction', description: 'A classic novel about the American Dream', price: 20, image: 'https://media.geeksforgeeks.org/wp-content/uploads/20240110011815/sutterlin-1362879_640-(1).jpg' },
            { title: 'To Kill a Mockingbird', author: 'Harper Lee', genre: 'Fiction', description: 'A powerful story of racial injustice and moral growth', price: 15, image: 'https://media.geeksforgeeks.org/wp-content/uploads/20240110011854/reading-925589_640.jpg' },
            { title: '1984', author: 'George Orwell', genre: 'Dystopian', description: 'A dystopian vision of a totalitarian future society', price: 25, image: 'https://media.geeksforgeeks.org/wp-content/uploads/20240110011929/glasses-1052010_640.jpg' },
        ];

        await Book.insertMany(books);
        console.log('Database seeded successfully');
    } catch (error) {
        console.error('Error seeding database:', error);
    }
};

// Seed the database on server startup
seedDatabase();

// Define API endpoint for fetching all books
app.get('/api/books', async (req, res) => {
    try {
        const allBooks = await Book.find();
        res.json(allBooks);
    } catch (error) {
        console.error(error);
        res.status(500).json({ error: 'Internal Server Error' });
    }
});

app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});
```

### Start the Backend Server

```bash
node server.js
```

## Frontend Setup

### Step 1: Set Up React Frontend

```bash
npx create-react-app client
cd client
```

### Step 2: Install Required Dependencies

```bash
npm install @fortawesome/free-solid-svg-icons @fortawesome/react-fontawesome
```

### Project Structure

```
client/
│
├── src/
│   ├── components/
│   │   ├── Header.js
│   │   └── ProductList.js
│   ├── context/
│   │   └── ItemContext.js
│   ├── App.js
│   ├── App.css
│   └── ...
├── public/
├── package.json
└── ...
```

### App.js

```javascript
import React from 'react';
import ProductList from './components/ProductList';
import Header from './components/Header';
import './App.css';
import CustomItemContext from './context/ItemContext';

const App = () => {
    return (
        <CustomItemContext>
            <Header />
            <ProductList />
        </CustomItemContext>
    );
};

export default App;
```

### Start the Frontend

```bash
npm start
```

## Deployment
### Project Link
The project is deployed and can be accessed at: https://bookstore-deploy-e2cc0qkhb-shyamjee1645s-projects.vercel.app/

### Options for Free Deployment

1. **GitHub Pages**
2. **Netlify**
3. **Vercel**
4. **Firebase Hosting**

Follow the respective documentation for deploying React applications on these platforms.

```

This `README.md` file provides a comprehensive overview of the project, setup instructions, and deployment options. Make sure to replace placeholders like `<Your connection string>` with actual values relevant to your project.
