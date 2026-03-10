<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Game Store</title>

<style>

body{
font-family:Arial;
margin:0;
background:#f1f5f9;
transition:0.3s;
}

header{
background:#34a853;
color:white;
padding:15px;
display:flex;
justify-content:space-between;
align-items:center;
}

#search{
padding:10px;
border-radius:6px;
border:none;
width:60%;
}

button{
padding:8px 12px;
border:none;
border-radius:6px;
cursor:pointer;
}

.grid{
display:grid;
grid-template-columns:repeat(2,1fr);
gap:15px;
padding:15px;
}

.app{
background:white;
padding:10px;
border-radius:10px;
text-align:center;
box-shadow:0 2px 6px rgba(0,0,0,0.2);
}

.app img{
width:70px;
height:70px;
}

.estrelas span{
font-size:20px;
cursor:pointer;
color:#ccc;
}

.estrelas .ativo{
color:gold;
}

.dark{
background:#121212;
color:white;
}

.dark .app{
background:#1e1e1e;
}

</style>

</head>

<body>

<header>

<h2>🎮 Game Store</h2>

<input id="search" placeholder="🔎 Buscar jogo..." onkeyup="buscar()">

<button onclick="modo()">🌙</button>

</header>

<div class="grid" id="loja"></div>

<script>

let jogos=[

{
nome:"Subway Surfers",
icone:"https://play-lh.googleusercontent.com/I6k8G6M3D8QX0iMHDLecxB2S98RMyCV2wAPOQgpdnXl16rDpD6PE_P24kTx5cDIe8JDf",
link:"https://play.google.com/store/apps/details?id=com.kiloo.subwaysurf"
},

{
nome:"Free Fire",
icone:"https://play-lh.googleusercontent.com/8o6W0C5XbkNvVKgfHBlC9ZwTe74MkRUYw35vj0IadB1iKsFcEYJIyaKOA1NVuMcZpNig",
link:"https://play.google.com/store/apps/details?id=com.dts.freefireth"
},

{
nome:"Minecraft",
icone:"https://play-lh.googleusercontent.com/7QyH3rroWAtxEvsC0BpvyOukgqS0bkkCm1cW0XkyR3O6-hwxKF1u9IiiaTZGi99Z0eK6",
link:"https://play.google.com/store/apps/details?id=com.mojang.minecraftpe"
},

{
nome:"Roblox",
icone:"https://play-lh.googleusercontent.com/9W7HQwZ0pniS3pSke1Mt2rt7NmBGG99nmCaTKtyfPBkO5RAwOB1p5MNDoAuCEi0aKBsl",
link:"https://play.google.com/store/apps/details?id=com.roblox.client"
},

{
nome:"Clash Royale",
icone:"https://play-lh.googleusercontent.com/7eM5BXAvzkdxl3pNGdisz8Iky3Uczdlz7YT1DoP70uQgmO6ijLJMEVN6a_BE5R16vuMJ",
link:"https://play.google.com/store/apps/details?id=com.supercell.clashroyale"
}

]

let loja=document.getElementById("loja")

function mostrar(lista){

loja.innerHTML=""

lista.forEach((jogo,i)=>{

let downloads=localStorage.getItem("down"+i)||0
let nota=localStorage.getItem("rate"+i)||0

let div=document.createElement("div")
div.className="app"

div.innerHTML=`

<img src="${jogo.icone}">

<h4>${jogo.nome}</h4>

<div class="estrelas">
<span onclick="avaliar(${i},1)">★</span>
<span onclick="avaliar(${i},2)">★</span>
<span onclick="avaliar(${i},3)">★</span>
<span onclick="avaliar(${i},4)">★</span>
<span onclick="avaliar(${i},5)">★</span>
</div>

<p>⭐ ${nota}</p>

<p>📥 ${downloads} downloads</p>

<button onclick="instalar(${i})">Instalar</button>

`

loja.appendChild(div)

})

}

function avaliar(id,valor){

localStorage.setItem("rate"+id,valor)

mostrar(jogos)

}

function instalar(i){

let d=localStorage.getItem("down"+i)||0
d++

localStorage.setItem("down"+i,d)

window.open(jogos[i].link)

mostrar(jogos)

}

function buscar(){

let texto=document.getElementById("search").value.toLowerCase()

let filtrado=jogos.filter(j=>j.nome.toLowerCase().includes(texto))

mostrar(filtrado)

}

function modo(){

document.body.classList.toggle("dark")

}

mostrar(jogos)

</script>

</body>
</html>
