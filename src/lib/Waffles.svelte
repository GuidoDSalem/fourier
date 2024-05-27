<script>
  import * as d3 from "d3"
  export let numbers = []
</script>

<div class="waffles_container">
  {#each numbers as n}

  <div class="waffle_wrapper">
    <div class="waffle">
      {#each d3.range(0, 100) as number}
        {#if number < n}
          <div class="cuad lleno"></div>
        {:else}
          <div class="cuad vacio"></div>
        {/if}
      {/each}
    </div>
    <p class="number">{n}</p>
  </div>

  {/each}
</div>

<style>
  .waffles_container {
    display: flex;
    /* flex-direction: column; */
    align-items: center;
    /* justify-content: center; */
    gap: 10px;
  }

  .waffle {
    display: grid;
    grid-template-columns: repeat(10, 1fr);
    grid-template-rows: repeat(10, 1fr);
    grid-auto-flow: column-reverse;
    transform: rotateX(180deg);
    width: 100%;
    height: 100%;
    gap: 1px;
    /* margin: 10px; */
  }
  .cuad {
    font-size: 5px;
    width: 10px;
    height: 10px;
    /* border: 1px solid black; */
  }
  .vacio {
    background-color: #ddd;
  }
  .lleno {
    background-color: red;
  }
  .number {
    text-align: center;
    margin-top: 10px;
  }
</style>
