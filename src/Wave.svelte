<script>
    import { onMount, onDestroy } from 'svelte';

    let canvas;
    let context;
    let width;
    let height;
    let animationId;
    let offset = 0;
    let frameCount = 0;

    // Valores iniciales para la frecuencia y la amplitud
    let frequency = 0.5;
    let amplitude = 1;

    // Función para generar un array de valores de seno
    function generateSineValues(length, frequency, amplitude) {
        const values = [];
        for (let i = 0; i < length; i++) {
            const angle = (i * 2 * Math.PI * frequency) / length;
            values.push(amplitude * Math.sin(angle));
        }
        return values;
    }

    let values = generateSineValues(100, frequency, amplitude); // Generar valores iniciales

    // Función para actualizar los valores de la onda cuando cambian la frecuencia o la amplitud
    function updateWave() {
        values = generateSineValues(100, frequency, amplitude);
        cancelAnimationFrame(animationId);
        drawWave();
    }

    function drawWave() {
        if (!context) return;

        context.clearRect(0, 0, width, height);
        context.beginPath();

        const step = width / values.length;

        for (let i = 0; i < values.length; i++) {
            const x = i * step;
            const y = height / 2 + values[(i + offset) % values.length] * (height / 2);
            if (i === 0) {
                context.moveTo(x, y);
            } else {
                context.lineTo(x, y);
            }
        }

        context.strokeStyle = 'blue';
        context.lineWidth = 2;
        context.stroke();

        frameCount++;
        if (frameCount >= 5) { // Reducir la velocidad de animación
            frameCount = 0;
            offset = (offset + 1) % values.length;
        }

        animationId = requestAnimationFrame(drawWave);
    }

    onMount(() => {
        canvas.width = canvas.clientWidth;
        canvas.height = canvas.clientHeight;
        context = canvas.getContext('2d');
        width = canvas.width;
        height = canvas.height;
        drawWave();
    });

    onDestroy(() => {
        cancelAnimationFrame(animationId);
    });
</script>

<canvas bind:this={canvas}></canvas>

<div>
    <label for="frequency">Frecuencia:</label>
    <input type="range" id="frequency" min="-10" max="10" step="1" bind:value={frequency} on:input={updateWave} />
    <span>{frequency.toFixed(1)}</span>
</div>

<div>
    <label for="amplitude">Amplitud:</label>
    <input type="range" id="amplitude" min="0.01" max="1" step="0.05" bind:value={amplitude} on:input={updateWave} />
    <span>{amplitude.toFixed(1)}</span>
</div>

<style>
    canvas {
        width: 100%;
        height: 400px;
        border: 1px solid black;
    }

    div {
        margin-top: 10px;
    }
</style>
