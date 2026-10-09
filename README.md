# slot-naga-emas.
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Slot Naga Emas</title>
<style>
*{box-sizing:border-box}
body{
  margin:0;
  font-family:Arial,sans-serif;
  background:linear-gradient(160deg,#100d18,#301020,#080808);
  color:white;
  text-align:center;
}
header{
  padding:22px 10px;
  background:#111;
  border-bottom:2px solid gold;
}
h1{color:gold;margin:0;font-size:27px}
main{padding:20px 12px;max-width:440px;margin:auto}
.card{
  background:#1b1720;
  border:1px solid #72551a;
  border-radius:18px;
  padding:20px 12px;
  margin-bottom:16px;
  box-shadow:0 5px 20px #0008;
}
.balance{color:#ffd700;font-size:23px;font-weight:bold}
.reels{display:flex;justify-content:center;gap:8px;margin:22px 0}
.reel{
  background:#fff8e7;
  color:#171017;
  width:88px;height:90px;
  display:flex;align-items:center;justify-content:center;
  font-size:43px;border-radius:12px;
  border:3px solid gold;
}
button{
  border:0;border-radius:12px;
  padding:14px 22px;font-size:17px;
  font-weight:bold;cursor:pointer;
}
.spin{background:linear-gradient(#ffe86b,#ff9c00);color:#281500;width:100%}
.secondary{background:#35303c;color:white;margin:5px}
button:disabled{opacity:.5}
#message{min-height:26px;color:#ffe28a;margin-top:15px}
.games{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.game{background:#302433;border-radius:12px;padding:15px 5px}
footer{color:#aaa;font-size:12px;padding:20px}
</style>
</head>
<body>
<header>
  <h1>🐉 SLOT NAGA EMAS</h1>
  <p>GAME KOIN VIRTUAL</p>
</header>

<main>
  <section class="card">
    <p>💰 SALDO KOIN VIRTUAL</p>
    <div class="balance"><span id="balance">1000</span> 🪙</div>
    <p>Gunakan koin virtual untuk bermain.</p>
  </section>

  <section class="card">
    <h2>🎰 Naga Fortune</h2>
    <div class="reels">
      <div class="reel" id="r1">🐉</div>
      <div class="reel" id="r2">💎</div>
      <div class="reel" id="r3">👑</div>
    </div>
    <p>Biaya bermain: 10 koin virtual</p>
    <button class="spin" id="spin" onclick="play()">SPIN SEKARANG</button>
    <div id="message">Tekan SPIN untuk bermain!</div>
  </section>

  <section class="card">
    <h3>🎮 PILIH PERMAINAN</h3>
    <div class="games">
      <div class="game">🐉<br>Naga Fortune</div>
      <div class="game">💎<br>Permata Emas</div>
      <div class="game">👑<br>Raja Emas</div>
      <div class="game">🧧<br>Hoki Merah</div>
    </div>
  </section>

  <section class="card">
    <h3>🎁 BONUS KOIN</h3>
    <p>Klaim bonus koin virtual untuk mencoba permainan.</p>
    <button class="secondary" onclick="bonus()">KLAIM BONUS</button>
    <p id="bonusmsg"></p>
  </section>
</main>

<footer>
  Game hiburan dengan koin virtual. Tidak menggunakan uang asli.
</footer>

<script>
let balance = 1000;
let bonusClaimed = false;
let playing = false;
const symbols = ["🐉","💎","👑","🔔","🍀","⭐"];

function updateBalance(){
  document.getElementById("balance").textContent=balance;
}

function play(){
  if(playing) return;
  if(balance<10){
    document.getElementById("message").textContent=
      "Koin habis. Klaim bonus virtual untuk melanjutkan.";
    return;
  }

  playing=true;
  const btn=document.getElementById("spin");
  btn.disabled=true;
  balance-=10;
  updateBalance();

  let count=0;
  const reels=[
    document.getElementById("r1"),
    document.getElementById("r2"),
    document.getElementById("r3")
  ];

  const timer=setInterval(()=>{
    reels.forEach(r=>{
      r.textContent=symbols[Math.floor(Math.random()*symbols.length)];
    });
    count++;

    if(count>=12){
      clearInterval(timer);
      const result=reels.map(r=>r.textContent);

      if(result.every(s=>s===result[0])){
        balance+=100;
        document.getElementById("message").textContent=
          "🎉 JACKPOT VIRTUAL! Kamu mendapat 100 koin!";
      }else if(result[0]===result[1]||result[1]===result[2]){
        balance+=20;
        document.getElementById("message").textContent=
          "✨ Dua simbol cocok! Kamu mendapat 20 koin!";
      }else{
        document.getElementById("message").textContent=
          "Coba lagi! Semoga beruntung.";
      }

      updateBalance();
      playing=false;
      btn.disabled=false;
    }
  },100);
}

function bonus(){
  if(bonusClaimed){
    document.getElementById("bonusmsg").textContent=
      "Bonus sudah diklaim pada sesi ini.";
    return;
  }
  balance+=100;
  bonusClaimed=true;
  updateBalance();
  document.getElementById("bonusmsg").textContent=
    "🎁 Berhasil! Kamu mendapat 100 koin virtual.";
}
</script>
</body>
</html>
