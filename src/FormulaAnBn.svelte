<script lang="ts">
    import * as d3 from 'd3';
    import { onMount } from 'svelte';
  
    let L = 2; // Valor inicial de L
    let datos = []; // Almacena los datos del gráfico
    let svg; // Referencia al SVG
    let an = 1  
    let bn = 1
  
    // Función para calcular la serie de Fourier
    function fourierSeries(x, L, an, bn) {
      const nMax = 10; // Número máximo de términos en la serie (ajústalo según tus necesidades)
      let result = 0;
  
      for (let n = 1; n <= nMax; n++) {
        result += an * Math.cos((n * Math.PI * x) / L) + bn * Math.sin((n * Math.PI * x) / L);
      }
  
      return 0.5 * result;
    }
  
    // Función para actualizar el gráfico cuando cambie L
    $: actualizarGrafico = () => {
      datos = [];
      for (let x = 0; x <= 10; x += 0.1) {
        const y = fourierSeries(x, L,an , bn);
        datos.push([x, y]);
      }
      actualizarSVG();
    };
  
    function actualizarSVG() {
      if (svg) {
        // Si el SVG ya existe, elimínalo
        svg.remove();
      }
  
      // Crea un nuevo SVG
      svg = d3.select("#grafico1")
        .append("svg")
        .attr("width", 500)
        .attr("height", 300);
  
      const escalaX = d3.scaleLinear()
        .domain([0, 10])
        .range([0, 500]);
  
      const escalaY = d3.scaleLinear()
        .domain([-10, 10])
        .range([300, 0]);
  
      const linea = d3.line()
        .x(d => escalaX(d[0]))
        .y(d => escalaY(d[1]));
  
      svg.append("path")
        .datum(datos)
        .attr("d", linea)
        .style("stroke", "blue")
        .style("stroke-width", 2)
        .attr("filter", "none")
        .attr("fill", "none");
    }
  
    // Llama a la función cuando cambie el valor de L
    $: actualizarGrafico();
    onMount(() => {
      actualizarGrafico();
    });
  </script>
  
  <div id="grafico1" />
  <input type="range" min="0" max="2" step="0.01" bind:value={an} on:input={actualizarGrafico} />
  <input type="range" min="0" max="2" step="0.01" bind:value={bn} on:input={actualizarGrafico} />

  <p>An: {an}, Bn: {bn}</p>
  
  
  <style>
   #grafico1 {
    width: 100%;
    height: 400px;
    border: 1px solid black;
    align-items: center;
    display: flex;
    justify-content: center;
  }
  
  svg {
    display:block;
  }
  </style>
  