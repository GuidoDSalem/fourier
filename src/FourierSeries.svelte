<script>
  import FourierCircle from './FourierCircle.svelte';

  let numCircles = 5; // Número de círculos
  let baseRadius = 50; // Radio base del primer círculo
  let baseSpeed = 1; // Velocidad angular base del primer círculo

  // Generar datos para los círculos de la serie de Fourier
  let circles = Array.from({ length: numCircles }, (_, i) => {
    const n = i + 1;
    return {
      radius: baseRadius / n,
      speed: baseSpeed * n
    };
  });
</script>

<style>
  .container {
    position: relative;
    width: 100%;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
  }
</style>

<div class="container">
  {#each circles as { radius, speed }, i}
    <FourierCircle
      {radius}
      angularSpeed={speed}
      parentRotation={i === 0 ? 0 : circles[i - 1].speed * 360}
      
    />
  {/each}
</div>
