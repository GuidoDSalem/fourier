<script>
  import * as d3 from "d3"
  import Waffles from "./lib/Waffles.svelte"
  import IrregularPath from "./lib/IrregularPath.svelte"
  import CoffeColumns from "./lib/CoffeColumns.svelte"
  import Donas from "./lib/Donas.svelte"
  import Circulo from "./Circulo.svelte"
  import FourierCircle from "./FourierCircle.svelte"
  import FourierSerie from "./FourierSeries.svelte"
  import FourierSeries from "./FourierSeries.svelte";
  import CirculoUnitario from "./CirculoUnitario.svelte"
  import Wave from "./Wave.svelte"

  let numbers = [5, 18, 29, 75, 100]
  let numbersDivided5 = numbers.map(n => Math.floor(n / 5))

  // const waveArray = Array.from({ length: 100 }, () =>
  //   Math.sin(Math.random() * 2 * Math.PI)
  // );
  // const values = Array.from({ length: 100 }, () =>
  //   Math.sin(Math.sin() * 2 * Math.PI)
  // );

</script>

<main>
  <h1>Series de Fourier</h1>
  <Circulo />
  <CirculoUnitario />

  <h1>Onda Animada</h1>
  <!-- <Wave {values} speed={5} /> -->
  <Wave />
  <Wave />
  <Wave />

  <h1>Visualización de la Serie de Fourier</h1>
  <FourierSeries />

</main>

<style>

  .test{
    border-radius: 50%;
    background-color: aqua;

    height: 100px;
    width: 100px;


  }

  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    /* height: 100vh; */
  }

  h1 {
    margin-bottom: 20px;
  }
</style>
