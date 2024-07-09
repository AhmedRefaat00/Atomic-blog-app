# Atomic Blog README

## Overview

Atomic Blog is a simple React application for managing blog posts. It includes functionalities for adding, searching, and archiving posts, as well as toggling a fake dark mode. This project utilizes React hooks such as `useState` and `useEffect`, and employs a context provider for state management.

## Features

- Toggle fake dark mode.
- Add new posts.
- Search through posts.
- Clear all posts.
- Archive posts and add them back to the main list.

## Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/your-username/atomic-blog.git
   cd atomic-blog
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Start the application**:
   ```bash
   npm start
   ```

## File Structure

```
.
├── src
│   ├── App.js
│   ├── PostProvider.js
│   └── index.js
├── public
│   └── index.html
└── package.json
```

## Components

### `App`
The main component that renders the entire application. It includes the header, main content area, archive, and footer. It also manages the fake dark mode.

### `Header`
Contains the application title, the number of posts, search functionality, and a button to clear all posts.

### `Main`
Includes the form to add a new post and the list of current posts.

### `Archive`
Shows archived posts and allows adding them back to the main list.

### `Footer`
Displays the footer of the application.

## Usage

### Toggling Fake Dark Mode

Click the button with the sun/moon icon to toggle between fake dark mode and light mode. This changes the class on the `documentElement`.

### Adding a Post

1. Fill out the "Post title" and "Post body" fields.
2. Click the "Add post" button.

### Searching Posts

Type into the search input field to filter posts based on their titles.

### Clearing Posts

Click the "Clear posts" button to remove all posts from the list.

### Viewing and Adding Archived Posts

1. Click the "Show archive posts" button to view archived posts.
2. Click the "Add as new post" button next to an archived post to add it to the main list.

## Context Provider

### `PostProvider`
Handles the state management for posts using React's Context API. It provides functions to add, clear, and search posts.

### `usePosts`
A custom hook to consume the post context in various components.

## Dependencies

- React
- faker (for generating random posts)

## Example Code

Here's a brief look at how the `PostProvider` and `usePosts` are used in the application:

### `PostProvider.js`
```javascript
import { createContext, useContext, useState } from 'react';
import faker from 'faker';

const PostContext = createContext();

export function PostProvider({ children }) {
  const [posts, setPosts] = useState([]);

  function createRandomPost() {
    return {
      title: `${faker.hacker.adjective()} ${faker.hacker.noun()}`,
      body: faker.hacker.phrase(),
    };
  }

  function onAddPost(post) {
    setPosts([...posts, post]);
  }

  function onClearPosts() {
    setPosts([]);
  }

  const value = {
    posts,
    onAddPost,
    onClearPosts,
  };

  return <PostContext.Provider value={value}>{children}</PostContext.Provider>;
}

export function usePosts() {
  return useContext(PostContext);
}
```

### Usage in `App.js`
```javascript
import { PostProvider, usePosts } from './PostProvider';

function App() {
  return (
    <PostProvider>
      <Header />
      <Main />
      <Archive />
      <Footer />
    </PostProvider>
  );
}
```

