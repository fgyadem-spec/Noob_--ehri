
<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Noob Şehri</title>
<style>
*{box-sizing:border-box}
body{margin:0;background:#17202a;color:white;font-family:Arial;text-align:center}
header{background:#111827;padding:12px}
h1{margin:4px;color:#ffe66d}
#stats{display:flex;justify-content:space-around;gap:5px;flex-wrap:wrap;margin:10px}
#game{position:relative;width:100%;height:55vh;min-height:320px;max-height:520px;overflow:hidden;background:#70bd61}
#road{position:absolute;left:22%;width:56%;height:100%;background:#454b53;border-left:5px solid #eee;border-right:5px solid #eee}
.line{position:absolute;left:49%;width:3px;height:45px;background:#fff}
.building{position:absolute;width:15%;height:90px;background:#d8894a;border:3px solid #8b5a36}
.b2{background:#8d9fc3}.b3{background:#c4b17a}
#car{position:absolute;left:43%;bottom:45px;width:14%;min-width:42px;height:65px;background:#ffcf33;border:4px solid #fff;border-radius:12px;z-index:3;transition:left .08s}
#car:before,#car:after{content:"";position:absolute;background:#222;width:8px;height:15px;top:10px}
#car:before{left:-7px}#car:after{right:-7px}
#car span{display:block;background:#8ee8ff;height:18px;margin:8px 3px;border-radius:4px}
#message{padding:8px;color:#ffe66d;font-weight:bold}
button{border:0;border-radius:12px;padding:13px 15px;font-size:16px;font-weight:bold;background:#ffe66d;color:#17202a;margin:4px;touch-action:manipulation}
.controls{display:flex;justify-content:center;flex-wrap:wrap}
.panel{padding:10px;background:#253244;margin:10px;border-radius:14px}
input{padding:10px;width:65%;border-radius:8px;border:0}
</style>
</head>
<body>
<header>
<h1>🏙️ NOOB ŞEHRİ 🚗</h1>
<div>Şehrin kralı olmaya hazır mısın?</div>
</header>
<div id="stats">
<div>💰 Para: <b id="money">0</b>₺</div>
<div>🚘 Araba: <b id="carname">Noob Arabası</b></div>
<div>⭐ Seviye: <b id="level">1</b></div>
</div>

<div id="game">
<div id="road"></div>
<div class="building" style="left:3%;top:8%"></div>
<div class="building b2" style="left:3%;top:42%;height:105px"></div>
<div class="building b3" style="right:3%;top:15%;height:110px"></div>
<div class="building b2" style="right:3%;top:58%;height:95px"></div>
<div class="line" style="top:0"></div>
<div class="line" style="top:25%"></div>
<div class="line" style="top:50%"></div>
<div class="line" style="top:75%"></div>
<div id="car"><span></span></div>
</div>
<div id="message">Noob Şehri'ne hoş geldin!</div>

<div class="controls">
<button onclick="move(-1)">⬅️ SOL</button>
<button onclick="earn()">💰 PARA KAZAN</button>
<button onclick="move(1)">SAĞ ➡️</button>
</div>
<div class="controls">
<button onclick="drive()">🚗 SÜR</button>
<button onclick="horn()">📢 KORNA</button>
<button onclick="buy()">🏎️ ARABA AL (100₺)</button>
</div>

<div class="panel">
<h3>👥 Arkadaş Odası (Demo)</h3>
<input id="room" placeholder="Oda adı yaz">
<button onclick="joinRoom()">Odaya Gir</button>
<div id="roommsg">Henüz bir oda seçilmedi.</div>
<small>Bu sürümde oda ekranı demo; arkadaşlarla gerçek zamanlı oyun için sunucu gerekir.</small>
</div>

<script>
let money=0,level=1,x=43,speed=0,carIndex=0;
const cars=[
{name:"Noob Arabası",color:"#ffcf33",price:0},
{name:"Mavi Yarışçı",color:"#28a9ff",price:100},
{name:"Süper Araba",color:"#ff3b55",price:250},
{name:"Galaksi Arabası",color:"#bd65ff",price:500}
];
const car=document.getElementById("car");
function update(){
 document.getElementById("money").textContent=money;
 document.getElementById("level").textContent=level;
 document.getElementById("carname").textContent=cars[carIndex].name;
 car.style.left=x+"%";
 car.style.background=cars[carIndex].color;
}
function move(d){
 x=Math.max(24,Math.min(62,x+d*5));
 update();
 document.getElementById("message").textContent=d<0?"Sola döndün!":"Sağa döndün!";
}
function earn(){
 money+=10;
 level=Math.floor(money/100)+1;
 update();
 document.getElementById("message").textContent="+10₺ kazandın!";
}
function drive(){
 speed++;
 earn();
 document.getElementById("message").textContent="🚗 Vııın! Şehirde tur attın! +10₺";
}
function horn(){
 document.getElementById("message").textContent="📢 BİİİİP! Noob geliyor!";
}
function buy(){
 let next=carIndex+1;
 if(next>=cars.length){
  document.getElementById("message").textContent="Bütün arabalar sende! 🏆";
  return;
 }
 if(money<cars[next].price){
  document.getElementById("message").textContent="Yeterli para yok! Para kazan.";
  return;
 }
 money-=cars[next].price;
 carIndex=next;
 update();
 document.getElementById("message").textContent="Yeni araban hayırlı olsun! 🏎️";
}
function joinRoom(){
 let name=document.getElementById("room").value.trim();
 document.getElementById("roommsg").textContent=name?
 "🏙️ '"+name+"' odası seçildi! (Şimdilik demo)":
 "Önce bir oda adı yaz!";
}
update();
</script>
</body>
</html>
