Smart Printing Station
Welcome to the Smart Printing Station, a modern web application that integrates a Telegram bot with a print preview interface. This system allows users to send documents to a Telegram bot, receive a unique PIN, and use that PIN on a web app to preview their file, configure print options, and generate a payment QR code.

This document provides a comprehensive guide to understanding, installing, and running the project.

Table of Contents
How It Works

Features

Technology Stack

System Requirements

Project Setup and Installation

Dependencies Explained

Backend Dependencies

Frontend Dependencies

Development Dependencies

Troubleshooting

How It Works
The user workflow is designed to be simple and secure:

File Submission: A user sends a document (e.g., PDF, JPG, PNG) to a dedicated Telegram bot.

PIN Generation: The backend server receives the file, saves it locally, and generates a unique 4-digit PIN.

Receive PIN: The Telegram bot sends this PIN back to the user.

Web Preview: The user navigates to the Smart Printing Station web application and enters the PIN.

File Retrieval: The web app sends the PIN to the backend, which verifies it and serves the corresponding file for preview.

Configuration & Payment: The user can then adjust print options (like color, paper size, etc.) and generate a UPI QR code to pay for the print job.

Features
Telegram Bot Integration: Easily submit files for printing through Telegram.

Secure PIN Access: Files are accessed via a unique, temporary PIN.

Real-time Print Preview: A web interface to preview documents before printing.

PDF and Image Support: Handles common document and image formats.

Dynamic Print Options: Customize color mode, duplex, paper size, quality, and page ranges.

Automatic Price Calculation: The total cost is calculated in real-time based on the selected options.

UPI QR Code Generation: Instantly generates a QR code for easy payment.

Technology Stack
This project is built with modern web technologies.

Backend:

Language: JavaScript (Node.js)

Framework: Express.js

Module System: CommonJS (.cjs)

Frontend:

Language: JavaScript (ESM) with JSX

Framework: React 19

Build Tool: Vite

Styling: Vanilla CSS with Flexbox and Grid

Communication:

Bot API: node-telegram-bot-api

Web Server Communication: RESTful API endpoints

System Requirements
Before you begin, ensure you have the following installed on your system:

Node.js: Version 18.x or higher.

npm (Node Package Manager): Usually comes with Node.js.

A Telegram Account: To create and manage the bot.

Project Setup and Installation
Follow these steps to get the project running on your local machine.

Step 1: Get a Telegram Bot Token
Open Telegram and search for the @BotFather user.

Start a chat and send the /newbot command.

Follow the instructions to name your bot and choose a username.

BotFather will provide you with a unique API Token. Copy this token and keep it safe.

Step 2: Install Project Dependencies
Clone or download the project repository to your local machine.

Open a terminal in the project's root directory (printproj-main).

Install all the required frontend and backend packages by running:

Bash

npm install
Step 3: Configure the Backend
Navigate to the backend folder and open the index.cjs file (backend/index.cjs).

Find the following line and replace the placeholder with the Telegram Bot Token you copied earlier:

JavaScript

const TOKEN = "YOUR_REAL_BOT_TOKEN_HERE";
Important: Ensure the backend file is named index.cjs so that Node.js treats it as a CommonJS module.

Step 4: Run the Application
From the root directory of the project, run the following command:

Bash

npm start
This command uses concurrently to start both the backend server and the frontend Vite development server at the same time. You will see output from both servers in your terminal.

The backend will be running on http://localhost:3000.

The frontend will be running on a port like http://localhost:5173. Open this URL in your browser to use the application.

Dependencies Explained
This project uses several libraries to function. Here is a detailed breakdown of each one.

Backend Dependencies
These packages are essential for running the backend server and are listed in package.json.

express: A fast and minimalist web framework for Node.js. It is used to create the API endpoints that the frontend communicates with, such as /file/:pin.

node-telegram-bot-api: A library that allows Node.js to interact with the Telegram Bot API. It handles receiving messages and files from users and sending replies.

cors: A Node.js package that enables Cross-Origin Resource Sharing. It is necessary because our frontend (on port 5173) needs to make requests to our backend (on port 3000).

node-fetch: A module that brings the fetch API to Node.js. It is used in the backend to download the files from Telegram's servers.

Frontend Dependencies
These are the libraries used to build the user interface and are listed in package.json.

react: A JavaScript library for building user interfaces. It is the core of the frontend application.

react-dom: Provides the methods to render React components into the DOM (the webpage).

pdfjs-dist: A library by Mozilla for parsing and rendering PDF files in the browser. It is used to create the print preview for PDF documents.

qrcode: A library to generate QR codes. It is used to create the UPI payment QR code from a text string.

axios: A promise-based HTTP client for making requests from the browser to the backend. (Note: The current implementation uses the browser's built-in fetch, but axios is available).

Development Dependencies
These packages are used during the development process (e.g., for bundling, linting, and running the dev server) and are listed in package.json.

vite: A modern build tool that provides a fast development experience for web projects. It serves the React application during development and bundles it for production.

@vitejs/plugin-react: The official Vite plugin for React, enabling features like Fast Refresh.

eslint: A tool for identifying and reporting on patterns in JavaScript code, helping to maintain code quality and consistency.

eslint-plugin-react-hooks & eslint-plugin-react-refresh: ESLint plugins specifically for validating React code, ensuring hooks are used correctly and refresh works as expected.

concurrently: A utility to run multiple commands simultaneously. It is used in the npm start script to run both the frontend and backend servers with one command.

Troubleshooting
Error: require is not defined

This means your backend script is being treated as an ES Module. Ensure the file is renamed to index.cjs and you are starting it with node backend/index.cjs.

Error: 401 Unauthorized in the backend terminal

Your Telegram Bot Token is incorrect or has been revoked. Generate a new one from BotFather and update it in backend/index.cjs.

Frontend Error: "Failed to fetch" or Network Error

Ensure your backend server is running correctly on http://localhost:3000.

Check that the cors package is installed and used in your backend server file
