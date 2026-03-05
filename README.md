<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Smart Assist</title>

<style>
body{
  margin:0;
  font-family:Arial;
  background:#f2f2f2;
  text-align:center;
}

header{
  background:#075E54;
  color:white;
  padding:20px;
  font-size:22px;
  font-weight:bold;
}

.section{
  padding:20px;
}

button{
  width:90%;
  padding:15px;
  margin:10px;
  font-size:18px;
  border:none;
  border-radius:8px;
  background:#25D366;
  color:white;
}

button:hover{
  background:#128C7E;
}

.gameBox{
  background:white;
  padding:15px;
  margin:15px;
  border-radius:10px;
  box-shadow:0 2px 5px rgba(0,0,0,0.2);
}

input{
  width:85%;
  padding:12px;
  margin:8px;
  font-size:16px;
}
</style>
</head>

<body>

<header>
🧑‍🦯 Smart Assist
</header>

<div class="section">

<h2>📞 Emergency Contacts</h2>

<input id="familyInput" value="9321748592">
<button onclick="callNumber(document.getElementById('familyInput').value)">
Call Family
</button>

<input id="doctorInput" value="8104952319">
<button onclick="callNumber(document.getElementById('doctorInput').value)">
Call Doctor
</button>

<input id="newNumber" placeholder="Add New Contact Number">
<button onclick="addNewContact()">Add & Call</button>

<button onclick="callNumber('112')">
Emergency Call (112)
</button>

<hr>

<h2>🎮 Accessible Games</h2>

<!-- Game 1 Voice Tap -->
<div class="gameBox">
<h3>Voice Tap Game</h3>
<p>Tap screen anywhere 10 times</p>
<p id="tapCount">Taps: 0</p>
<button onclick="resetTap()">Reset</button>
</div>

<!-- Game 2 Memory Voice -->
<div class="gameBox">
<h3>Memory Voice Game</h3>
<button onclick="memoryGame()">Hear Random Number</button>
<p id="memoryText"></p>
</div>

<!-- Game 3 Big Button Game -->
<div class="gameBox">
<h3>Big Button Reaction</h3>
<button onclick="bigButtonGame()" style="height:100px;font-size:24px;">
PRESS ME
</button>
<p id="bigResult"></p>
</div>

</div>

<script>

function speak(text){
  if('speechSynthesis' in window){
    window.speechSynthesis.cancel();
    const speech=new SpeechSynthesisUtterance(text);
    speech.lang="en-US";
    setTimeout(()=>{window.speechSynthesis.speak(speech);},200);
  }
}

function callNumber(num){
  speak("Calling now");
  window.location.href="tel:"+num;
}

function addNewContact(){
  let num=document.getElementById("newNumber").value;
  if(num!=""){
    speak("Calling new number");
    window.location.href="tel:"+num;
  }else{
    speak("Please enter number");
  }
}

let tapCount=0;
document.body.addEventListener("click",function(){
  tapCount++;
  document.getElementById("tapCount").innerText="Taps: "+tapCount;
});

function resetTap(){
  tapCount=0;
  document.getElementById("tapCount").innerText="Taps: 0";
}

function memoryGame(){
  let random=Math.floor(Math.random()*100);
  document.getElementById("memoryText").innerText="Remember this: "+random;
  speak("Remember this number "+random);
}

function bigButtonGame(){
  let time=Math.floor(Math.random()*5)+1;
  document.getElementById("bigResult").innerText=
  "You pressed after "+time+" seconds";
  speak("Good job");
}

</script>

</body>
</html>
