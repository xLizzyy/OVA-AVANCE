<template>
    <!-- Contenedor Principal -->
    <div id="contenidoPrincipal">
      <!-- Cabezote -->
      <div class="header"> 
        <h1>ENFOQUES DE INVESTIGACIÓN</h1> 
        <nav> 
          <ul class="menu"> 
            <li><a href=""> Guías </a></li>
            <li><a href="" id="botonActividades"> Actividades </a></li>
            <li><a href="">Enfoques </a></li>
            <li><a href=""> Evaluación </a></li>
            <li><a href=""> Créditos </a></li>
          </ul>  
        </nav>
      </div>
  
      <!-- Contenido debajo del cabezote -->
      <div class="main-content">
        <!-- Aquí irá todo el contenido de la página después del cabezote -->
        <p>Bienvenido al contenido de Enfoques de Investigación.</p>
      </div>
    </div>
  </template>
  <style>
  /* Variables globales */
  :root { 
    --primary-color: #1a237e; /* azul oscuro */
    --secondary-color: #303f9f; /* azul más claro */
    --accent-color: #7986cb; /* azul pastel */
    --background-color: #f5f6fa; /* gris claro */
  }
  
  /* Estilos generales */
  body {
    background-color: var(--background-color);
    font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
    margin: 0;
    padding: 0;
  }
  
  /* Contenedor principal */
  #contenidoPrincipal {
    margin: 0;
    padding: 0;
    width: 100%;
  }
  
  /* Cabezote */
  .header {
    background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
    padding: 1.5rem 0;
    box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    width: 100%;
    position: fixed; /* Hace que el cabezote quede fijo arriba */
    top: 0;
    left: 0;
    z-index: 1000;
  }
  
  .header h1 {
    margin: 0;
    color: rgb(255, 255, 255);
    font-size: 2rem;
    font-weight: 600;
    text-align: center;
    top: 0;
  }
  
  /* Menú */
  .menu {
    background: rgba(255,255,255,0.1);
    border-radius: 50px;
    padding: 0.5rem;
    margin: 1rem auto;
    list-style: none;
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    max-width: 1304px;
    width: 90%;
  }
  
  .menu li {
    margin: 0 0.5rem;
  }
  
  .menu a {
    color: rgb(255, 255, 255);
    padding: 0.5rem 1.5rem;
    border-radius: 25px;
    transition: all 0.3s ease;
    text-decoration: none;
    display: inline-flex;
    align-items: center;
    gap: 0.3rem;
  }
  
  .menu a:hover {
    background: white;
    color: var(--primary-color);
  }
  
  .menu i {
    margin-right: 0.3rem;
  }
  
  /* Contenido debajo del cabezote */
  .main-content {
    max-width: 1200px;
    margin: 0 auto;
    padding: 150px 20px 40px 20px; /* padding-top grande para que no lo tape el cabezote */
    display: block;
  }
  </style>