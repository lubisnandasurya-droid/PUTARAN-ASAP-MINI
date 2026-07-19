# PUTARAN-ASAP-MINI
<!DOCTYPE html>
<html lang="id">
body{
    margin:0;
    min-height:100vh;
    background-image:url("images/background.jpg");
    background-size:cover;
    background-position:center;
    background-repeat:no-repeat;
    background-attachment:fixed;
}
}
</style>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Spin Nama</title>

<style>
body{
    margin:0;
    background:#222;
    color:white;
    font-family:Arial,Helvetica,sans-serif;
    display:flex;
    justify-content:center;
    align-items:center;
    flex-direction:column;
    min-height:100vh;
}

h1{
    color:#FFD700;
    text-align:center;
}

canvas{
    border:8px solid white;
    border-radius:50%;
    background:white;
}

button{
    margin-top:20px;
    padding:12px 30px;
    font-size:18px;
    cursor:pointer;
    border:none;
    border-radius:8px;
    background:#00b894;
    color:white;
}

button:hover{
    background:#019875;
}

#hasil{
    margin-top:20px;
    font-size:28px;
    font-weight:bold;
}

.arrow{
    width:0;
    height:0;
    border-left:20px solid transparent;
    border-right:20px solid transparent;
    border-top:40px solid red;
    margin-bottom:-8px;
    z-index:10;
}
</style>
</head>
<body>

<h1>🚭 BATAS MEROKOK HANYA 20 MENIT YA ABANG ABANG 🚭</h1>

<div class="arrow"></div>
<canvas id="wheel" width="500" height="500"></canvas>

<button onclick="spin()">🎯 SPIN</button>

<div id="hasil"></div>

<script>

let nama = [
"Agung",
"Kojek",
"Tio",
"Baim",
"Dafa",
"Nanda",
"Aji",
"Roy"
];

const warnaAsli=[
"#ff7675",
"#74b9ff",
"#55efc4",
"#ffeaa7",
"#a29bfe",
"#fd79a8",
"#81ecec",
"#fab1a0"
];

let warna=[...warnaAsli];

const canvas=document.getElementById("wheel");
const ctx=canvas.getContext("2d");

const radius=canvas.width/2;

let angle=0;

function gambar(){

ctx.clearRect(0,0,canvas.width,canvas.height);

if(nama.length==0){

ctx.fillStyle="black";
ctx.font="30px Arial";
ctx.textAlign="center";
ctx.fillText("SELESAI",radius,radius);

return;

}

const arc=(2*Math.PI)/nama.length;

for(let i=0;i<nama.length;i++){

const start=angle+i*arc;

ctx.beginPath();
ctx.moveTo(radius,radius);
ctx.arc(radius,radius,radius,start,start+arc);
ctx.fillStyle=warna[i%warna.length];
ctx.fill();

ctx.save();

ctx.translate(radius,radius);
ctx.rotate(start+arc/2);

ctx.fillStyle="black";
ctx.font="bold 20px Arial";
ctx.textAlign="right";
ctx.fillText(nama[i],radius-20,8);

ctx.restore();

}

}

gambar();

let sedang=false;

function spin(){

if(sedang) return;

if(nama.length==0){

alert("Semua nama sudah terpilih!");

return;

}

sedang=true;

document.getElementById("hasil").innerHTML="";

const menang=Math.floor(Math.random()*nama.length);

const arc=(2*Math.PI)/nama.length;

const target=(Math.PI*1.5)-(menang*arc)-(arc/2);

const putaran=(Math.PI*2*6)+target;

const awal=angle;

const durasi=5000;

let mulai=null;

function animasi(w){

if(!mulai) mulai=w;

let p=(w-mulai)/durasi;

if(p>1)p=1;

let ease=1-Math.pow(1-p,3);

angle=awal+(putaran*ease);

gambar();

if(p<1){

requestAnimationFrame(animasi);

}else{

sedang=false;

let pemenang=nama[menang];

document.getElementById("hasil").innerHTML="🏆 "+pemenang+" Terpilih!";

nama.splice(menang,1);
warna.splice(menang,1);

angle=0;

setTimeout(()=>{
gambar();
},800);

if(nama.length==0){

setTimeout(()=>{
alert("Semua nama sudah mendapatkan giliran.");
},1000);

}

}

}

requestAnimationFrame(animasi);

}

</script>

</body>
</html>
