# webdevTools
Used for installing petinode webapp it includes LEMP stack with laravel

sudo webDevTools [server name]


## API route documentation
 **Authentication:**
`#POST /login` Login a user with JSON Web Tokens
```
Request in JSON
{
    "email": "jose@wandertiki.com", // required
	"password": "value"             // required
}
```
```
Response in JSON
{
    "jwt": "eyJhbiOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyI"
}
```
`#POST /logout` Logout
