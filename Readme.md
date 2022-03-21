### sign-up

- **location** : /api/auth/signup
- **api**:
- **method** : POST
- **working** : takes parameter and creats a user
- **Code** : 

```jsx
{
      // import user.js from Models
const user = require("../../Models/user");

// require bcryptjs to hash the password
const bcrypt = require("bcryptjs");


// create a sign up callback with follwing fields:-
// 1. name
// 2. email
// 3. phone
// 4. usertype
// 5. password (encrypt the password using bcryptjs)

const SignUp = async (req, res) => {
  try {
    const { name, email, phone, usertype, password } = req.body;

    // check if the user already exists
    const userExists = await user.exists({ email });

    if (userExists) {
      return res.status(400).json({
        error: "user already exists",
      });
    }

    // hash the password
    const salt = await bcrypt.genSalt(10);
    const hashedPassword = await bcrypt.hash(password, salt);

    // create a new user
    const newUser = new user({
      name,
      email,
      phone,
      usertype,
      password: hashedPassword,
    });

    // after 

    // save the user
    await newUser.save();

    

    // send a response
    res.json({
      msg: "user successfully created",
    });
  } catch (err) {
    console.log(err.message);
    res.json({
      error: err.message,
    });
  }
};

module.exports = { SignUp };
```

- **Example Input** :

```jsx
{
      "name":"Deeapm"
      "email":"kumardeepam8600@gmail.com",
      "phone":"9845738299",
      "password":"password",

}
```

- **status** :
- 200, status :0 and msg:"Created" if it is succesfull
- status:"un", msg:"Username not sent"
- status:'ue',msg:"Username is not unique"
- "msg":"didnt work"

### Login

- **location** : /api/auth/Login
- **api**:
- **method** : POST
- **working** : takes parameter and creats a user

- **Example Input** :

```jsx
{
      
```

- **status** :
- 200, status :0 and msg:"Created" if it is succesfull
- "msg":"didnt work"


