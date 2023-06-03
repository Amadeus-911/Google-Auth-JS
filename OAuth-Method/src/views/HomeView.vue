<template>
    <div class="home">
        <Navbar :isLoggedIn="isLoggedIn" @logout="logout" />
        <template v-if="isDataLoaded">
            <div class="container">
                <Profile :imageUrl="user.imageUrl" :name="user.name" :email="user.email" />
            </div>
        </template>
    </div>
</template>

<script>
    import Navbar from '@/components/Navbar.vue'
    import Profile from '../components/Profile.vue'
    import { ref } from 'vue'

    export default {
        name: 'HomeView',
        components: {
            Navbar,
            Profile,
        },
        data() {
            return {
                user: {
                    imageUrl: '',
                    name: '',
                    email: '',
                },
                isLoggedIn: false,
                isDataLoaded: false,
            }
        },

        created() {
            const accessToken = localStorage.getItem('accessToken')

            if (accessToken != null) {
                this.isLoggedIn = true

                const apiUrl = 'https://www.googleapis.com/oauth2/v3/userinfo'
                fetch(apiUrl, {
                    headers: {
                        Authorization: `Bearer ${accessToken}`,
                    },
                })
                    .then((response) => {
                        if (response.ok) {
                            return response.json()
                        } else {
                            throw new Error('Request failed.')
                        }
                    })
                    .then((data) => {
                        console.log(data.email)
                        localStorage.setItem('imgUrl', data.picture)
                        localStorage.setItem('name', data.given_name.concat(' ', data.family_name))
                        localStorage.setItem('email', data.email)
                        this.user = {
                            imageUrl: data.picture,
                            name: data.family_name ? data.given_name.concat(' ', data.family_name) : data.given_name,
                            email: data.email,
                        }
                        this.isDataLoaded = true
                    })
                    .catch((error) => {
                        console.error(error)
                    })
            }
        },
        methods: {
            logout() {
                this.isLoggedIn = false
                this.user.imageUrl = ''
                this.user.email = ''
                this.user.name = ''
                localStorage.clear()
            },
        },
    }
</script>

<style>
    .container {
        display: flex;
        justify-content: center;
        align-items: flex-start;
        padding: 20px;
    }
</style>
