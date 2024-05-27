<script>
    import { onMount } from 'svelte';
  
    let radius = 50; // Radio inicial del círculo
    let angularSpeed = 1; // Velocidad angular inicial del círculo
    let rotation = 0; // Estado inicial de la rotación
  
    const rotateCircle = () => {
      rotation += angularSpeed; // Aumentamos la rotación según la velocidad angular
      if (rotation >= 360) rotation -= 360; // Mantenemos la rotación en un rango de 0 a 359 grados
      requestAnimationFrame(rotateCircle); // Pedimos el siguiente frame
    };
  
    onMount(() => {
      rotateCircle();
    });
  </script>
  
  <style>
    .controls {
      display: flex;
      flex-direction: column;
      align-items: center;
      margin-bottom: 20px;
    }
  
    .circle-container {
      position: relative;
      width: 200px;
      height: 200px;
      display: flex;
      align-items: center;
      justify-content: center;
    }
  
    .circle {
      position: absolute;
      border-radius: 50%;
      background-color: lightblue;
      display: flex;
      align-items: center;
      justify-content: center;
    }
  
    .line {
      position: absolute;
      width: 2px;
      height: 50%;
      background-color: red;
      transform-origin: center;
      transform: translateY(-50%);
    }
  </style>
  
  <div class="controls">
    <label>
      Radio:
      <input type="range" min="10" max="100" bind:value={radius} />
      {radius}px
    </label>
    <label>
      Velocidad Angular:
      <input type="range" min="0" max="10" step="0.1" bind:value={angularSpeed} />
      {angularSpeed}deg/frame
    </label>
  </div>
  
  <div class="circle-container">
    <div class="circle" style="width: {radius * 2}px; height: {radius * 2}px; transform: rotate({rotation}deg);">
      <div class="line" style="height: {radius}px;"></div>
      
    </div>
  </div>
  