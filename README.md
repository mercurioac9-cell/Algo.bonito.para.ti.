<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ramo Emoji con Corazones Iniciales</title>
<style>
body{
    margin:0;
    height:100vh;
    overflow:hidden;
    background: linear-gradient(to bottom, #ffd4a5, #ffb87c);
    font-family: Arial, sans-serif;
    position:relative;
    display:flex;
    justify-content:center;
    align-items:flex-end;
}

/* 🌷 emoji */
#florEmoji{
    font-size:250px; 
    opacity:0;
    transform:translateY(250px);
    transition:3s;
    position:absolute;
    bottom:0;
    text-shadow: 2px 2px 5px #ff9999, -2px -2px 5px #ff66cc, 0 0 15px #ff99ff;
    cursor:default;
}

/* Botón arriba */
.boton{
    position:absolute;
    top:30px;
    left:50%;
    transform:translateX(-50%) scale(0.8);
    padding:12px 25px;
    font-size:22px;
    border:none;
    border-radius:30px;
    background:white;
    color:#ff4d88;
    font-weight:bold;
    cursor:pointer;
    box-shadow:0 5px 15px rgba(0,0,0,0.2);
    opacity:0;
    transition:1s;
}

/* Mensajes */
#mensajeContainer{
    position:absolute;
    top:50%;
    left:50%;
    transform:translate(-50%, -50%) scale(0.8);
    text-align:center;
    color:white;
    opacity:0;
    transition:1.5s;
}

#linea1{
    font-weight:bold;
    font-size:32px;
    margin-bottom:10px;
}

#linea2{
    color:red;
    font-weight:bold;
    font-size:28px;
    margin-bottom:20px;
}

#linea3{
    font-size:22px;
    line-height:1.5;
}

/* Partículas */
.corazon, .estrella, .corazonInicial{
    position:absolute;
    pointer-events:none;
    animation:subir linear forwards;
}

.corazon{
    font-size:24px;
}

.corazonInicial{
    font-size:22px;
    color:#ff99cc;
    animation-duration:6s;
    animation-iteration-count: infinite;
}

.estrella{
    font-size:18px;
    color:yellow;
}

@keyframes subir{
    0%{ transform:translateY(0) scale(1); opacity:1; }
    100%{ transform:translateY(-300px) scale(1.5); opacity:0; }
}
</style>
</head>
<body>

<!-- Flor emoji -->
<div id="florEmoji">🌷</div>

<!-- Botón -->
<button class="boton" id="boton" onclick="mostrarMensaje()">💌 Abrir</button>

<!-- Mensajes -->
<div id="mensajeContainer">
    <div id="linea1">Por si nadie te lo ha dicho hoy.</div>
    <div id="linea2">✨ FELIZ DÍA DE SAN VALENTÍN 🥀</div>
    <div id="linea3"></div>
</div>

<script>
// Animación del emoji subiendo
window.addEventListener('load', ()=>{
    let flor = document.getElementById('florEmoji');
    setTimeout(()=>{
        flor.style.opacity = 1;
        flor.style.transform = 'translateY(0)';
    },500);

    // Mostrar botón arriba después de 3s
    setTimeout(()=>{
        let boton = document.getElementById('boton');
        boton.style.opacity = 1;
        boton.style.transform = 'translateX(-50%) scale(1)';
    },3000);

    // Crear corazones iniciales solo en la primera animación
    for(let i=0;i<15;i++){
        crearCorazonInicial();
    }
});

// Función al tocar el botón
function mostrarMensaje(){
    document.body.style.background = 'linear-gradient(to bottom, #ff9a9e, #fad0c4)';

    // Ocultar flor y botón
    document.getElementById('florEmoji').style.opacity = 0;
    document.getElementById('boton').style.opacity = 0;

    // Remover todos los corazones iniciales 🩷
    document.querySelectorAll('.corazonInicial').forEach(c => c.remove());

    // Mostrar mensaje
    let cont = document.getElementById('mensajeContainer');
    cont.style.opacity = 1;
    cont.style.transform = 'translate(-50%, -50%) scale(1)';

    // Línea 3 letra por letra
    let texto = "Quizás no seré tu 14 de febrero, pero quiero que cuentes conmigo para lo que quieras 🫠";
    let linea3 = document.getElementById('linea3');
    linea3.textContent = '';
    let i = 0;
    let interval = setInterval(()=>{
        linea3.textContent += texto[i];
        i++;
        if(i >= texto.length) clearInterval(interval);
    },50);

    // Crear partículas nuevas solo después de tocar el botón
    for(let j=0;j<50;j++){
        crearParticula();
    }
}

// Crear partículas normales (solo al tocar el botón)
function crearParticula(){
    let tipo = Math.random() < 0.5 ? 'corazon' : 'estrella';
    let p = document.createElement('div');
    p.classList.add(tipo);
    p.style.left = Math.random()*100 + 'vw';
    p.style.top = Math.random()*100 + 'vh';
    if(tipo==='corazon') p.innerHTML = '❤️';
    else p.innerHTML = '⭐';
    p.style.animationDuration = (3 + Math.random()*2) + 's';
    document.body.appendChild(p);
    setTimeout(()=>{ p.remove(); },5000);
}

// Crear corazones iniciales (solo primera animación)
function crearCorazonInicial(){
    let c = document.createElement('div');
    c.classList.add('corazonInicial');
    c.innerHTML = '🩷';
    c.style.left = (window.innerWidth/2 + (Math.random()*200-100)) + 'px';
    c.style.top = (window.innerHeight/2 + (Math.random()*50-25)) + 'px';
    document.body.appendChild(c);
    // Animación infinita simple
    setInterval(()=>{
        c.style.left = (window.innerWidth/2 + (Math.random()*200-100)) + 'px';
        c.style.top = (window.innerHeight/2 + (Math.random()*50-25)) + 'px';
    },6000);
}
</script>

</body>
</html>
