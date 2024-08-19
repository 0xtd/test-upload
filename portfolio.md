## MERN Stack Portfolio Website

This project outlines the creation of a portfolio website using the MERN stack (MongoDB, Express.js, React.js, and Node.js) with Tailwind CSS for styling and Vite for fast development.

**Project Structure:**

```
portfolio-website/
├── client/
│   ├── src/
│   │   ├── components/
│   │   │   ├── Navbar.jsx
│   │   │   ├── Home.jsx
│   │   │   ├── Services.jsx
│   │   │   ├── About.jsx
│   │   │   ├── Contact.jsx
│   │   │   ├── Footer.jsx
│   │   ├── App.jsx
│   │   ├── main.jsx
│   │   ├── index.css
│   ├── index.html
│   ├── vite.config.js
│   ├── package.json
├── server/
│   ├── models/
│   │   ├── message.js // For contact form submissions
│   ├── routes/
│   │   ├── contactRoutes.js
│   ├── server.js
│   ├── package.json
```

**1. Frontend (client folder):**

**a) Setting up the React project using Vite:**

```bash
cd client
npm create vite@latest
```

Choose `React` as the framework and `JavaScript` as the variant.

**b) Install dependencies:**

```bash
npm install tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

**c) Configure Tailwind CSS:**

In `tailwind.config.js`:

```javascript
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {
      colors: {
        'primary-blue': '#2563eb', // Example blue color
        'dark-blue': '#1e40af',
        'black': '#000',
      },
    },
  },
  plugins: [],
}
```

Add the Tailwind directives to your `index.css` file:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

**d) Components:**

Create the following components in `src/components`:

- **Navbar.jsx:**

```javascript
import React from 'react';

function Navbar() {
  return (
    <nav className="bg-dark-blue p-4">
      <div className="container mx-auto flex justify-between items-center">
        <a href="/" className="text-white text-xl font-bold">Your Name</a>
        <ul className="flex space-x-4">
          <li><a href="/" className="text-white hover:text-primary-blue">Home</a></li>
          <li><a href="/services" className="text-white hover:text-primary-blue">Services</a></li>
          <li><a href="/about" className="text-white hover:text-primary-blue">About</a></li>
          <li><a href="/contact" className="text-white hover:text-primary-blue">Contact</a></li>
        </ul>
      </div>
    </nav>
  );
}

export default Navbar;
```

- **Home.jsx:**

```javascript
import React from 'react';

function Home() {
  return (
    <div className="bg-black text-white min-h-screen flex items-center justify-center">
      <div className="text-center">
        <h1 className="text-4xl font-bold mb-4">Welcome to my Portfolio!</h1>
        <p className="text-lg">I'm a MERN Stack Developer passionate about building web applications.</p>
      </div>
    </div>
  );
}

export default Home;
```

- **Services.jsx:**

```javascript
import React from 'react';

function Services() {
  return (
    <div className="bg-gray-900 text-white py-12">
      <div className="container mx-auto">
        <h2 className="text-3xl font-bold text-center mb-8">My Services</h2>
        <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
          {/* Add your service cards here */}
          <div className="bg-dark-blue p-6 rounded-lg">
            <h3 className="text-xl font-bold mb-2">Web Development</h3>
            <p>Building responsive and performant web applications using the MERN stack.</p>
          </div>
          {/* ... more service cards */}
        </div>
      </div>
    </div>
  );
}

export default Services;
```

- **About.jsx:**

```javascript
import React from 'react';

function About() {
  return (
    <div className="bg-black text-white py-12">
      <div className="container mx-auto">
        <h2 className="text-3xl font-bold text-center mb-8">About Me</h2>
        <p className="text-lg">Write something about yourself, your skills, and experience.</p>
      </div>
    </div>
  );
}

export default About;
```

- **Contact.jsx:**

```javascript
import React, { useState } from 'react';

function Contact() {
  const [name, setName] = useState('');
  const [email, setEmail] = useState('');
  const [message, setMessage] = useState('');

  const handleSubmit = async (e) => {
    e.preventDefault();

    // Send data to the backend (replace with your actual API endpoint)
    try {
      const response = await fetch('/api/contact', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({ name, email, message }),
      });

      if (response.ok) {
        // Handle successful submission
        console.log('Message sent successfully!');
        setName('');
        setEmail('');
        setMessage('');
      } else {
        // Handle errors
        console.error('Error sending message.');
      }
    } catch (error) {
      console.error('Error sending message:', error);
    }
  };

  return (
    <div className="bg-gray-900 text-white py-12">
      <div className="container mx-auto">
        <h2 className="text-3xl font-bold text-center mb-8">Contact Me</h2>
        <form onSubmit={handleSubmit} className="max-w-md mx-auto">
          <div className="mb-4">
            <label htmlFor="name" className="block text-sm font-bold mb-2">Name:</label>
            <input type="text" id="name" value={name} onChange={(e) => setName(e.target.value)} className="w-full px-3 py-2 border rounded-md" required />
          </div>
          <div className="mb-4">
            <label htmlFor="email" className="block text-sm font-bold mb-2">Email:</label>
            <input type="email" id="email" value={email} onChange={(e) => setEmail(e.target.value)} className="w-full px-3 py-2 border rounded-md" required />
          </div>
          <div className="mb-4">
            <label htmlFor="message" className="block text-sm font-bold mb-2">Message:</label>
            <textarea id="message" value={message} onChange={(e) => setMessage(e.target.value)} className="w-full px-3 py-2 border rounded-md" required></textarea>
          </div>
          <button type="submit" className="bg-primary-blue text-white px-4 py-2 rounded-md hover:bg-dark-blue">Send Message</button>
        </form>
      </div>
    </div>
  );
}

export default Contact;
```

- **Footer.jsx:**

```javascript
import React from 'react';

function Footer() {
  return (
    <footer className="bg-dark-blue p-4 text-center text-white">
      <p>&copy; {new Date().getFullYear()} Your Name. All rights reserved.</p>
    </footer>
  );
}

export default Footer;
```

**e) App.jsx:**

```javascript
import React from 'react';
import { BrowserRouter, Routes, Route } from 'react-router-dom';
import Navbar from './components/Navbar';
import Home from './components/Home';
import Services from './components/Services';
import About from './components/About';
import Contact from './components/Contact';
import Footer from './components/Footer';

function App() {
  return (
    <BrowserRouter>
      <Navbar />
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/services" element={<Services />} />
        <Route path="/about" element={<About />} />
        <Route path="/contact" element={<Contact />} />
      </Routes>
      <Footer />
    </BrowserRouter>
  );
}

export default App;
```

**2. Backend (server folder):**

**a) Setting up the Node.js project:**

```bash
cd server
npm init -y
```

**b) Install dependencies:**

```bash
npm install express mongoose cors body-parser nodemon
```

**c) Create server.js:**

```javascript
const express = require('express');
const mongoose = require('mongoose');
const cors = require('cors');
const bodyParser = require('body-parser');

const app = express();
const PORT = process.env.PORT || 5000;

// Middleware
app.use(cors());
app.use(bodyParser.json());

// Connect to MongoDB (replace with your MongoDB connection string)
mongoose.connect('mongodb://localhost:27017/portfolio', {
  useNewUrlParser: true,
  useUnifiedTopology: true,
});

const db = mongoose.connection;
db.on('error', console.error.bind(console, 'MongoDB connection error:'));

// Define routes (e.g., for contact form submission)
const contactRoutes = require('./routes/contactRoutes');
app.use('/api/contact', contactRoutes);

app.listen(PORT, () => {
  console.log(`Server listening on port ${PORT}`);
});
```

**d) Create models/message.js:**

```javascript
const mongoose = require('mongoose');

const messageSchema = new mongoose.Schema({
  name: String,
  email: String,
  message: String,
});

module.exports = mongoose.model('Message', messageSchema);
```

**e) Create routes/contactRoutes.js:**

```javascript
const express = require('express');
const router = express.Router();
const Message = require('../models/message');

router.post('/', async (req, res) => {
  try {
    const newMessage = new Message(req.body);
    await newMessage.save();
    res.status(201).json({ message: 'Message sent successfully!' });
  } catch (error) {
    console.error('Error saving message:', error);
    res.status(500).json({ error: 'Error sending message.' });
  }
});

module.exports = router;
```

**3. Running the application:**

- Start the backend server:

```bash
cd server
nodemon server.js
```

- Start the frontend development server:

```bash
cd client
npm run dev
```

This detailed guide helps you build a MERN stack portfolio website with eye-catching graphics using Tailwind CSS. Remember to replace placeholder values like database connection strings and personalize content to reflect your skills and experience. You can further customize the styling and add features as needed. Good luck!
