<template>
    <h2>Redirecting</h2>
</template>

<script>
    import router from '@/router'

    export default {
        name: 'parse',
        mounted() {
            const url = new URL(window.location.href)
            const fragment = url.hash
            const cleanedFragment = fragment.slice(1)
            const paramsArray = cleanedFragment.split('&')
            const params = {}
            paramsArray.forEach((param) => {
                const [key, value] = param.split('=')
                params[key] = value
            })

            localStorage.setItem('accessToken', params.access_token)
            localStorage.setItem('isToken', true)
            if (params.access_token) {
                router.push('/')
            } else {
                router.push('/login?login_failed=1')
            }
        },
    }
</script>

<style></style>
