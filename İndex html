
<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
<title>Kare Dünya - Obby</title>
<style>
*{box-sizing:border-box}
body{margin:0;background:#111827;color:white;font-family:Arial;text-align:center}
header{padding:12px;background:#202d42}
h1{margin:5px;color:#7cf7ff}
button,input{font-size:15px;border:0;border-radius:10px;padding:11px;margin:3px}
button{background:#ffe66d;font-weight:bold;color:#202030}
button:active{transform:scale(.96)}
.stats{display:flex;justify-content:space-around;flex-wrap:wrap;padding:8px;gap:5px}
#world{height:48vh;min-height:300px;max-height:480px;position:relative;overflow:hidden;background:linear-gradient(#6cc8ff 0%,#c4f4ff 70%,#79c95b 70%)}
.cloud{position:absolute;font-size:35px}
#platforms{position:absolute;inset:0}
.platform{position:absolute;height:17px;background:#28a66a;border:3px solid #146b45;border-radius:4px}
#lava{position:absolute;left:0;bottom:0;width:100%;height:9%;background:#ff493f}
#player{position:absolute;left:9%;bottom:10%;width:35px;height:48px;z-index:5;transition:left .12s,bottom .12s}
.head{height:20px;width:25px;background:#ffcc91;margin:auto;border:2px solid #7d4e31;border-radius:4px}
.body{height:19px;width:32px;background:#2585ff;margin:auto;border:2px solid #1554a0}
.legs{display:flex;justify-content:center;height:10px}
.legs i{width:12px;background:#25375e;border:1px solid #111;margin:0 2px}
#checkpoint{position:absolute;bottom:10%;left:78%;font-size:30px}
#notice{min-height:28px;padding:7px;color:#ffe66d;font-weight:bold}
.panel{background:#202d42;border-radius:14px;margin:9px;padding:12px}
.grid{display:grid;grid-template-columns:1fr 1fr;gap:5px}
input{width:65%;max-width:220px}
small{color:#cbd5e1}
</style>
</head>
<body>
<header>
<h1>🟦 KARE DÜNYA</h1>
<div>Obby • Avatar • Arkadaşlar</div>
</header>

<div class="stats">
<div>🪙 Coin: <b id="coins">0</b></div>
<div>🏁 Bölüm: <b id="stage">1</b></div>
<div>👤 <b id="skinname">Mavi Noob</b></div>
</div>

<div id="world">
<div class="cloud" style="left:15%;top:8%">☁️</div>
<div class="cloud" style="left:68%;top:15%">☁️</div>
<div id="platforms">
<div class="platform" style="left:0;bottom:10%;width:24%"></div>
<div class="platform" style="left:31%;bottom:24%;width:17%"></div>
<div class="platform" style="left:55%;bottom:39%;width:17%"></div>
<div class="platform" style="left:78%;bottom:10%;width:22%"></div>
<div id="lava"></div>
<div id="checkpoint">🏁</div>
</div>
<div id="player">
<div class="head"></div><div class="body"></div>
<div class="legs"><i></i><i></i></div>
</div>
</div>

<div id="notice">Obby'ye hoş geldin! Platformlara zıpla!</div>

<div class="panel">
<h3>🎮 Karakter Kontrolleri</h3>
<div class="grid">
<button onclick="move(-1)">⬅️ SOL</button>
<button onclick="move(1)">SAĞ ➡️</button>
<button onclick="jump()">⬆️ ZIPLA</button>
<button onclick="reset()">🔄 BAŞTAN</button>
</div>
<p><small>Bu, telefonda dokunarak oynanan basit bir obby prototipidir.</small></p>
</div>

<div class="panel">
<h3>👕 Avatar Mağazası</h3>
<p>Görünüşünü değiştir, coin harca!</p>
<button onclick="buySkin('Mavi Noob','#2585ff',0)">🔵 Mavi - Ücretsiz</button>
<button onclick="buySkin('Kırmızı Noob','#ff4545',25)">🔴 Kırmızı - 25🪙</button>
<button onclick="buySkin('Mor Noob','#b45cff',50)">🟣 Mor - 50🪙</button>
</div>

<div class="panel">
<h3>🪙 Oyun Parası</h3>
<p>Parkuru tamamlayarak coin kazan!</p>
<button onclick="collect()">Coin Ödülü Al (+10)</button>
<p><small>Bu coinler yalnızca bu prototipin oyun içi parasıdır; Robux değildir.</small></p>
</div>

<div class="panel">
<h3>👥 Arkadaş Sistemi</h3>
<input id="friendName" maxlength="20" placeholder="Arkadaş adı">
<button onclick="addFriend()">Arkadaş Ekle</button>
<div id="friends">Henüz arkadaş eklenmedi.</div>
<p><small>Arkadaş listesi bu tarayıcıda demo olarak çalışır. Diğer oyuncularla gerçek bağlantı sağlamaz.</small></p>
</div>

<div class="panel">
<h3>💎 Robux Hakkında</h3>
<p>Bu oyunda gerçek Robux yoktur. Kendi oyun paran ve mağazan bulunur.</p>
</div>

<script>
let x=9,stage=1,coins=0,jumping=false,gotReward=false;
let friends=[];
const player=document.getElementById('player');

function say(t){document.getElementById('notice').textContent=t}
function draw(){
 player.style.left=x+'%';
 document.getElementById('coins').textContent=coins;
 document.getElementById('stage').textContent=stage;
}
function move(d){
 x=Math.max(0,Math.min(90,x+d*6));
 draw();
 if(x>27&&x<48){say('Platforma geldin! Şimdi zıpla!')}
 else if(x>=48&&x<76){say('Güzel gidiyorsun! Bir kez daha zıpla!')}
 else if(x>=76){finish()}
 else{say('İleri git ve engelleri aş!')}
}
function jump(){
 if(jumping)return;
 jumping=true;
 player.style.bottom='32%';
 say('Zıplıyorsun! 🚀');
 setTimeout(()=>{
  player.style.bottom='10%';
  jumping=false;
  if(x>=27&&x<48||x>=48&&x<76){
   say('İyi zıpladın! Bir sonraki platforma ilerle.');
  }else if(x<27){
   say('Bir platforma ulaşmak için daha ileri git.');
  }else if(x>=76){finish()}
 },650);
}
function finish(){
 if(!gotReward){
  gotReward=true;
  coins+=20;
  stage++;
  draw();
  say('🏆 OBBy TAMAMLANDI! +20 coin kazandın!');
  x=9;
  setTimeout(draw,1000);
 }else say('Harikasın! Yeni tur için devam et.');
}
function reset(){
 x=9;gotReward=false;draw();say('Yeni tur başladı! 🏁');
}
function collect(){
 coins+=10;draw();say('+10 oyun coini kazandın! 🪙');
}
function buySkin(name,color,price){
 if(name===document.getElementById('skinname').textContent){
  say('Bu görünüş zaten seçili!');
  return;
 }
 if(coins<price){say('Yeterli coin yok! Obby oyna veya ödül al.');return}
 coins-=price;
 document.querySelector('.body').style.background=color;
 document.getElementById('skinname').textContent=name;
 draw();say(name+' görünüşü seçildi!');
}
function addFriend(){
 const input=document.getElementById('friendName');
 const name=input.value.trim();
 if(!name){say('Önce arkadaş adı yaz!');return}
 if(friends.some(n=>n.toLowerCase()===name.toLowerCase())){
  say('Bu isim listende var!');return
 }
 friends.push(name);
 document.getElementById('friends').textContent='👤 '+friends.join(' • ');
 input.value='';
 say(name+' demo arkadaş listene eklendi!');
}
draw();
</script>
</body>
</html>
