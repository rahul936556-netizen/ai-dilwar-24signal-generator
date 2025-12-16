<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>AI Dilwar 24 OTC Signal Generator</title>

<style>
*{box-sizing:border-box}
html,body{
  margin:0;
  padding:0;
  width:100%;
  height:100%;
  background:#0f172a;
  font-family:Arial, sans-serif;
  color:#fff;
}
.app{
  min-height:100vh;
  display:flex;
  justify-content:center;
  align-items:center;
}
.card{
  width:100%;
  max-width:600px;
  background:#020617;
  border-radius:16px;
  padding:20px;
  box-shadow:0 0 25px rgba(0,0,0,.6);
}
h1{text-align:center;color:#38bdf8;margin-bottom:10px}
select,button{
  width:100%;
  padding:12px;
  margin-top:8px;
  border:none;
  border-radius:10px;
  font-weight:bold;
}
button{
  background:#38bdf8;
  color:#000;
  cursor:pointer;
}
.row{
  display:flex;
  justify-content:space-between;
  margin:6px 0;
}
.buy{color:#22c55e;font-weight:bold}
.sell{color:#ef4444;font-weight:bold}
.wait{color:#facc15;font-weight:bold}
.note{
  text-align:center;
  font-size:12px;
  color:#94a3b8;
  margin-top:8px;
}
.flex{
  display:flex;
  gap:10px;
}
</style>
</head>

<body>
<div class="app">
<div class="card">

<h1>OTC Signal Panel (1 Minute)</h1>

<!-- OTC MARKET LIST -->
<select id="market">
<option>EUR/USD (OTC)</option>
<option>GBP/USD (OTC)</option>
<option>USD/JPY (OTC)</option>
<option>AUD/USD (OTC)</option>
<option>USD/CAD (OTC)</option>
<option>USD/CHF (OTC)</option>
<option>NZD/USD (OTC)</option>

<option>EUR/JPY (OTC)</option>
<option>GBP/JPY (OTC)</option>
<option>AUD/JPY (OTC)</option>
<option>CAD/JPY (OTC)</option>
<option>CHF/JPY (OTC)</option>
<option>NZD/JPY (OTC)</option>

<option>EUR/GBP (OTC)</option>
<option>EUR/AUD (OTC)</option>
<option>EUR/CAD (OTC)</option>
<option>EUR/CHF (OTC)</option>
<option>EUR/NZD (OTC)</option>

<option>GBP/AUD (OTC)</option>
<option>GBP/CAD (OTC)</option>
<option>GBP/CHF (OTC)</option>
<option>GBP/NZD (OTC)</option>

<option>AUD/CAD (OTC)</option>
<option>AUD/CHF (OTC)</option>
<option>AUD/NZD (OTC)</option>

<option>USD/INR (OTC)</option>
<option>USD/PKR (OTC)</option>
<option>USD/BDT (OTC)</option>
<option>USD/BRL (OTC)</option>
<option>USD/MXN (OTC)</option>
<option>USD/ZAR (OTC)</option>
<option>USD/NGN (OTC)</option>
<option>USD/ARS (OTC)</option>
</select>

<!-- 7 INDICATORS -->
<div class="row"><span>RSI (14)</span><span id="rsi" class="wait">WAIT</span></div>
<div class="row"><span>EMA (9/21)</span><span id="ema" class="wait">WAIT</span></div>
<div class="row"><span>Supertrend</span><span id="super" class="wait">WAIT</span></div>
<div class="row"><span>Stochastic</span><span id="stoch" class="wait">WAIT</span></div>
<div class="row"><span>MACD</span><span id="macd" class="wait">WAIT</span></div>
<div class="row"><span>Bollinger</span><span id="bb" class="wait">WAIT</span></div>
<div class="row"><span>ADX</span><span id="adx" class="wait">WAIT</span></div>

<hr>

<div class="row">
<strong>FINAL SIGNAL</strong>
<strong id="final" class="wait">WAIT</strong>
</div>

<div class="flex">
<button onclick="generateSignal()">GENERATE</button>
<button onclick="resetSignal()">REFRESH</button>
</div>

<button onclick="openFullscreen()">FULL SCREEN</button>

<div class="note">
Time Frame: 1 Minute<br>
Rule: 7 me se minimum 4 indicators same ho tabhi BUY / SELL
</div>

</div>
</div>

<script>
// RANDOM DEMO SIGNAL (real data nahi)
function randomSignal(){
  let r=Math.random();
  if(r>0.66) return "BUY";
  if(r<0.33) return "SELL";
  return "WAIT";
}

function setSignal(id,val){
  let e=document.getElementById(id);
  e.innerText=val;
  e.className = val==="BUY" ? "buy" : val==="SELL" ? "sell" : "wait";
}

// GENERATE SIGNAL (4/7 RULE)
function generateSignal(){
  let data={
    rsi:randomSignal(),
    ema:randomSignal(),
    super:randomSignal(),
    stoch:randomSignal(),
    macd:randomSignal(),
    bb:randomSignal(),
    adx:randomSignal()
  };

  let buy=0, sell=0;

  for(let k in data){
    setSignal(k,data[k]);
    if(data[k]==="BUY") buy++;
    if(data[k]==="SELL") sell++;
  }

  let final="WAIT";
  if(buy>=4) final="BUY";
  else if(sell>=4) final="SELL";

  setSignal("final",final);
}

// RESET
function resetSignal(){
  ["rsi","ema","super","stoch","macd","bb","adx","final"].forEach(id=>{
    document.getElementById(id).innerText="WAIT";
    document.getElementById(id).className="wait";
  });
}

// FULL SCREEN
function openFullscreen(){
  document.documentElement.requestFullscreen();
}

// AUTO RESET EVERY 1 MIN
setInterval(resetSignal,60000);
</script>

</body>
</html>
