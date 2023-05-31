<template>
    <nav class="navbar">
      <div class="navbar-left">Test Google Login</div>
      <div class="navbar-right">
        <router-link to="/login" class="login-link">Login</router-link>
      </div>
    </nav>
  </template>
  
  <style>
  .navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #f44336; /* Red color */
    padding: 15px;
    color: white;
  }
  
  .navbar-left {
    font-weight: bold;
  }
  
  .login-link {
    color: white;
    text-decoration: none;
    padding: 8px 16px;
    border-radius: 4px;
    background-color: transparent;
    border: 1px solid white;
    transition: background-color 0.3s, border-color 0.3s;
  }
  
  .login-link:hover {
    background-color: white;
    color: #f44336; /* Red color */
  }
  </style>
  