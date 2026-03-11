<!DOCTYPE html>
<html>
<head>

<title>Care Support Website</title>

<meta name="viewport" content="width=device-width, initial-scale=1">

<style>

body{
font-family:Arial;
text-align:center;
background:#f2f2f2;
margin:0;
padding:20px;
}

h1{
color:green;
}

button{
margin:8px;
padding:12px 20px;
background:green;
color:white;
border:none;
border-radius:6px;
font-size:16px;
cursor:pointer;
}

input{
padding:8px;
margin:5px;
}

.box{
margin-top:20px;
}

</style>

</head>

<body>

<h1>Care Support Website</h1>

<button onclick="showHome()">Home</button>
<button onclick="showContacts()">Contacts</button>
<button onclick="showGames()">Games</button>

<div id="content" class="box"></div>

<script>

/* STORAGE */

let doctor = localStorage.getItem("doctor") || "";
let family = localStorage.getItem("family") || "";
let emergency = localStorage.getItem("emergency") || "";

/* HOME */

function showHome(){

document.getElementById("content").innerHTML=
`
<h2>Welcome</h2>

<p>This website helps Blind, Disabled and Old Age people.</p>

<button onclick="speak()">🔊 Speak</button>
`;

}

function speak(){

const speech=new SpeechSynthesisUtterance(
"Welcome to Care Support Website"
);

speechSynthesis.speak(speech);

}

/* CONTACT PAGE */

function showContacts(){

document.getElementById("content").innerHTML=
`
<h2>Emergency Contacts</h2>

<h3>Doctor Number</h3>

<input id="doctorInput" value="${doctor}" placeholder="Enter doctor number">

<button onclick="saveDoctor()">Save</button>

<br>

<a href="tel:${doctor}">
<button>Call Doctor</button>
</a>

<hr>

<h3>Family Number</h3>

<input id="familyInput" value="${family}" placeholder="Enter family number">

<button onclick="saveFamily()">Save</button>

<br>

<a href="tel:${family}">
<button>Call Family</button>
</a>

<hr>

<h3>Emergency Number</h3>

<input id="emergencyInput" value="${emergency}" placeholder="Enter emergency number">

<button onclick="saveEmergency()">Save</button>

<br>

<a href="tel:${emergency}">
<button>Call Emergency</button>
</a>
`;

}

/* SAVE FUNCTIONS */

function saveDoctor(){

doctor=document.getElementById("doctorInput").value;

localStorage.setItem("doctor",doctor);

alert("Doctor number saved");

}

function saveFamily(){

family=document.getElementById("familyInput").value;

localStorage.setItem("family",family);

alert("Family number saved");

}

function saveEmergency(){

emergency=document.getElementById("emergencyInput").value;

localStorage.setItem("emergency",emergency);

alert("Emergency number saved");

}

/* GAMES PAGE */

function showGames(){

document.getElementById("content").innerHTML=
`
<h2>Games</h2>

<button onclick="guessGame()">Guess Game</button>
<button onclick="mathGame()">Math Game</button>
<button onclick="colorGame()">Color Game</button>

<div id="gameArea"></div>
`;

}

/* GUESS GAME */

let random=Math.floor(Math.random()*5)+1;

function guessGame(){

document.getElementById("gameArea").innerHTML=
`
<h3>Guess Number Game</h3>

<p>Guess number between 1 to 5</p>

<input id="guess">

<button onclick="checkGuess()">Check</button>

<p id="result"></p>
`;

}

function checkGuess(){

let g=document.getElementById("guess").value;

if(g==random)
document.getElementById("result").innerHTML="Correct!";
else
document.getElementById("result").innerHTML="Try Again!";

}

/* MATH GAME */

function mathGame(){

let a=Math.floor(Math.random()*10);
let b=Math.floor(Math.random()*10);

document.getElementById("gameArea").innerHTML=
`
<h3>Math Game</h3>

<p>${a} + ${b} = ?</p>

<input id="math">

<button onclick="checkMath(${a+b})">Check</button>

<p id="mathResult"></p>
`;

}

function checkMath(ans){

let user=document.getElementById("math").value;

if(user==ans)
document.getElementById("mathResult").innerHTML="Correct!";
else
document.getElementById("mathResult").innerHTML="Wrong!";

}

/* COLOR GAME */

function colorGame(){

document.getElementById("gameArea").innerHTML=
`
<h3>Color Game</h3>

<p>What color is the sky?</p>

<button onclick="checkColor('blue')">Blue</button>
<button onclick="checkColor('green')">Green</button>

<p id="colorResult"></p>
`;

}

function checkColor(c){

if(c=="blue")
document.getElementById("colorResult").innerHTML="Correct!";
else
document.getElementById("colorResult").innerHTML="Wrong!";

}

/* START */

showHome();

</script>

</body>
</html>
