<template>
  <div class="home">
    <Navbar />
    <Profile :imageUrl="user.imageUrl" :name="user.name" :email="user.email"/>
  </div>
</template>

<script>
// @ is an alias to /src

import Navbar from '@/components/Navbar.vue';
import Profile from '../components/Profile.vue'



const url = new URL(window.location.href)
const fragment = url.hash;
const cleanedFragment = fragment.slice(1);
const paramsArray = cleanedFragment.split('&');
const params = {};
paramsArray.forEach(param => {
  const [key, value] = param.split('=');
  params[key] = value;
});

console.log(params, params.access_token);

const g_access_token = params.access_token


if( g_access_token != null){
    const apiUrl = "https://www.googleapis.com/oauth2/v3/userinfo";
    fetch(apiUrl, {
    headers: {
        Authorization: `Bearer ${g_access_token}`
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
        uData = data
        localStorage.setItem('imgUrl', data.picture);
        localStorage.setItem('name', data.given_name.concat(' ', data.family_name));
        localStorage.setItem('email', data.email);

    })
    .catch(error => {
        console.error(error);
    });

}



export default {
  name: 'HomeView',
  components : {
    Navbar,
    Profile
  },
  data() {
    return {
      user: {
        imageUrl: localStorage.getItem('imgUrl'),
        name: localStorage.getItem('name'),
        email: localStorage.getItem('email')
      }
    };
  }
  
}

</script>
