#Sign in with JS

This Application is created for testing google sign in in localhost. 
This follows the official documentation of Google (https://developers.google.com/identity/protocols/oauth2/javascript-implicit-flow)

At first a google application has to be set up for client ID and Client Secret. 
Go to https://console.cloud.google.com/apis/credentials?project=life-good-315813

# Set up OAuth Consent Screen
Give app name -> 
centact email address -> 
application home page url (here localhost/Myapp) -> 
give test email address
and continue and Save.

# Go to Credentials
Create Credential ->  
Oauth Client Id -> 
Web Application -> 
add web app name -> 
add redirect uri (the url where google will send back its response such as localhost/login.php)

Download the config JSON file containing client ID and Client Secret


# client

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
