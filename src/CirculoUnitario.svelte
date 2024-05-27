<script>

 let k = 0;
 let radius = 100;

 const posX = (t) => {
    // deg to rad
     return Math.cos(t*(Math.PI/180));
 }

    const posY = (t) => {
        return Math.sin(t*(Math.PI/180));
    }

</script>

<div class="container">

    <div class="line"></div>
    <div class="line" style="transform: rotate(90deg);"></div>
    <div class="point" style="transform: translate({1000*posX(k)}%,{(-1)*1000*posY(k)}%)"></div>

</div>

<label>
    k:
    <input type="range" min="0" max="720" bind:value={k} />
    {k}
</label>
<style>

    .point {
        position: absolute;
        width: 25px;
        height: 25px;
        background-color: rgb(254, 0, 0);
        border-radius: 50%;
        
    }
    .line {
        position: absolute;
        width: 2px;
        height: 100%;
        background-color: rgb(0, 0, 0);
        transform-origin: center;
    }

    .container {
        position: relative;
        width: 100%;
        height: 100vh;
        display: flex;
        align-items: center;
        justify-content: center;
    }

</style>