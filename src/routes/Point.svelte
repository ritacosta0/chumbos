<script>
    import { tweened } from "svelte/motion";
    import { onMount } from "svelte";

    export let x;
    export let y;
    export let index;
    export let type;
    export let endingX;
    export let endingY;
    // Duration for the animation (in milliseconds)
    const duration = 10 * index; // 1 second

    // Create tweened functions for x and y coordinates
    const animatedX = tweened(x);
    const animatedY = tweened(y);
    function getRandomNumber(min, max) {
        return Math.floor(Math.random() * (max - min + 1)) + min;
    }

    // Trigger the animation on component mount
    onMount(() => {
        // Animate the x and y coordinates from the initial position (0, 0) to the destination coordinates
        animatedX.set(
            type === "fail"
                ? getRandomNumber(110, endingX / 2 - 10)
                : getRandomNumber(endingX / 2 + 10, endingX - 100),
            {
                duration,
            }
        );
        animatedY.set(y, { duration });
    });

    let status = type === "pass" ? "#118ab2" : "#fb8500";
</script>

<style>
    /* Styles for the moving circle */
    .circle {
        fill: var(--status);
    }
</style>

<!-- SVG circle -->
<circle
    style="--status:{status}"
    class="circle"
    cx={$animatedX}
    cy={$animatedY}
    stroke="white"
    r="5"
    opacity={0.5} />
