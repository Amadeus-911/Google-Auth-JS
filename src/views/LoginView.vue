<template>
    <div class="container">
        <div class="login-box">
          <h2>Login</h2>
          <form>
            <div class="input-group">
              <label>Email:</label>
              <input type="email" name="email" required>
            </div>
            <div class="input-group">
              <label>Password:</label>
              <input type="password" name="password" required>
            </div>
            <div class="input-group">
              <button type="submit" class="login-button">Login</button>
            </div>
            <div class="separator">
              <span>or</span>
            </div>
            <div class="input-group">
                <button type="button" class="google-button" @click="handleClick">
                  <i class="fa-brands fa-google"></i> Sign in with Google
                </button>
            </div>
          </form>
        </div>
    </div>
</template>


<script>



function googleSignIn(){
    // Google's OAuth 2.0 endpoint for requesting an access token
    var oauth2Endpoint = 'https://accounts.google.com/o/oauth2/v2/auth';

    // Create <form> element to submit parameters to OAuth 2.0 endpoint.
    var form = document.createElement('form');
    form.setAttribute('method', 'GET'); // Send as a GET request.
    form.setAttribute('action', oauth2Endpoint);

    // Parameters to pass to OAuth 2.0 endpoint.
    var params = {'client_id': '1020136124385-i9is0ag7pr3hapsa97ac1u06horb932a.apps.googleusercontent.com',
                'redirect_uri': 'http://localhost:8080/',
                'response_type': 'token',
                'scope': 'https://www.googleapis.com/auth/drive.metadata.readonly',
                'include_granted_scopes': 'true',
                'state': 'pass-through value'};

    // Add form parameters as hidden input values.
    for (var p in params) {
        var input = document.createElement('input');
        input.setAttribute('type', 'hidden');
        input.setAttribute('name', p);
        input.setAttribute('value', params[p]);
        form.appendChild(input);
    }

    // Add form to page and submit it to open the OAuth 2.0 endpoint.
    document.body.appendChild(form);
    form.submit();
}


// const url = new URL(window.location.href);

// const searchParams = new URLSearchParams(url.hash.substr(1));
// const state = searchParams.get('state');
// const access_token = searchParams.get('access_token');
// const token_type = searchParams.get('token_type');
// const expires_in = searchParams.get('expires_in');
// const scope = searchParams.get('scope');
// const authuser = searchParams.get('authuser');
// const prompt = searchParams.get('prompt');




function cleanUrl(){
    const currentURL = window.location.href;
    const cleanURL = currentURL.split('#')[0];
    window.history.replaceState({}, document.title, cleanURL);
}

//cleanUrl()

export default {
    name: 'LoginView',
    data(){
        return{
        }
        
    },
    methods :{
        async handleClick(){
            await googleSignIn()
        }
    }
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
    
    input[type="email"],
    input[type="password"] {
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
    