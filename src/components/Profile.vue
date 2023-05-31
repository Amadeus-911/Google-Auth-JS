<template>
    <div class="user-profile">
      <div class="profile-picture">
        <img :src="imageUrl" :alt="name" />
      </div>
      <div class="profile-details">
        <h3>{{ name }}</h3>
        <p>{{ email }}</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'UserProfile',
    props: {
      imageUrl: {
        type: String,
        required: true
      },
      name: {
        type: String,
        required: true
      },
      email: {
        type: String,
        required: true
      }
    }
  };
  </script>
  
  <style scoped>
  .user-profile {
    display: flex;
    align-items: center;
  }
  
  .profile-picture img {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    object-fit: cover;
    margin-right: 10px;
  }
  
  .profile-details {
    display: flex;
    flex-direction: column;
  }
  
  .profile-details h3 {
    margin: 0;
    font-size: 20px;
  }
  
  .profile-details p {
    margin: 0;
    font-size: 16px;
    color: #888;
  }
  </style>
  