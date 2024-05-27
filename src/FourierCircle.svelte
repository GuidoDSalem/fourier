<script>
    import { onMount } from 'svelte';
    
    export let radius;
    export let angularSpeed;
    export let parentRotation = 0;
  
    let rotation = 0;
  
    const rotateCircle = () => {
      rotation += angularSpeed;
      if (rotation >= 360) rotation -= 360;
      requestAnimationFrame(rotateCircle);
    };
  
    onMount(() => {
      rotateCircle();
    });
  </script>
  
  <style>
    .circle-container {
      position: absolute;
      transform-origin: center;
      display: flex;
      align-items: center;
      justify-content: center;
    }
  
    .circle {
      position: absolute;
      border-radius: 50%;
      background-color: rgba(173, 216, 230, 0.5); /* lightblue with opacity */
      display: flex;
      align-items: center;
      justify-content: center;
    }
  
    .line {
      position: absolute;
      width: 2px;
      background-color: red;
      transform-origin: bottom center;
    }
  </style>
  
  <div class="circle-container" style="transform: rotate({parentRotation}deg);">
    <div class="circle" style="width: {radius * 2}px; height: {radius * 2}px; transform: rotate({rotation}deg);">
      <div class="line" style="height: {radius}px;"></div>
      <slot></slot>
    </div>
  </div>
  