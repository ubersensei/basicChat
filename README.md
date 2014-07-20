#basicChat



###1
`express basicChat`

comment out the below in app.js:

```javascript
//var routes = require('./routes/index');
//var users = require('./routes/users');
```

```javascript
// view engine setup
//app.set('views', path.join(__dirname, 'views'));
//app.set('view engine', 'jade');
```

```javascript
//app.use('/', routes);
//app.use('/users', users);
```

and instead, add the below in `app.js`:

```javascript
app.get('/', function (req, res) {
    res.sendfile(__dirname + '/index.html');
});
```
create the file `index.html` under `/public/`


###2
`git init`, `.gitignore` commits

###3
cut the below from `/bin/wwww` and paste it into `app.js`

```javascript
var debug = require('debug')('basicChat');
app.set('port', process.env.PORT || 3000);

var server = app.listen(app.get('port'), function() {
    debug('Express server listening on port ' + server.address().port);
});
```

###4
`npm install socket.io --save`
and copy the following into `app.js`

```javascript
var io = require('socket.io').listen(server);
io.on('connection', function (socket) {
    console.log("user connected");
    socket.emit('news', { hello: 'world' });
    socket.on('my other event', function (data) {
        console.log(data);
    });
});
```

###5
Add the client side code:
```javascript
<body>
Please work !

<script src="/socket.io/socket.io.js"></script>
<script>
    var socket = io.connect('http://localhost');
    socket.on('news', function (data) {
        console.log(data);
        socket.emit('my other event', { my: 'data' });
    });
</script>
</body>
```

