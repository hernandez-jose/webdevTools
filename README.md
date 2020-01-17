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
User information sample e.g available fields:
```
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
    ...
    user information
    ...
}
```

`#GET /user/:userID` Get user information by user ID
```
Response in JSON
{
    ...
    user information
    ...
}
```

`#PUT /user/:userID` Update a user
```
Request fields
{
    "first_name": "Jose",
    "last_name": "Hernandez",
    "email": "some@email.com",
    "password": "value"
}
```

`#DELETE /user/:userID` Delete a user by ID
```
Response in JSON
{
    "message": "User successfully deleted."
}
```
### Hostel:

Hostel information sample e.g available fields
```
{
    "_id": "5e0bb87a364cc7e9c12a5214"
    "hostel_name": "USA Hostel",
    "address": "711 Post St",
    "city": "San Francisco",
    "state": "California",
    "country": "USA",
    "phone_number": "4154405600",
    "social_media": ["url_1", "url_2"],
    "languages": ["English", "Spanish"],
    "created_date": "1577845074", // UNIX timestamp
    "__v": 0
}
```

`#POST /hostel` Create a hostel
```
Request fields
{
    "hostel_name": "USA Hostel",  // required
    "address": "711 Post St",
    "city": "San Francisco",
    "state": "California",
    "country": "USA",
    "phone_number": "4154405600",
    "social_media": ["url_1", "url_2"],
    "languages": ["English", "Spanish"]
}
```
```
Response in JSON
{
    ...
    hostel information
    ...
}
```
`#GET /hostel/:hostelID` Get hostel information by ID
```
Response in JSON
{
    ...
    hostel information
    ...
}
```
`#PUT /hostel/:hostelID` Update hostel information by ID
```
Request fields
{
    "hostel_name": "USA Hostel",  // required
    "address": "711 Post St",
    "city": "San Francisco",
    "state": "California",
    "country": "USA",
    "phone_number": "4154405600",
    "social_media": ["url_1", "url_2"],
    "languages": ["English", "Spanish"]
}
```
```
Response in JSON
{
	...
	hostel updated information
	...
}
```

`#DELETE /hostel/:hostelID` Delete hostel by ID
```
Response in JSON
{
	...
	hostel information
	...
}
```

`#GET /hostel/search/name/:hostelName` Search hostel by hostel name
```
Response in JSON
[
    {
        ...
        hostel information
        ...
    },
    ...
]
```

`#GET /hostel/search/name/:hostelCity` Search hostel by city
```
Response in JSON
[
    {
        ...
        hostel information
        ...
    },
    ...
]
```

`#POST /hostle/comment/:hostelID` Post a comment on hostel page
```
Request fields
{
    "user_id": "2oiejd972jsksnc63okdhd89", // required
    "comment": "Cool place to stay."       // required
}
```
```
Response in JSON
{
    "hostel_id": "5e0bb87a364cc7e9c12a5214",
    "user_id": "2oiejd972jsksnc63okdhd89", // user that posted comment
    "comment": "Cool place to stay.",
    "created_at: "1577845074", // UNIX timestamp
    "likes": 0
}
```

`#GET /hostle/comment/:hostelID` Get hostel comment from a hostel by ID
```
Response in JSON
[
    {
        "hostel_id": "5e0bb87a364cc7e9c12a5214",
        "user_id": "2oiejd972jsksnc63okdhd89", // user that posted comment
        "comment": "Cool place to stay.",
        "created_at: "1577845074", // UNIX timestamp
        "likes": 127,
    },
    ...
]
```

`#DELETE /hostel/comment/:commentID` Delete a comment by ID
```
Response in JSON
{
    ...
    comment information
    ...
}
```

### Message:

`#POST /message` Create a new message
```
Request fields
{
    "sender_type": "user",                       // required
    "sender_id": "5e0bb87a364cc7e9c12a5214",     // required
    "receiver_type": "user",                     // required
    "receiver_id": "739shd72892asiqmcf70297hd",  // required
    "message": "The message to another user."    // required
}
```
```
Response in JSON
{
    "_id": "63hdd459jdke4jdk" // message ID
    "message": "Some message",
    "receiver_type": "user",
    "receiver_id": "739shd72892asiqmcf70297hd",
    "sender_type": "hostel",
    "sender_id": "5e0bb87a364cc7e9c12a5214",
    "created_at: "1577845074", // UNIX timestamp
    "read_at: "1577845074",    // UNIX timestamp
}
```

`#DELETE /message/:messageID` Delete a message by ID
```
Response in JSON
{
    "_id": "63hdd459jdke4jdk" // message ID
    "message": "Some message",
    "receiver_type": "user",
    "receiver_id": "739shd72892asiqmcf70297hd",
    "sender_type": "hostel",
    "sender_id": "5e0bb87a364cc7e9c12a5214",
    "created_at: "1577845074", // UNIX timestamp
    "read_at: "1577845074",    // UNIX timestamp
}
```

`#POST /message/threads` List message threads of a user
```
Request fields
{
    "receiver_type": "user",                     // required
    "receiver_id": "739shd72892asiqmcf70297hd",  // required
}
```
```
Response in JSON
[
    {
        "_id": "123jdkd45ifu578" // thread id
        "receiver_type": "user",
        "receiver_id": "739shd72892asiqmcf70297hd",
        "sender_type": "hostel",
        "sender_id": "5e0bb87a364cc7e9c12a5214",
        "created_at: "1577845074", // UNIX timestamp
        "updated_at: "1577849873", // UNIX timestamp
        "last_message": "Hello there"
    },
    ...
]
```

`#POST /message/thread` List messages from a  message thread. The receiver_id is the user looking for their messages.
```
Request fields
{
    "receiver_type": "user",                     // required
    "receiver_id": "739shd72892asiqmcf70297hd",  // required
    "sender_type": "hostel",                     // required
    "sender_id": "5e0bb87a364cc7e9c12a5214"      // required
}
```
```
Response in JSON
[
    {
        "_id": "63hdd459jdke4jdk" // message ID
        "message": "Some message",
        "receiver_type": "user",
        "receiver_id": "739shd72892asiqmcf70297hd",
        "sender_type": "hostel",
        "sender_id": "5e0bb87a364cc7e9c12a5214",
        "created_at: "1577845074", // UNIX timestamp
        "read_at: "1577845074",    // UNIX timestamp
    },
    ...
]
```

`#DELETE /message/thread/:threadID` Delete the thread and all messages inside of a thread.
```
Response in JSON
{
    "_id": "123jdkd45ifu578" // thread id
    "receiver_type": "user",
    "receiver_id": "739shd72892asiqmcf70297hd",
    "sender_type": "hostel",
    "sender_id": "5e0bb87a364cc7e9c12a5214",
    "created_at: "1577845074", // UNIX timestamp
    "updated_at: "1577849873", // UNIX timestamp
    "last_message": "Hello there"
}
```

### Push notifications:

`#POST /push/notification/ios` Send a push notification to an IOS device
```
Request fields
{
    "device_id": "kjd792kjhhae8932qlkawed",
    "user_id": "195rsdd38383jdksoaj92",
    "title": "New message received",
    "subtitle": "Event at basment 7:00PM today",
    "body": "Everone come to the basement for free drinks."
}
```
```
Response in JSON
{
    "message": "Push notification sent."
}
```

`#POST /push/device` Associate a device ID with a user ID
```
Request fields
{
    "user_id": "js77292judcnlandywo974",
    "device_id": "kjd792kjhhae8932qlkawed"
}
```
