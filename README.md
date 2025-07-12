# SocietySpot Club Management System

A web-based club management system built with PHP and MySQL that helps educational institutions manage their clubs, members, and activities efficiently.

## Features

- **User Management**: Multi-role system supporting students, club members, club leaders, and administrators
- **Club Management**: Create and manage clubs with descriptions, announcements, and events
- **Post System**: Share updates and information through a built-in posting system
- **Rewards System**: Track and manage user achievements and rewards
- **Real-time Updates**: Automatic timestamp tracking for all activities

## Prerequisites

- PHP (Latest stable version recommended)
- XAMPP/WAMP/MAMP server
- MySQL Database
- Web Browser

## Installation

1. Install and start XAMPP server
2. Clone this repository to your XAMPP's `htdocs` directory
3. Create a new database named `club_managment` in phpMyAdmin
4. Set up the required tables by running these SQL commands in phpMyAdmin:

### Users Table
```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    role ENUM('student', 'club_member', 'club_leader', 'administrator') NOT NULL DEFAULT 'student',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

### Clubs Table
```sql
CREATE TABLE clubs (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    description TEXT NOT NULL,
    creation_date DATE NOT NULL,
    club_leader_id INT NOT NULL,
    announcements TEXT,
    events TEXT,
    posts TEXT,
    members TEXT,
    FOREIGN KEY (club_leader_id) REFERENCES users(id) ON DELETE CASCADE ON UPDATE CASCADE
);
```

### Rewards Table
```sql
CREATE TABLE rewards (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    reward TEXT NOT NULL,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

### Posts Table
```sql
CREATE TABLE posts (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    content TEXT NOT NULL,
    user_id INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

## Usage

1. Start your XAMPP server (Apache and MySQL)
2. Open your web browser
3. Navigate to: `http://localhost/swe/admin/home.php`

## User Roles

- **Student**: Basic access to view clubs and posts
- **Club Member**: Participate in club activities
- **Club Leader**: Manage club content and members
- **Administrator**: Full system access and management



