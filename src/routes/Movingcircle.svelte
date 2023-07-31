<script>
    export let screenSize;
    export let screenHeight;
    // export let sizeVariable;
    export let totalStudents;
    export let percentSuccessfulStudents;
    export let successfulStudents;
    // export let type;
    // export let clickBigButton;
    import Point from "./Point.svelte";
    export let index = 0;

    let array = Array.from({ length: 1000 }, (x, i) => i);

    // Function to generate a random number between min and max (inclusive)
    function getRandomNumber(min, max) {
        return Math.floor(Math.random() * (max - min + 1)) + min;
    }
    function getRandomIndex(max) {
        return Math.floor(Math.random() * max);
    }

    // New array of objects with random numbers
    const newArray = array.map((number, i) => ({
        number,
        x: 100,
        y: getRandomNumber(4, screenHeight / 2 - 4),
        type: "pass",
        // type: i > percentSuccessfulStudents * 10 ? "fail" : "pass",
    }));

    // Number of objects you want to update (in this case, 2)
    let numberOfObjectsToUpdate = 1000 - percentSuccessfulStudents * 10;

    // New value you want to assign
    let newValue = "fail";

    // Randomly select two distinct indices from the array
    let indicesToUpdate = [];
    while (indicesToUpdate.length < numberOfObjectsToUpdate) {
        let randomIndex = getRandomIndex(array.length);
        if (!indicesToUpdate.includes(randomIndex)) {
            indicesToUpdate.push(randomIndex);
        }
    }

    // Update the selected objects with the new value
    indicesToUpdate.forEach((index) => {
        newArray[index].type = newValue;
    });
</script>

<style>
    svg {
        margin-left: auto;
        margin-right: auto;
        display: block;
        position: relative;
    }
    .text-marks {
        font-size: 12px;
        color: white;
    }
</style>

<!-- SVG container -->
<svg
    width={screenSize}
    height={screenHeight / 2 + 100}
    xmlns="http://www.w3.org/2000/svg">
    <line
        x1="100"
        y1={0}
        x2="100"
        y2={screenHeight / 2}
        stroke="white"
        stroke-dasharray="5,5" />
    <foreignObject x="60" y={screenHeight / 2 + 10} width="100" height="100">
        <div class="text-marks">Iniciaram o secundário em 2018/2019</div>
    </foreignObject>

    <line
        x1={screenSize / 2}
        y1={0}
        x2={screenSize / 2}
        y2={screenHeight / 2}
        stroke="white"
        stroke-dasharray="5,5" />
    {#each newArray as point, index}
        <Point
            x={point.x}
            y={point.y}
            index={point.number}
            type={point.type}
            endingX={screenSize}
            endingY={screenHeight / 2} />
    {/each}
</svg>
