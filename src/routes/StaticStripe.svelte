<script>
    import { tweened } from "svelte/motion";
    import { onMount } from "svelte";

    export let x;
    export let y;
    export let index;
    export let type;
    export let endingX;
    export let endingY;
    export let percentSuccessfulStudents;
    export let step;
    let status = type === "pass" ? "#118ab2" : "#fb8500";
    // Duration for the animation (in milliseconds)
    function getRandomNumber(min, max) {
        return Math.floor(Math.random() * (max - min + 1)) + min;
    }
    const duration = 25 * getRandomNumber(0, 100); // 1 second

    // // Create tweened functions for x and y coordinates
    // const animatedX = tweened(x);
    // const animatedY = tweened(y);

    // // Trigger the animation on component mount
    // onMount(() => {
    //     // Animate the x and y coordinates from the initial position (0, 0) to the destination coordinates
    //     animatedX.set(index === 0 ? 100 : index * (endingX / 100) + 100, {
    //         duration,
    //     });
    //     animatedY.set(y, { duration });
    // });

    $: {
        if (step == 0 || step === undefined) {
            status = "#D3D3D3";
        }
        if (step == 1) {
            status = type === "pass" ? "#118ab2" : "#D3D3D3";
        }
        if (step == 2) {
            status = type !== "pass" ? "#fb8500" : "#D3D3D3";
        }
    }
</script>

<style>
    /* Styles for the moving circle */
    .circle {
        fill: var(--status);
    }
</style>

<!-- SVG circle -->
<rect
    style="--status:{status}"
    class="circle"
    {x}
    {y}
    stroke="white"
    width={endingX / 100}
    height={endingY}
    opacity={0.5} />
