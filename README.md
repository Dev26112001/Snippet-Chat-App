# Snippet-Chat-App
//index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Snippet chat app</title>
    <script defer src="http://localhost:8000/socket.io/socket.io.js"></script>
    <script defer src = "js/client.js"></script>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <nav>
        <img class = "logo" src="chat.png.png" alt="">
        <h1>Welcome to Snippet Chat app</h1>
    </nav>
    <div class="container">
        <div class="message right">Dev: Hey , whats up</div>
        <div class="message left">Rajveer: I am fine bro</div>
    </div>

    <div class = "send">
        <form action="#" id="send-container">
            <input type="text" name="messageInp" id="messageInp">
            <button class="btn" type="submit">Send</button>

        </form>
    </div>

</body>
</html>

//style.css
body{
    height: 100vh;
    background-image: linear-gradient(rgb(191, 212, 69), rgb(216, 58, 124));
}


.logo{
     display: block;
     margin: auto;
     width: 133px;
     height: 107px;

}

h1{
    margin-top: 12px;
    font-size: 30px;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    text-align: center;
}

.container{
          max-width: 955px;
          border: 2px solid black;
          margin: auto;
          height: 60vh;
          padding: 33px;
          overflow-y: auto;
          margin-bottom: 23px;
}

.message{
        background-color: grey;
        width: 24%;
        padding: 10px;
        margin: 17px 12px;
        border: 2px solid black;
        border-radius: 10px;

}

.left{
     float: left;
     clear: both;

}

.right{
      float: right;
      clear: both;

}

#send-container{
    display: block;
    margin: auto;
    text-align: center;
    max-width: 985px;
    width: 100%;
}

#messageInp{
    width: 92%;
    border: 2px solid black;
    border-radius: 6px;
    height: 34px;
}

.btn{
    cursor: pointer;
    border: 2px solid black;
    border-radius: 6px;
    height: 34px;
}

//client.js
const e = require("cors");

const socket = io(http://localhost:8000)

const form = document.getElementById('send-container');
const messageInput = document.getElementById('messageInp')
const messageContainer = document.querySelector(".container")
var audio = new Audio('notification_sound.mp3.mp3');

const append = (message, position) =>{
    const messageElement = document.createElement('div')
    messageElement.innerText = message;
    messageElement.classList.add('message');
    messageElement.classList.add('position');
    messageContainer.append(messageElement);
    if(position == 'left'){
        audio.play();
    }

}

form.addEventListener('submit', () =>{
    e.preventDefault();
    const message = messageInput.valur;
    append('You : ${message}', 'right');
    socket.emit('send', message);
    messageInput.value = ''
}
//const name = prompt("Enter your name to join ")
socket.emit('new-user-joined', name)

socket.on('user-joined', name =>{
    append('${name} joined the chat', 'right')

})

//index.js
const io = require('socket.io')(8000)

const users = {};

io.on('connection',socket =>{
    socket.on('new-user-joined', name =>{
        //console.log("New user", name)
        user[socket.id] = name;
        socket.broadcast.emit('user-joined')
    });

    socket.on('send', message =>{
        socket.broadcast.emit('receive', {message : message, name: user[socket,id] })

    });

    socket.on('disconnect', message =>{
        socket.broadcast.emit('left', users[socket.id] });
        delete users[socket.id];
})
