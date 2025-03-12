# Project Title
CityExplorer / WanderMap 

## Overview
Full Stack City Guide Application
CityExplorer would be an interactive platform allowing users to discover and explore cities through local recommendations, personalized itineraries, and authentic experiences.

### Problem Space
Information Overload
Travelers are overwhelmed by generic tourist information and countless reviews across multiple platforms. They struggle to filter through endless options to find authentic experiences that match their interests.

Inefficient Planning Process
Creating itineraries is time-consuming, involving multiple websites, spreadsheets, and manual mapping to organize a cohesive travel plan.

Unreliable Information
Operating hours, pricing, and availability information is often outdated on existing platforms, leading to frustrating travel experiences.

### User Profile

Who will use your app? How will they use it? Add any special considerations that your app must take into account.

Travelers & Tourists
Remote Workers & Digital Nomads
Curious Explorers & Students

### Features

List the functionality that your app will include. These can be written as user stories or descriptions with related details. Do not describe _how_ these features are implemented, only _what_ needs to be implemented.

- As a user, I want to be able to browse through cities from around the world and find out more about them.
- As a user, I want to be able to explore specific attractions within each city, whether they’re tourist landmarks, hidden gems, restaurants, museums, parks, etc.

## Implementation

### Tech Stack

-Html, css, scss, bootstrap
- React
- MySQL
- Express
- Client libraries: 
    - react
    - react-router
    - axios
- Server libraries:
    - knex
    - express
-Firebase:
    -for auth    

### APIs

- Maps
- creating one for cities and their popular places in sql for Itineraries.

### Sitemap

- Home page
- Itinerary page
- Map page
- City Details screen

# Once above completed (Diving deeper)
- User page
 - Register
 - Login


### Mockups

Provide visuals of your app's screens. You can use pictures of hand-drawn sketches, or wireframing tools like Figma.

### Data

-- Users Table (for authentication)
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(255) NOT NULL UNIQUE,
    email VARCHAR(255) NOT NULL UNIQUE,
    password_hash VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

-- Cities Table
CREATE TABLE cities (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    country VARCHAR(255) NOT NULL,
    description TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

-- Attractions Table
CREATE TABLE attractions (
    id INT AUTO_INCREMENT PRIMARY KEY,
    city_id INT NOT NULL,
    name VARCHAR(255) NOT NULL,
    category VARCHAR(255),
    description TEXT,
    address VARCHAR(255),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (city_id) REFERENCES cities(id) ON DELETE CASCADE
);

-- Itinerary Table
CREATE TABLE itinerary (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    attraction_id INT NOT NULL,
    visit_date DATE,
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE,
    FOREIGN KEY (attraction_id) REFERENCES attractions(id) ON DELETE CASCADE
);

### Endpoints
Cities Endpoints

1. **GET /api/cities**
   * Get all cities
   * Parameters: limit, page, search

2. **GET /api/cities/:id**
   * Get details for specific city

Attractions Endpoints

1. **GET /api/cities/:cityId/attractions**
   * Get attractions for specific city
   * Parameters: limit, page, category

2. **GET /api/attractions/:id**
   * Get details for specific attraction

Itinerary Endpoints

1. **GET /api/itinerary**
   * Get current user's saved attractions
   * Authentication: Required

2. **POST /api/itinerary**
   * Save attraction to user's itinerary
   * Authentication: Required
   * Request Body: attraction ID, visit date, notes

3. **DELETE /api/itinerary/:id**
   * Remove attraction from user's itinerary
   * Authentication: Required

# Once above completed (Diving deeper)
Users Endpoints

1. **GET /api/users/me**
   * Get current user profile based on Firebase Auth token
   * Authentication: Required

2. **POST /api/users**
   * Register new user in MySQL database after Firebase Auth
   * Authentication: Required
   * Request Body: Firebase UID and user information



## Roadmap
- Create client
    - react project with routes and boilerplate pages
    - basic SCSS styling setup with variables and mixins 
    - configure react-router with basic route structure 

Server (Backend)
- Set up Express server with initial configuration 
- Set up MySQL database connection using Knex.js 
- Create Knex migrations for required tables 
- Create Knex seed files with sample data 
- Set up Firebase project and configure authentication SDK 
- Gather 15 sample attraction geolocations for two cities 

Features (Split by Frontend/Backend Components)

 Backend Feature Components
- List attractions endpoint: Create GET /attractions endpoint with Knex queries
- View attraction details: Implement GET /attractions/:id endpoint
- Protected routes: Connect Firebase auth with Express backend


 Feature: Home page
- List attractions: Build React component with Axios integration, Add localStorage for location data
- Create GET /api/cities
 

 Feature: City Details
-Implement city details page
-Create GET /api/cities/:id endpoint
-Create detailed view component with SCSS styling, Set up dynamic routing with react-router

Feature: Map
-Implement interactive map page
-Fetch and display locations from the database
-Create GET /api/cities/:cityId/attractions endpoint

Feature: Itinerary
-Implement itinerary page to view saved locations
-Create GET /api/itinerary endpoint to fetch user's saved itinerary
-Create POST /api/itinerary endpoint to add places to the itinerary
-Create DELETE /api/itinerary/:id endpoint to remove places from itinerary
-Authentication: Required

- Deploy client and server projects with automatic deployment 
- Address any lingering issues with Firebase auth
- Additional bug fixes as needed
- Final deployment check 
- Bug fixes and testing 


- DEMO DAY

## Nice-to-haves
- Ability to add the itinerary
- Forgot password functionality
- Mode to transportation
- Expanded user information: 
        - Saving itinerary
        - Implement login and register pages with forms
        - Create POST /api/users endpoint to register a user after Firebase authentication
        - Create POST /api/auth/verify endpoint to verify Firebase token and return session info
-Reviews and Ratings for Attractions
-Expanded User Information
    -Allow users to save additional information like preferences (e.g., interests in types of attractions, food, etc.).
    -Enable users to save and categorize their itineraries (e.g., by city, by trip dates, etc.).
