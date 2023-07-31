<script>
    export let screenSize;
    export let screenHeight;
    export let expectedSuccessfulStudents;
    export let step;
    let endingX = screenSize - 200;
    let endingY = screenHeight / 2;

    const endingAreaUnsuccessful =
        ((100 - expectedSuccessfulStudents) * endingX) / 100;
    const endingAreaSuccessful = endingX - endingAreaUnsuccessful;
</script>

<style>
</style>

<!-- SVG circle -->
<svg
    width={screenSize}
    height={screenHeight}
    xmlns="http://www.w3.org/2000/svg">
    <rect
        fill={'#fb8500'}
        x={100}
        y={endingY + 20}
        stroke="white"
        width={endingAreaUnsuccessful}
        height={40}
        opacity={0.5} />
    <rect
        fill={'#118ab2'}
        x={endingAreaUnsuccessful + 100}
        y={endingY + 20}
        stroke="white"
        width={endingAreaSuccessful}
        height={40}
        opacity={0.5} />
</svg>
