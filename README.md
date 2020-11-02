# my-mern-app

## GOAL: Build a fullstack MERN App

## Steps

### 1. Setup the server.js

- Create your `server.js` file.
- Run `npm init -y`
- Run `npm install express mongoose dotenv if-env`
- Build out the basic server

```javascript
require("dotenv").config();
const express = require("express");
const mongoose = require("mongoose");

const PORT = process.env.PORT || 3001;

const app = express();

app.use(express.urlencoded({ extended: true }));
app.use(express.json());

mongoose.connect(process.env.MONGODB_URI || "mongodb://localhost/my-mern", {
  useNewUrlParser: true,
  useUnifiedTopology: true,
  useCreateIndex: true,
  useFindAndModify: false,
});

const connection = mongoose.connection;

connection.on("connected", () => {
  console.log("Mongoose successfully connected.");
});

connection.on("error", (err) => {
  console.log("Mongoose connection error: ", err);
});

app.get("/api/config", (req, res) => {
  res.json({
    success: true,
  });
});

app.listen(PORT, () => {
  console.log(`App is running on http://localhost:${PORT}`);
});
```


### 2. Add create-react-app client on top. 
* In the root, run `npx create-react-app client --use-npm`