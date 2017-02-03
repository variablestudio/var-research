# Electron

## communicating between windows
http://electron.atom.io/docs/api/ipc-main/

```javascript
// In main process.
const {ipcMain} = require('electron')
ipcMain.on('asynchronous-message', (event, arg) => {
  console.log(arg)  // prints "ping"
  event.sender.send('asynchronous-reply', 'pong')
})

ipcMain.on('synchronous-message', (event, arg) => {
  console.log(arg)  // prints "ping"
  event.returnValue = 'pong'
})

// In renderer process (web page).
const {ipcRenderer} = require('electron')
console.log(ipcRenderer.sendSync('synchronous-message', 'ping')) // prints "pong"

ipcRenderer.on('asynchronous-reply', (event, arg) => {
  console.log(arg) // prints "pong"
})
ipcRenderer.send('asynchronous-message', 'ping')`
```

## socket.io

server.js
```javascript
var express = require('express')
var server = express()
var http = require('http').Server(server)
var io = require('socket.io')(http)

server.use(express.static('.'))

io.on('connection', function (socket) {
  console.log('a user connected')
})

http.listen(3010, function () {
  console.log('listening on *:3010')
})
```

html
```html
<script src="http://localhost:3010/socket.io/socket.io.js"></script>
```

client.js
```javascript
var socket = io('http://localhost:3010')
socket.on('news', function (data) {
  console.log(data)
  socket.emit('my other event', { my: 'data' })
})
```


