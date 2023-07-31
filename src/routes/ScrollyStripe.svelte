<script>
    import Stripe from "./Stripe.svelte";
    import RefBar from "./RefBar.svelte";
    import StaticStripe from "./StaticStripe.svelte";
    export let screenSize;
    export let screenHeight;
    export let selected;
    export let index = 0;
    export let step;

    let percentSuccessfulStudents = Number(
        selected[
            "% alunos da região que concluíram os cursos científico-humanísticos (CH) em três anos2020/2021"
        ].replace("%", "")
    );
    let totalNumberOfStudents =
        selected["Número de alunos da região na amostra2020/2021"];

    let expectedSuccessfulKey =
        selected[
            "% alunos do país com um perfil semelhante aos da região que concluíram os cursos científico-humanísticos (CH) em 3 anos (média nacional comparável)2020/2021"
        ];
    let expectedSuccessfulStudents =
        expectedSuccessfulKey !== null
            ? Number(
                  selected[
                      "% alunos do país com um perfil semelhante aos da região que concluíram os cursos científico-humanísticos (CH) em 3 anos (média nacional comparável)2020/2021"
                  ].replace("%", "")
              )
            : null;

    let array = Array.from({ length: 100 }, (x, i) => i);

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
        x: getRandomNumber(100, screenSize - 100),
        y: getRandomNumber(4, screenHeight / 2),
        // type: "pass",
        type: i < 100 - percentSuccessfulStudents ? "fail" : "pass",
    }));

    const endingArea =
        (100 - percentSuccessfulStudents) * ((screenSize - 200) / 100) + 100;
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
        text-align: right;
    }
</style>

<!-- SVG container -->
<svg
    width={screenSize}
    height={screenHeight}
    xmlns="http://www.w3.org/2000/svg">
    {#each newArray as point, index}
        <StaticStripe
            x={point.x}
            y={point.y}
            index={point.number}
            type={point.type}
            endingX={screenSize - 200}
            endingY={screenHeight / 4}
            {percentSuccessfulStudents}
            {step} />
    {/each}
    {#if expectedSuccessfulStudents !== null}
        <RefBar {expectedSuccessfulStudents} {screenHeight} {screenSize} />
    {/if}
</svg>
