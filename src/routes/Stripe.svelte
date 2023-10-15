<script>
    import { tweened } from "svelte/motion";
    import { onMount } from "svelte";
    import { tooltip } from "../utils/tooltip.js";

    export let x;
    export let y;
    export let index;
    export let type;
    export let endingX;
    export let endingY;
    export let percentSuccessfulStudents;
    export let step;
    export let type1;
    export let type2;

    // Duration for the animation (in milliseconds)
    function getRandomNumber(min, max) {
        return Math.floor(Math.random() * (max - min + 1)) + min;
    }
    const duration = 25 * getRandomNumber(0, 100); // 1 second

    // Create tweened functions for x and y coordinates
    const animatedX = tweened(x);
    const animatedY = tweened(y);

    const endingArea = ((100 - percentSuccessfulStudents) * endingX) / 100;
    let status = type === "pass" ? "#118ab2" : "#fb8500";

    $: {
        if (step === undefined) {
            onMount(() => {
                // Animate the x and y coordinates from the initial position (0, 0) to the destination coordinates
                animatedX.set(
                    index === 0 ? 100 : index * (endingX / 100) + 100,
                    {
                        duration,
                    }
                );
                animatedY.set(endingY, { duration });
            });
        }
        if (step == 0) {
            status = "#D3D3D3";
            onMount(() => {
                // Animate the x and y coordinates from the initial position (0, 0) to the destination coordinates
                animatedX.set(
                    index === 0 ? 100 : index * (endingX / 100) + 100,
                    {
                        duration,
                    }
                );
                animatedY.set(endingY, { duration });
            });
        }
        if (step == 1) {
            status = type !== "pass" ? "#fb8500" : "#D3D3D3";

            onMount(() => {
                // Animate the x and y coordinates from the initial position (0, 0) to the destination coordinates
                animatedX.set(
                    index === 0 ? 100 : index * (endingX / 100) + 100,
                    {
                        duration,
                    }
                );
                animatedY.set(endingY, { duration });
            });
        }
        if (step == 2) {
            status = type === "pass" ? "#118ab2" : "#D3D3D3";
            onMount(() => {
                // Animate the x and y coordinates from the initial position (0, 0) to the destination coordinates
                animatedX.set(
                    index === 0 ? 100 : index * (endingX / 100) + 100,
                    {
                        duration,
                    }
                );
                animatedY.set(endingY, { duration });
            });
        }
        if (step == 3) {
            status = type === "pass" ? "#cdcdcd" : "#cdcdcd";
            onMount(() => {
                // Animate the x and y coordinates from the initial position (0, 0) to the destination coordinates
                animatedX.set(
                    index === 0 ? 100 : index * (endingX / 100) + 100,
                    {
                        duration,
                    }
                );
                animatedY.set(endingY, { duration });
            });
        }
        if (step == 4) {
            status = type1 === "pass" ? "#118ab2" : "#fb8500";
            onMount(() => {
                // Animate the x and y coordinates from the initial position (0, 0) to the destination coordinates

                animatedX.set(
                    index === 0 ? 100 : index * (endingX / 100) + 100,
                    {
                        duration,
                    }
                );
                animatedY.set(endingY, { duration });
            });
        }
        if (step == 5) {
            status = type2 === "pass" ? "#118ab2" : "#fb8500";

            onMount(() => {
                // Animate the x and y coordinates from the initial position (0, 0) to the destination coordinates
                animatedX.set(
                    index === 0 ? 100 : index * (endingX / 100) + 100,
                    {
                        duration,
                    }
                );
                animatedY.set(endingY, { duration });
            });
        }
        if (step == 6) {
            onMount(() => {
                // Animate the x and y coordinates from the initial position (0, 0) to the destination coordinates
                animatedX.set(
                    index === 0 ? 100 : index * (endingX / 100) + 100,
                    {
                        duration,
                    }
                );
                animatedY.set(endingY, { duration });
            });
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
    x={$animatedX}
    y={$animatedY}
    stroke="white"
    width={endingX / 100}
    height={endingY}
    opacity={0.5} />

<!-- <svg
    xmlns="http://www.w3.org/2000/svg"
    xml:space="preserve"
    class="circle"
    height="50.24px"
    width="40.19px"
    version="1.1"
    x={$animatedX}
    y={$animatedY}
    style="--status:{status}"
    xmlns:ns="&amp;#38;ns_ai;"
    viewBox="0 0 124.189 132.243">
    <path
        stroke-width="1.25"
        d="m62.096 8.5859c-5.208 0-9.424 4.2191-9.424 9.4261 0.001 5.203 4.217 9.424 9.424 9.424 5.202 0 9.422-4.221 9.422-9.424 0-5.208-4.22-9.4261-9.422-9.4261zm-10.41 21.268c-6.672 0-12.131 5.407-12.131 12.07v29.23c0 2.275 1.791 4.123 4.07 4.123 2.28 0 4.127-1.846 4.127-4.123v-26.355h2.102s0.048 68.811 0.048 73.331c0 3.05 2.478 5.53 5.532 5.53 3.052 0 5.525-2.48 5.525-5.53v-42.581h2.27v42.581c0 3.05 2.473 5.53 5.531 5.53 3.054 0 5.549-2.48 5.549-5.53v-73.331h2.127v26.355c0 2.275 1.85 4.123 4.126 4.123 2.28 0 4.073-1.846 4.073-4.123v-29.23c0-6.663-5.463-12.07-12.129-12.07h-20.82z" />
</svg> -->
