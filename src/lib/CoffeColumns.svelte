<script>
  import * as d3 from "d3"

  export let numbers = []

  function alturaColCoffe(n) {
    let scale = d3
      .scaleLinear()
      .domain([0, d3.max(numbers)]) // extent returns [min, max]
      .range([0, 100])
    return scale(n)
  }

</script>


<div class="coffes-container">
  {#each numbers as n}
  <div>
    <div class="column-wrapper">
      <div class="column-coffe" style="height: {alturaColCoffe(n)}%;"></div>
      <img class="coffe" src="./images/coffe-cup-mask.svg" alt="">
    </div>
    <p class="number">{n}</p>
  </div>
  {/each}
</div>

<style>
  .coffes-container {
    display: flex;
  }
  .column-wrapper {
    position: relative;
    width: 160px;
    height: 200px;
    /* background-color: #ccc;
    border: black 1px solid; */
  }
  .column-coffe {
    position: absolute;
    height: 50%;
    left: 10%;
    right: 10%;
    bottom: 0;
    /* width: 100%; */
    background-color: red;
  }
  .coffe {
    position: absolute;
    bottom: -10px;
    width: 100%;
  }
  .number {
    text-align: center;
  }
</style>
