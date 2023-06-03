<template>
    <div class="container">
        <div class="login-box">
            <h2>Login</h2>
            <form>
                <div class="input-group">
                    <label>Email:</label>
                    <input type="email" name="email" required />
                </div>
                <div class="input-group">
                    <label>Password:</label>
                    <input type="password" name="password" required />
                </div>
                <div class="input-group">
                    <button type="submit" class="login-button">Login</button>
                </div>
                <div class="separator">
                    <span>or</span>
                </div>
                <div class="input-group">
                    <div id="buttonDiv"></div>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
    import router from '@/router'

    export default {
        name: 'login',
        mounted() {
            const handleCredentialResponse = (response) => {
                console.log('Encoded JWT ID token: ' + response.credential)
                localStorage.setItem('token', response.credential)
                router.push('/')
            }

            google.accounts.id.initialize({
                client_id: '1020136124385-i9is0ag7pr3hapsa97ac1u06horb932a.apps.googleusercontent.com',
                callback: handleCredentialResponse,
            })

            google.accounts.id.renderButton(document.getElementById('buttonDiv'), {
                theme: 'outline',
                size: 'large',
                locale: 'EN-US',
            })

            google.accounts.id.prompt() // Also display the One Tap dialog
        },
    }
</script>

<style scoped>
    body {
        font-family: Arial, sans-serif;
        background-color: #f2f2f2;
        margin: 0;
        padding: 0;
    }

    .container {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
    }

    .login-box {
        background-color: #ffffff;
        padding: 40px;
        border-radius: 6px;
        box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        max-width: 400px;
        width: 100%;
    }

    h2 {
        text-align: center;
        margin-top: 0;
        margin-bottom: 20px;
        color: #333333;
    }

    .input-group {
        margin-bottom: 20px;
    }

    label {
        display: block;
        margin-bottom: 5px;
        color: #666666;
    }

    input[type='email'],
    input[type='password'] {
        width: 100%;
        padding: 10px;
        border: 1px solid #cccccc;
        border-radius: 4px;
        color: #333333;
    }

    .login-button {
        display: block;
        width: 100%;
        padding: 10px;
        background-color: #4285f4;
        border: none;
        border-radius: 4px;
        color: #ffffff;
        font-size: 16px;
        cursor: pointer;
    }

    .google-button {
        display: flex;
        align-items: center;
        justify-content: center;
        width: 100%;
        padding: 10px;
        background-color: #f2f2f2;
        border: 1px solid #cccccc;
        border-radius: 4px;
        color: #666666;
        font-size: 16px;
        cursor: pointer;
    }

    .google-button:hover {
        background-color: #e0e0e0;
    }

    .google-button i {
        margin-right: 10px;
    }

    .separator {
        text-align: center;
        margin: 20px 0;
    }

    .separator span {
        background-color: #ffffff;
        padding: 0 10px;
        color: #999999;
        font-size: 14px;
    }
</style>
