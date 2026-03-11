<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Care Support Website</title>
<meta name="viewport" content="width=device-width, initial-scale=1">

<style>

body{
font-family: Arial;
text-align: center;
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

#content{
margin-top:20px;
}

</style>

</head>

<body>

<h1>Care Support Website</h1>

<button onclick="showHome()">Home</button>
<button onclick="showContacts()">Contacts</button>
<button onclick="showGames()">Games</button>

<div id="content"></div>

<script>

/* LOAD SAVED NUMBERS */

let doctor = localStorage.getItem("doctor") || "";
let family = localStorage.getItem("family") || "";
let emergency = localStorage.getItem("emergency") || "";

/* HOME */

function showHome(){

document.getElementById("content").innerHTML = `
<h2>Welcome</h2>
<p>This website helps Blind, Disabled and Old Age people.</p>
<button onclick="speak()">🔊 Speak</button>
`;

}

/* VOICE */

function speak(){

const speech = new SpeechSynthesisUtterance(
"Welcome to Care Support Website"
);

speechSynthesis.speak(speech);

}

/* CONTACT PAGE */

function showContacts(){

document.getElementById("content").innerHTML = `
<h2>Emergency Contacts</h2>

<h3>Doctor</h3>
<input id="doctorInput" placeholder="Enter doctor number" value="${doctor}">
<button onclick="saveDoctor()">Save</button>
<br>
<a id="doctorCall" href="tel:${doctor}">
<button>Call Doctor</button>
</a>

<hr>

<h3>Family</h3>
<input id="familyInput" placeholder="Enter family number" value="${family}">
<button onclick="saveFamily()">Save</button>
<br>
<a id="familyCall" href="tel:${family}">
<button>Call Family</button>
</a>

<hr>

<h3>Emergency</h3>
<input id="emergencyInput" placeholder="Enter emergency number" value="${emergency}">
<button onclick="saveEmergency()">Save</button>
<br>
<a id="emergencyCall" href="tel:${emergency}">
<button>Call Emergency</button>
</a>
`;

}

/* SAVE FUNCTIONS */

function saveDoctor(){

doctor = document.getElementById("doctorInput").value;

localStorage.setItem("doctor", doctor);

alert("Doctor number saved");

showContacts();

}

function saveFamily(){

family = document.getElementById("familyInput").value;

localStorage.setItem("family", family);

alert("Family number saved");

showContacts();

}

function saveEmergency(){

emergency = document.getElementById("emergencyInput").value;

localStorage.setItem("emergency", emergency);

alert("Emergency number saved");

showContacts();

}

/* GAMES PAGE */

function showGames(){

document.getElementById("content").innerHTML = `
<h2>Games</h2>

<button onclick="guessGame()">Guess Game</button>
<button onclick="mathGame()">Math Game</button>
<button onclick="colorGame()">Color Game</button>

<div id="gameArea"></div>
`;

}

/* GAME 1 */

let random = Math.floor(Math.random()*5)+1;

function guessGame(){

document.getElementById("gameArea").innerHTML = `
<h3>Guess Number Game</h3>
<p>Guess number between 1 to 5</p>

<input id="guessInput">
<button onclick="checkGuess()">Check</button>

<p id="guessResult"></p>
`;

}

function checkGuess(){

let g = document.getElementById("guessInput").value;

if(g == random)
document.getElementById("guessResult").innerHTML="Correct!";
else
document.getElementById("guessResult").innerHTML="Try Again!";

}

/* GAME 2 */

function mathGame(){

let a = Math.floor(Math.random()*10);
let b = Math.floor(Math.random()*10);

document.getElementById("gameArea").innerHTML = `
<h3>Math Game</h3>

<p>${a} + ${b} = ?</p>

<input id="mathInput">

<button onclick="checkMath(${a+b})">Check</button>

<p id="mathResult"></p>
`;

}

function checkMath(ans){

let user = document.getElementById("mathInput").value;

if(user == ans)
document.getElementById("mathResult").innerHTML="Correct!";
else
document.getElementById("mathResult").innerHTML="Wrong!";

}

/* GAME 3 */

function colorGame(){

document.getElementById("gameArea").innerHTML = `
<h3>Color Game</h3>

<p>What color is the sky?</p>

<button onclick="checkColor('blue')">Blue</button>
<button onclick="checkColor('green')">Green</button>

<p id="colorResult"></p>
`;

}

function checkColor(c){

if(c == "blue")
document.getElementById("colorResult").innerHTML="Correct!";
else
document.getElementById("colorResult").innerHTML="Wrong!";

}

/* START PAGE */

showHome();

</script>

</body>
</html>
