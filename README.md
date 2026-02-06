# Top-
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Roses Day Game 🌹</title>

<style>
*{margin:0;padding:0;box-sizing:border-box}
body{
  font-family:Arial,sans-serif;
  background:linear-gradient(135deg,#c41e3a,#ff1744,#ff6b9d);
  min-height:100vh;
  display:flex;
  justify-content:center;
  align-items:center;
  padding:20px;
}
.card{
  background:white;
  max-width:500px;
  width:100%;
  padding:30px;
  border-radius:20px;
  text-align:center;
  box-shadow:0 20px 40px rgba(0,0,0,.3);
}
h1{color:#c41e3a;margin-bottom:8px}
.subtitle{color:#d63447;font-weight:bold;margin-bottom:15px}
.level-indicator{
  background:linear-gradient(135deg,#ff1744,#ff6b9d);
  color:white;
  padding:12px;
  border-radius:12px;
  margin-bottom:15px;
  font-weight:bold;
}
.roses button{
  width:100%;
  padding:14px;
  margin:8px 0;
  font-size:18px;
  border:none;
  border-radius:12px;
  cursor:pointer;
  background:linear-gradient(135deg,#ff1744,#ff6b9d);
  color:white;
  font-weight:bold;
}
.game-section{display:none}
.result{
  background:#fff5f7;
  padding:15px;
  border-radius:12px;
  margin-top:15px;
  border-left:5px solid #c41e3a;
}
.result-title{
  font-size:22px;
  color:#c41e3a;
  font-weight:bold;
  margin-bottom:10px;
}
.result-paragraph{
  background:white;
  padding:12px;
  border-radius:10px;
  margin-top:12px;
  color:#c41e3a;
  font-style:italic;
}
.memory-game{
  display:grid;
  grid-template-columns:repeat(4,1fr);
  gap:10px;
  margin-top:15px;
}
.memory-card{
  aspect-ratio:1;
  border:none;
  border-radius:8px;
  font-size:24px;
  cursor:pointer;
  background:linear-gradient(135deg,#ff6b9d,#ff9fb2);
}
.memory-card.flipped{
  background:white;
  border:2px solid #ff1744;
}
.memory-card.matched{
  background:#c41e3a;
  color:white;
}
.gift-counter{
  margin-top:10px;
  padding:10px;
  background:linear-gradient(135deg,#ff1744,#ff6b9d);
  color:white;
  border-radius:10px;
  font-weight:bold;
}
</style>
</head>

<body>
<div class="card">
  <h1>🌹 Roses Day Mini Game 🌹</h1>
  <div class="subtitle">A Special Gift 💖</div>

  <!-- LEVEL 1 -->
  <div id="welcomeSection">
    <div class="level-indicator">🎯 Level 1: Pick a Rose</div>
    <div class="roses">
      <button onclick="playRose()">🌹 Pick Rose</button>
    </div>
    <div class="gift-counter">💝 Gifts: <span id="giftCount">0</span></div>
  </div>

  <!-- LEVEL 2 -->
  <div id="roseGameSection" class="game-section">
    <div class="level-indicator">🎯 Level 2: Memory Game</div>
    <div id="memoryGame" class="memory-game"></div>

    <div id="memoryResult" class="result" style="display:none"></div>
    <div id="memoryQA" class="result" style="display:none"></div>
  </div>
</div>

<script>
let giftCount = 0;
let cards = ['🌹','🌸','🌼','💐','🌹','🌸','🌼','💐'];
let flipped=[], matched=0, lock=false;

document.getElementById("giftCount").textContent = giftCount;

function playRose(){
  giftCount++;
  document.getElementById("giftCount").textContent = giftCount;
  document.getElementById("welcomeSection").style.display="none";
  document.getElementById("roseGameSection").style.display="block";
  startMemory();
}

function startMemory(){
  cards.sort(()=>Math.random()-0.5);
  let html="";
  cards.forEach((c,i)=>{
    html+=`<button class="memory-card" onclick="flip(${i})" data-i="${i}" data-v="${c}">?</button>`;
  });
  document.getElementById("memoryGame").innerHTML=html;
}

function flip(i){
  if(lock) return;
  let card=document.querySelector(`[data-i="${i}"]`);
  if(flipped.includes(i) || card.classList.contains("matched")) return;

  card.textContent=card.dataset.v;
  card.classList.add("flipped");
  flipped.push(i);

  if(flipped.length===2){
    lock=true;
    setTimeout(check,600);
  }
}

function check(){
  let [a,b]=flipped;
  let ca=document.querySelector(`[data-i="${a}"]`);
  let cb=document.querySelector(`[data-i="${b}"]`);

  if(ca.dataset.v===cb.dataset.v){
    ca.classList.add("matched");
    cb.classList.add("matched");
    matched++;
  }else{
    ca.textContent="?";
    cb.textContent="?";
    ca.classList.remove("flipped");
    cb.classList.remove("flipped");
  }
  flipped=[];
  lock=false;

  if(matched===4){
    giftCount+=2;
    document.getElementById("giftCount").textContent=giftCount;

    document.getElementById("memoryResult").innerHTML=`
      <div class="result-title">🎉 Memory Game Completed 🎉</div>
      <div>You matched all roses 💐</div>
      <div class="gift-counter">💝 Total Gifts: ${giftCount}</div>
    `;
    document.getElementById("memoryResult").style.display="block";

    document.getElementById("memoryQA").innerHTML=`
      <div class="result-title">💭 Just Two Questions 💭</div>
      🌹 <b>Mumma girl ask for rose?</b><br>
      👉 Yes 💖<br><br>
      🌸 <b>U give me any type of rose?</b><br>
      👉 Yes 🌹

      <div class="result-paragraph">
        Try kela tula avdnr ki ny idk but asa wla koni kela nasnr vatte mla 🥹<br>
        manun asa kela 🫶<br><br>
        ata happy rose day butkiiii 💗🌹
      </div>
    `;
    document.getElementById("memoryQA").style.display="block";
  }
}
</script>
</body>
</html>
