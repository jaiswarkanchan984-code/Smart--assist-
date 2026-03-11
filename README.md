<!DOCTYPE html>
<html>
<head>
<title>Care Support Website</title>

<style>

body{
font-family:Arial;
text-align:center;
background:#f2f2f2;
}

h1{
color:green;
}

button{
margin:6px;
padding:10px 18px;
background:green;
color:white;
border:none;
border-radius:6px;
font-size:15px;
}

input{
padding:6px;
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
<button onclick="startVoice()">🎤 Voice</button>
<button onclick="sos()">🚨 SOS</button>

<div id="content" class="box"></div>

<script>

/* STORAGE */

let doctors = JSON.parse(localStorage.getItem("doctors")) || [];
let family = JSON.parse(localStorage.getItem("family")) || [];
let emergency = JSON.parse(localStorage.getItem("emergency")) || [];

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

const speech = new SpeechSynthesisUtterance(
"Welcome to Care Support Website"
);

speechSynthesis.speak(speech);

}

/* CONTACT SYSTEM */

function showContacts(){

let doctorHTML="";
doctors.forEach((n,i)=>{
doctorHTML+=`
<p>${n}
<a href="tel:${n}"><button>Call</button></a>
<button onclick="deleteDoctor(${i})">Delete</button>
</p>
`;
});

let familyHTML="";
family.forEach((n,i)=>{
familyHTML+=`
<p>${n}
<a href="tel:${n}"><button>Call</button></a>
<button onclick="deleteFamily(${i})">Delete</button>
</p>
`;
});

let emergencyHTML="";
emergency.forEach((n,i)=>{
emergencyHTML+=`
<p>${n}
<a href="tel:${n}"><button>Call</button></a>
<button onclick="deleteEmergency(${i})">Delete</button>
</p>
`;
});

document.getElementById("content").innerHTML=
`
<h2>Doctor Numbers</h2>

<input id="doctorInput" placeholder="Enter doctor number">
<button onclick="addDoctor()">Add</button>

${doctorHTML}

<hr>

<h2>Family Numbers</h2>

<input id="familyInput" placeholder="Enter family number">
<button onclick="addFamily()">Add</button>

${familyHTML}

<hr>

<h2>Emergency Numbers</h2>

<input id="emergencyInput" placeholder="Enter emergency number">
<button onclick="addEmergency()">Add</button>

${emergencyHTML}
`;

}

/* ADD */

function addDoctor(){

let num=document.getElementById("doctorInput").value;

if(num){
doctors.push(num);
localStorage.setItem("doctors",JSON.stringify(doctors));
showContacts();
}

}

function addFamily(){

let num=document.getElementById("familyInput").value;

if(num){
family.push(num);
localStorage.setItem("family",JSON.stringify(family));
showContacts();
}

}

function addEmergency(){

let num=document.getElementById("emergencyInput").value;

if(num){
emergency.push(num);
localStorage.setItem("emergency",JSON.stringify(emergency));
showContacts();
}

}

/* DELETE */

function deleteDoctor(i){

doctors.splice(i,1);
localStorage.setItem("doctors",JSON.stringify(doctors));
showContacts();

}

function deleteFamily(i){

family.splice(i,1);
localStorage.setItem("family",JSON.stringify(family));
showContacts();

}

function deleteEmergency(i){

emergency.splice(i,1);
localStorage.setItem("emergency",JSON.stringify(emergency));
showContacts();

}

/* VOICE COMMAND */

function startVoice(){

const recognition = new webkitSpeechRecognition();

recognition.onresult = function(event){

let text = event.results[0][0].transcript.toLowerCase();

if(text.includes("doctor") && doctors.length>0){
window.location.href="tel:"+doctors[0];
}

if(text.includes("family") && family.length>0){
window.location.href="tel:"+family[0];
}

if(text.includes("emergency") && emergency.length>0){
window.location.href="tel:"+emergency[0];
}

};

recognition.start();

}

/* SOS */

function sos(){

if(doctors.length>0){
window.location.href="tel:"+doctors[0];
}

setTimeout(()=>{
if(family.length>0){
window.location.href="tel:"+family[0];
}
},4000);

}

/* GAMES */

function showGames(){

document.getElementById("content").innerHTML=
`
<h2>Games</h2>

<button onclick="game1()">Guess Game</button>
<button onclick="game2()">Math Game</button>
<button onclick="game3()">Color Game</button>
<button onclick="game4()">Click Speed</button>

<div id="gameArea"></div>
`;

}

/* GAME 1 */

let random=Math.floor(Math.random()*5)+1;

function game1(){

document.getElementById("gameArea").innerHTML=
`
<h3>Guess Number</h3>

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

/* GAME 2 */

function game2(){

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

/* GAME 3 */

function game3(){

document.getElementById("gameArea").innerHTML=
`
<h3>Color Game</h3>

<p>What color is the sky?</p>

<button onclick="color('blue')">Blue</button>
<button onclick="color('green')">Green</button>

<p id="colorResult"></p>
`;

}

function color(c){

if(c=="blue")
document.getElementById("colorResult").innerHTML="Correct!";
else
document.getElementById("colorResult").innerHTML="Wrong!";

}

/* GAME 4 */

let clicks=0;

function game4(){

clicks=0;

document.getElementById("gameArea").innerHTML=
`
<h3>Click Speed Game</h3>

<button onclick="count()">Click Fast</button>

<p id="clickResult">Clicks: 0</p>
`;

}

function count(){

clicks++;

document.getElementById("clickResult").innerHTML="Clicks: "+clicks;

}

/* START */

showHome();

</script>

</body>
</html>
