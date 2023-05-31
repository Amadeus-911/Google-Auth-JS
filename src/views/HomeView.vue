<template>
  <div class="home">
    <Navbar :isLoggedIn="isLoggedIn" @update:is-logged-in="updateIsLoggedIn" />
    <template v-if="isDataLoaded">
      <Profile :imageUrl="user.imageUrl" :name="user.name" :email="user.email" />
    </template>
  </div>
</template>

<script>
import Navbar from '@/components/Navbar.vue';
import Profile from '../components/Profile.vue';
import {ref} from 'vue'

export default {
  name: 'HomeView',
  components: {
    Navbar,
    Profile
  },
  data() {
    return {
      user: {
        imageUrl: ref(null),
        name: ref(null),
        email:ref(null)
      },
      isLoggedIn: false,
      isDataLoaded: false
    };
  },
  created() {
    const token = localStorage.getItem('isToken')
    const accessToken = localStorage.getItem('accessToken')
    console.log(token)
    if(token === 'true'){
      console.log('hello0');
      console.log(accessToken);
    }else{
      console.log('hello');
      const url = new URL(window.location.href);
      const fragment = url.hash;
      const cleanedFragment = fragment.slice(1);
      const paramsArray = cleanedFragment.split('&');
      const params = {};
      paramsArray.forEach(param => {
        const [key, value] = param.split('=');
        params[key] = value;
      });

      const g_access_token = params.access_token;

      localStorage.setItem('accessToken', g_access_token)
      localStorage.setItem('isToken', true)
      const accessToken = localStorage.getItem('accessToken')

      const cleanUrl = () => {
        const cleanURL = window.location.protocol + '//' + window.location.host + window.location.pathname;
        window.history.replaceState({}, document.title, cleanURL);
      };

      cleanUrl();
      }

      if (accessToken != null) {
        this.isLoggedIn = true;

        const apiUrl = 'https://www.googleapis.com/oauth2/v3/userinfo';
        fetch(apiUrl, {
          headers: {
            Authorization: `Bearer ${accessToken}`
          }
        })
          .then(response => {
            if (response.ok) {
              return response.json();
            } else {
              throw new Error('Request failed.');
            }
          })
          .then(data => {
            console.log(data.email);
            localStorage.setItem('imgUrl', data.picture);
            localStorage.setItem('name', data.given_name.concat(' ', data.family_name));
            localStorage.setItem('email', data.email);
            this.user = {
              imageUrl: localStorage.getItem('imgUrl'),
              name: localStorage.getItem('name'),
              email: localStorage.getItem('email')
            };
            this.isDataLoaded = true; 
          
          })
          .catch(error => {
            console.error(error);
          });
      }

    
  },
  methods: {
    updateIsLoggedIn(value) {
      this.isLoggedIn = value;
    }
  }
};
</script>
