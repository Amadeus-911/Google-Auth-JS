<template>
    <div class="about">
        <h1>This is an about page</h1>
        <div id="buttonDiv"></div>
    </div>
</template>

<script>
    export default {
        name: 'about',
        mounted() {
            function handleCredentialResponse(response) {
                console.log('Encoded JWT ID token: ' + response.credential)
            }
            window.onload = function () {
                google.accounts.id.initialize({
                    client_id: '1020136124385-i9is0ag7pr3hapsa97ac1u06horb932a.apps.googleusercontent.com',
                    callback: handleCredentialResponse,
                })
                google.accounts.id.renderButton(
                    document.getElementById('buttonDiv'),
                    { theme: 'outline', size: 'large' } // customization attributes
                )
                google.accounts.id.prompt() // also display the One Tap dialog
            }
        },
    }
</script>
