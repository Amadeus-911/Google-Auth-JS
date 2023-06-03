<template>
    <div class="home">
        <Navbar :isLoggedIn="isLoggedIn" @logout="logout" />
        <div class="container">
            <Profile :imageUrl="picture" :name="name" :email="email" />
        </div>
    </div>
</template>

<script>
    import Navbar from '@/components/Navbar.vue'
    import Profile from '@/components/Profile.vue'
    // @ is an alias to /src

    export default {
        name: 'HomeView',
        components: { Navbar, Profile },
        data() {
            return {
                email: '',
                name: '',
                picture: '',
                isLoggedIn: false,
            }
        },
        methods: {
            getJwtPayload(token) {
                try {
                    const base64Url = token.split('.')[1]
                    const base64 = base64Url.replace(/-/g, '+').replace(/_/g, '/')
                    const decodedToken = JSON.parse(window.atob(base64))

                    return decodedToken
                } catch (error) {
                    console.error('Error decoding JWT token:', error.message)
                    return null
                }
            },
            logout() {
                this.isLoggedIn = false
                localStorage.removeItem('token')
                this.email = ''
                this.name = ''
                this.picture = ''
            },
        },
        created() {
            const token = localStorage.getItem('token')
            if (token) {
                const payload = this.getJwtPayload(token)
                this.name = payload.family_name ? payload.given_name + ' ' + payload.family_name : payload.given_name
                this.email = payload.email
                this.picture = payload.picture
                this.isLoggedIn = true
                console.log(this.name)
            }
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
