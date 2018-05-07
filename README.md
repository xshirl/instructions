# instructions to create a react/express app

A. Create Express side.
1. npm init
2. npm i express morgan body-parser pg-promise
```
const express = require('express');
const logger = require('morgan');
const bodyParser = require('body-parser');

const todoRouter = require('./routes/todoRouter')

const app = express();

const PORT = process.env.PORT || 3001;

app.use(logger('dev'));
app.use(bodyParser.urlencoded({extended:false}));
app.use(bodyParser.json());

if(process.env.NODE_ENV === 'production') {
  app.use(express.static('client/build'));
}

app.use('/api/todos', todoRouter);

app.listen(PORT, ()=> {
  console.log(`Listening on port ${PORT}`);
})
```

3. Create routes, controllers, models, config, db folders. 
4. Create create-react-app name in folder. 
5. cd into client/ and build the React app with npm run build
6. Add below to package.json for express side
```
"scripts": {
    "start": "node server.js",
    "dev": "concurrently \"npm run start-server\" \"npm run start-client\"",
    "start-server": "nodemon server.js",
    "start-client": "cd client && npm start",
    "reset-db": "psql -f db/schema.sql && psql -f db/seed.sql"
}
```
7. Add "proxy": "http://localhost:3001" to react side package.json (end)
