# WanderTiki APIs
Phone and web APIs

**Terminal commands to purge database:**

```
// purge database of all messages
npm run db purge:messages

// purge database of all users
npm run db purge:users

// purge database of all message threads
npm run db purge:threads
```
## API route documentation
 ### Authentication:
`#POST /login` Login a user with JSON Web Tokens
```
Request fields
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
### Users:
`#POST /user` Used to create a new user e.g registration
```
Request fields
{
    "first_name": "Jose",       // required
    "last_name": "Hernandez",   // required
    "email": "some@email.com",  // required
    "password": "value"         // required
}
```
```
Response in JSON
{
    "status": ["pending"], // ENUM [‘pending’, ‘active’, ‘suspended’]
    "_id": "5e0c0892f0ec84f89b464ca2",
    "first_name": "Jose",
    "last_name": "Hernandez",
    "email": "some@email.com",
    "password": "value",
    "created_date": "1577845074", // UNIX timestamp
    "__v": 0
}
```

`#GET /user/:userID` Get user information by user ID
```
Response in JSON
{
    "status": ["pending"], // ENUM [‘pending’, ‘active’, ‘suspended’]
    "_id": "5e0bb87a364cc7e9c12a5214",
    "first_name": "Jose",
    "last_name": "Hernandez",
    "email": "some@email.com",
    "password": "value",
    "created_date": "1577845074", // UNIX timestamp
    "__v": 0
}
```
