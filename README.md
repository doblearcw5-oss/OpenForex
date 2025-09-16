<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>OpenForex</title>
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:'Roboto',sans-serif;}
body{background:#f4f6fa;color:#333;}

/* HEADER */
header{background:#0d1b2a;color:white;padding:15px 50px;display:flex;justify-content:space-between;align-items:center;position:sticky;top:0;z-index:1000;}
header h1{font-size:28px;color:#00bfff;}
nav a{color:white;margin-left:25px;text-decoration:none;font-weight:bold;transition:0.3s;}
nav a:hover{color:#00bfff;}

/* HERO */
.hero{background:linear-gradient(rgba(13,27,42,0.85), rgba(13,27,42,0.85)),url('https://images.unsplash.com/photo-1581091215369-c55f1f3c012f?fit=crop&w=1350&q=80') center/cover no-repeat;color:white;text-align:center;padding:120px 20px;}
.hero h2{font-size:50px;margin-bottom:20px;}
.hero p{font-size:20px;margin-bottom:30px;}
.hero button{background:#00bfff;border:none;padding:15px 30px;font-size:18px;color:white;cursor:pointer;border-radius:5px;transition:0.3s;}
.hero button:hover{background:#009acd;}

/* TRADING PANELS */
.trading-container{display:flex;flex-wrap:wrap;justify-content:space-around;padding:50px 20px;}
.chart-panel{background:#fff;padding:20px;border-radius:10px;box-shadow:0 5px 15px rgba(0,0,0,0.1);margin:20px;flex:1 1 500px;position:relative;}
.price-panel{background:#0d1b2a;color:white;padding:20px;border-radius:10px;margin:20px;flex:1 1 300px;text-align:center;transition:0.3s;position:relative;}
.price-panel:hover{transform:translateY(-5px);box-shadow:0 10px 20px rgba(0,0,0,0.2);}
.price-panel h3{margin-bottom:10px;}
.price{font-size:28px;color:#00ffb3;margin-bottom:10px;display:block;}
.btn-trade{background:#00bfff;color:white;padding:8px 15px;margin:5px;border:none;border-radius:5px;cursor:pointer;transition:0.3s;}
.btn-trade:hover{background:#009acd;}
.slider-container{margin-top:15px;text-align:left;}
.slider-container input{width:100%;}

/* FEATURES */
.features{display:flex;justify-content:space-around;flex-wrap:wrap;padding:60px 20px;background-color:#fff;}
.feature-card{background:#f4f6fa;width:300px;margin:20px;padding:30px;border-radius:10px;text-align:center;box-shadow:0 5px 15px rgba(0,0,0,0.1);transition:0.3s;}
.feature-card:hover{transform:translateY(-10px);box-shadow:0 10px 20px rgba(0,0,0,0.2);}
.feature-card h3{margin-bottom:15px;color:#0d1b2a;}
.feature-card p{color:#555;}

/* FOOTER */
footer{background:#0d1b2a;color:white;padding:40px 50px;text-align:center;}
footer p{margin-bottom:10px;}
footer a{color:#00bfff;text-decoration:none;}
footer a:hover{text-decoration:underline;}

@media(max-width:768px){
    .trading-container{flex-direction:column;align-items:center;}
    header{flex-direction:column;gap:15px;}
}
</style>
</head>
<body>

<header>
<h1>OpenForex</h1>
<nav>
<a href="#">Inicio</a>
<a href="#">Mercados</a>
<a href="#">Plataforma</a>
<a href="#">Contacto</a>
</nav>
</header>

<section class="hero">
<h2>Bienvenido a OpenForex</h2>
<p>Tu plataforma de trading confiable y moderna</p>
<button>Comenzar ahora</button>
</section>

<section class="trading-container">
<!-- Chart EUR/USD -->
<div class="chart-panel">
<h3>EUR/USD</h3>
<canvas id="eurusdChart"></canvas>
</div>

<!-- Chart BTC/USD -->
<div class="chart-panel">
<h3>BTC/USD</h3>
<canvas id="btcusdChart"></canvas>
</div>

<!-- Price Panel con sliders -->
<div class="price-panel">
<h3>Precios y Trading</h3>
<span>EUR/USD: <span class="price" id="eurusdPrice">1.1050</span></span>
<span>USD/JPY: <span class="price" id="usdjpyPrice">147.25</span></span>
<span>GBP/USD: <span class="price" id="gbpusdPrice">1.2900</span></span>
<div class="slider-container">
<label>Invertir cantidad:</label>
<input type="range" id="investment" min="100" max="10000" step="100" value="500">
<span id="investmentValue">500 USD</span>
</div>
<div>
<button class="btn-trade" onclick="trade('Comprar')">Comprar</button>
<button class="btn-trade" onclick="trade('Vender')">Vender</button>
</div>
</div>
</section>

<section class="features">
<div class="feature-card">
<h3>Trading en Tiempo Real</h3>
<p>Accede a los mercados con información actualizada y operaciones rápidas.</p>
</div>
<div class="feature-card">
<h3>Seguridad Avanzada</h3>
<p>Protegemos tus fondos y datos con tecnología de última generación.</p>
</div>
<div class="feature-card">
<h3>Plataforma Intuitiva</h3>
<p>Diseño sencillo y herramientas poderosas para traders de todos los niveles.</p>
</div>
</section>

<footer>
<p>© 2025 OpenForex. Todos los derechos reservados.</p>
<p><a href="#">Política de privacidad</a> | <a href="#">Términos y condiciones</a></p>
</footer>

<script>
// Función de alerta de trading simulada
function trade(type){
    const amount = document.getElementById('investment').value;
    alert(type + ' ejecutado por ' + amount + ' USD');
}

// Slider dinámico
const slider = document.getElementById('investment');
const sliderValue = document.getElementById('investmentValue');
slider.addEventListener('input',()=>{sliderValue.textContent = slider.value + ' USD';});

// Precios dinámicos cada segundo
function updatePrices(){
    document.getElementById('eurusdPrice').textContent = (1.10 + Math.random()*0.01).toFixed(4);
    document.getElementById('usdjpyPrice').textContent = (147 + Math.random()*0.5).toFixed(2);
    document.getElementById('gbpusdPrice').textContent = (1.28 + Math.random()*0.02).toFixed(4);
}
setInterval(updatePrices,1000);

// Charts dinámicos
function generateData(base,min,max){return Array.from({length:20},()=>base+Math.random()*(max-min)+min);}
const eurusdCtx = document.getElementById('eurusdChart').getContext('2d');
const btcusdCtx = document.getElementById('btcusdChart').getContext('2d');

const eurusdChart = new Chart(eurusdCtx,{
type:'line',
data:{labels:Array.from({length:20},(_,i)=>i),datasets:[{label:'EUR/USD',data:generateData(1.10,0,0.01),borderColor:'#00bfff',backgroundColor:'rgba(0,191,255,0.2)',fill:true,tension:0.3}]},
options:{responsive:true,plugins:{legend:{display:false}},scales:{x:{display:false}}}
});

const btcusdChart = new Chart(btcusdCtx,{
type:'line',
data:{labels:Array.from({length:20},(_,i)=>i),datasets:[{label:'BTC/USD',data:generateData(40000,0,1000),borderColor:'#ff9900',backgroundColor:'rgba(255,153,0,0.2)',fill:true,tension:0.3}]},
options:{responsive:true,plugins:{legend:{display:false}},scales:{x:{display:false}}}
});

// Actualización de charts cada segundo
setInterval(()=>{
    eurusdChart.data.datasets[0].data.push(1.10 + Math.random()*0.01);
    eurusdChart.data.datasets[0].data.shift();
    eurusdChart.update();

    btcusdChart.data.datasets[0].data.push(40000 + Math.random()*1000);
    btcusdChart.data.datasets[0].data.shift();
    btcusdChart.update();
},1000);
</script>

</body>
</html># OpenForex
OpenForex 
