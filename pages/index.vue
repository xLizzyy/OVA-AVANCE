<template>
  <!-- Página de entrada -->
  <div id="neural-bg"></div>

  <!-- Contenedor exclusivo para el cerebro -->
  <div id="brain-container"></div>

  <!-- Contenedor para el texto y el botón -->
  <div class="container">
      <h1>Explorando los enfoques de investigación</h1>
      <ul>
          <li class="btn-comenzar"><NuxtLink to="/ova/inicio">Comenzar</NuxtLink></li>
      </ul>
  </div>
</template>

<style>
body {
   margin: 0;
   padding: 0;
   font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
   background-color: #000;    
   color: white;
   height: 100vh;
   width: 100vw;
   overflow: hidden;
   display: flex;
   justify-content: center;
   align-items: center;
}

.container {
   text-align: center;
   position: relative;
   z-index: 10;
}

h1 {
   font-size: 3rem;
   position: relative;
   top: 155px;
   text-shadow: 0 0 10px rgba(64, 224, 208, 0.5);
   font-family: 'Jersey 20', sans-serif;
}

/* Estilo para el botón de "Comenzar" */
.btn-comenzar {
   list-style-type: none; /* Quita el punto del li */
   font-family: 'Jersey 20', sans-serif;
   background-color: rgba(64, 224, 208, 0.1); /* Fondo ligeramente visible */
   color: white;
   border: 2px solid #40e0d0; /* Color turquesa */
   padding: 15px 40px;
   height: 40px;
   width: 170px;
   font-size: 2.2rem; /* Tamaño de fuente más grande */
   border-radius: 40px; /* Más redondeado */
   cursor: pointer;
   transition: all 0.4s ease;
   margin: 350px auto 0; /* Mayor espacio superior para moverlo hacia abajo */
   left: -15px;
   display: flex;
   justify-content: center;
   align-items: center;
   text-shadow: 0 0 12px rgba(64, 224, 208, 0.7);
   position: relative;
   overflow: hidden;
   box-shadow: 0 0 10px rgba(64, 224, 208, 0.4); /* Sombra sutil por defecto */
   letter-spacing: 2px; /* Espaciado entre letras */
}

/* Eliminar subrayado en el enlace NuxtLink */
.btn-comenzar a {
   text-decoration: none; /* Elimina el subrayado del enlace */
   color: inherit; /* Asegura que el enlace herede el color del botón */
   display: block;
   width: 100%;
   text-align: center;
   position: relative;
   z-index: 2; /* Asegura que el texto esté por encima de los efectos */
}

/* Efecto hover sobre el botón */
.btn-comenzar:hover {
   background-color: rgba(64, 224, 208, 0.25);
   box-shadow: 0 0 20px rgba(64, 224, 208, 0.8), 0 0 40px rgba(64, 224, 208, 0.3);
   transform: translateY(-3px); /* Ligero movimiento hacia arriba */
   letter-spacing: 3px; /* Aumenta un poco el espaciado al hacer hover */
}

/* Efecto al hacer clic en el botón (ripple effect) */
.btn-comenzar:after {
   content: '';
   position: absolute;
   top: 50%;
   left: 50%;
   width: 5px;
   height: 5px;
   background: rgba(64, 224, 208, 0.8);
   opacity: 0;
   border-radius: 100%;
   transform: scale(1, 1) translate(-50%);
   transform-origin: 50% 50%;
   z-index: 1;
}

/* Efecto adicional de luz en el botón */
.btn-comenzar:before {
   content: '';
   position: absolute;
   top: 0;
   left: -100%;
   width: 100%;
   height: 100%;
   background: linear-gradient(
     90deg, 
     transparent, 
     rgba(64, 224, 208, 0.4), 
     transparent
   );
   z-index: 1;
   transition: all 0.8s;
}

.btn-comenzar:hover:before {
   left: 100%;
}

.btn-comenzar:focus:not(:active)::after {
   animation: ripple 1s ease-out;
}

@keyframes ripple {
   0% {
       transform: scale(0, 0);
       opacity: 1;
   }
   20% {
       transform: scale(25, 25);
       opacity: 1;
   }
   100% {
       opacity: 0;
       transform: scale(40, 40);
   }
}

/* Contenedor exclusivo para el cerebro */
#brain-container {
   position: absolute;
   top: 10px; /* Ajustado hacia arriba */
   left: 50%;
   transform: translateX(-50%);
   width: 600px;
   height: 600px;
   display: flex;
   justify-content: center;
   align-items: center;
   z-index: 0; /* Mantén el cerebro detrás del texto */
}

/* Estilo para el SVG del cerebro */
.brain-svg {
   width: 100%;
   height: auto;
   max-width: 900px;
   max-height: 900px;
   display: block; 
}

/* Estilo para las líneas del cerebro */
.brain-outline {
   transition: all 0.3s ease;
   cursor: pointer;
   filter: drop-shadow(0 0 5px rgba(64, 224, 208, 0.6));
   animation: glow 3s infinite alternate;
}

#brain-container:hover .brain-outline {
   stroke: #00BFFF !important;
   filter: drop-shadow(0 0 12px rgba(0, 191, 255, 0.8)) !important;
}

/* Animación del resplandor en el cerebro */
@keyframes glow {
   0% {
       filter: drop-shadow(0 0 3px rgba(64, 224, 208, 0.6));
   }
   100% {
       filter: drop-shadow(0 0 8px rgba(64, 224, 208, 0.9));
   }
}

/* Animación de pulso en el fondo */
@keyframes pulse {
   0% {
       opacity: 0.3;
   }
   50% {
       opacity: 1;
   }
   100% {
       opacity: 0.3;
   }
}

/* Fondo de redes neuronales */
#neural-bg {
   position: fixed;
   top: 0;
   left: 0;
   width: 100%;
   height: 100%;
   z-index: 1;
   overflow: hidden;
}
</style>


<script setup>
import { onMounted, onBeforeUnmount } from 'vue';

let resizeListener;

onMounted(() => {
 createNeuralBackground();

 const container = document.getElementById('brain-container');
 if (container) {
   const brain = createBrain();
   container.appendChild(brain);
 }

 resizeListener = () => {
   const bg = document.getElementById('neural-bg');
   if (bg) {
     bg.innerHTML = '';
     createNeuralBackground();
   }
 };
 window.addEventListener('resize', resizeListener);
});

onBeforeUnmount(() => {
 if (resizeListener) {
   window.removeEventListener('resize', resizeListener);
 }
});

function createNeuralBackground() {
 const svg = document.createElementNS("http://www.w3.org/2000/svg", "svg");
 const width = window.innerWidth * 1.2;
 const height = window.innerHeight * 1.2;

 svg.setAttribute('viewBox', `0 0 ${width} ${height}`);
 Object.assign(svg.style, {
   width: '100%',
   height: '100%',
   position: 'absolute',
   top: '0',
   left: '0',
 });

 const nodes = [];
 const connections = [];

 const nodeCount = Math.floor((width * height) / 5000);

 for (let i = 0; i < nodeCount; i++) {
   const x = Math.random() * width;
   const y = Math.random() * height;

   const node = document.createElementNS("http://www.w3.org/2000/svg", "circle");
   node.setAttribute('cx', x);
   node.setAttribute('cy', y);
   node.setAttribute('r', 1 + Math.random() * 2);
   node.setAttribute('fill', Math.random() > 0.3 ? 'rgba(64, 224, 208, 0.6)' : 'rgba(255, 255, 255, 0.6)');
   node.style.opacity = 0.2 + Math.random() * 0.4;
   const duration = 2 + Math.random() * 4;
   node.style.animation = `pulse ${duration}s infinite`;

   svg.appendChild(node);
   nodes.push({ node, x, y });
 }

 for (let i = 0; i < nodes.length; i++) {
   const maxConnections = 5 + Math.floor(Math.random() * 5);
   let connectionCount = 0;

   for (let j = 0; j < nodes.length && connectionCount < maxConnections; j++) {
     if (i === j) continue;

     const dist = Math.sqrt(
       Math.pow(nodes[i].x - nodes[j].x, 2) +
       Math.pow(nodes[i].y - nodes[j].y, 2)
     );

     if (dist < 250) {
       const line = document.createElementNS("http://www.w3.org/2000/svg", "line");
       line.setAttribute('x1', nodes[i].x);
       line.setAttribute('y1', nodes[i].y);
       line.setAttribute('x2', nodes[j].x);
       line.setAttribute('y2', nodes[j].y);
       line.setAttribute('stroke', 'rgba(64, 224, 208, 0.15)');
       line.setAttribute('stroke-width', '0.5');
       svg.appendChild(line);

       connectionCount++;

       if (Math.random() > 0.5) {
         const particle = document.createElementNS("http://www.w3.org/2000/svg", "circle");
         particle.setAttribute('r', '1');
         particle.setAttribute('fill', 'rgba(64, 224, 208, 0.8)');
         svg.appendChild(particle);

         connections.push({
           particle,
           node1: nodes[i],
           node2: nodes[j],
           progress: Math.random(),
           speed: 0.005 + Math.random() * 0.01, // 🔥 restauramos velocidad rápida
           direction: Math.random() > 0.5 ? 1 : -1
         });
       }
     }
   }
 }

 function animate() {
   connections.forEach(conn => {
     conn.progress += conn.speed * conn.direction;

     if (conn.progress > 1 || conn.progress < 0) {
       conn.direction *= -1;
     }

     const x = conn.node1.x + (conn.node2.x - conn.node1.x) * conn.progress;
     const y = conn.node1.y + (conn.node2.y - conn.node1.y) * conn.progress;

     conn.particle.setAttribute('cx', x);
     conn.particle.setAttribute('cy', y);
   });

   requestAnimationFrame(animate);
 }

 animate();

 const bg = document.getElementById('neural-bg');
 if (bg) {
   bg.appendChild(svg);
 }
}

function createBrain() {
 const svg = document.createElementNS("http://www.w3.org/2000/svg", "svg");
 svg.setAttribute('viewBox', '0 0 300 300');
 svg.classList.add('brain-svg');

 const brain = document.createElementNS("http://www.w3.org/2000/svg", "g");
 brain.setAttribute('transform', 'translate(1, -10)');

 const paths = [
   "M150,100 C100,50 50,100 50,150 C50,200 100,250 150,250 C200,250 250,200 250,150 C250,100 200,50 150,100 Z",
   "M150,100 C200,50 250,100 250,150 C250,200 200,250 150,250 C100,250 50,200 50,150 C50,100 100,50 150,100 Z",
   "M150,100 L150,250",
   "M120,110 C100,120 90,140 110,160", // ✅ M restaurado
   "M130,130 C110,140 100,160 120,180",
   "M180,110 C200,120 210,140 190,160",
   "M170,130 C190,140 200,160 180,180"
 ];

 paths.forEach(path => {
   const brainPath = document.createElementNS("http://www.w3.org/2000/svg", "path");
   brainPath.setAttribute('d', path);
   brainPath.setAttribute('fill', 'none');
   brainPath.setAttribute('stroke', 'rgba(64, 224, 208, 1)');
   brainPath.setAttribute('stroke-width', '2');
   brainPath.setAttribute('stroke-linecap', 'round');
   brainPath.classList.add('brain-outline');
   brain.appendChild(brainPath);
 });

 svg.appendChild(brain);
 return svg;
}
</script>