<script>
    export let screenSize;
    export let screenHeight;
    // export let sizeVariable;
    export let selected;
    export let step;
    // export let type;
    // export let clickBigButton;
    import Stripe from "./Stripe.svelte";
    import RefBar from "./RefBar.svelte";

    export let index = 0;

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

    // // New array of objects with random numbers
    // const newArray = array.map((number, i) => ({
    //     number,
    //     x: 100,
    //     y: getRandomNumber(4, screenHeight / 2 - 4),
    //     // type: "pass",
    //     type: i < 100 - percentSuccessfulStudents ? "fail" : "pass",
    // }));

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
    .step-content {
        font-size: 1rem;
        background: whitesmoke;
        border-radius: 5px;
        padding: 0.5rem 1rem;
        /* display: flex; */
        flex-direction: column;
        justify-content: center;
        box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.2);
        text-align: left;
        width: 75%;
        margin: 0 auto;
        max-width: 500px;
    }
    .mark-fail {
        background-color: #fb8500;
        color: white;
        padding-left: 2;
        padding-right: 2;
    }
    .underline {
        text-decoration: underline;
    }
</style>

<!-- SVG container -->
{#if step === 4 && selected['Nome da NUTS II/ NUTS III / Município'] !== 'Total Nacional (Continente) em Cursos Científico-Humanísticos'}
    <p class="step-content mun-paragraph">
        Neste município,
        <span class="mark-fail"> {100 - percentSuccessfulStudents}% </span>
        dos alunos não terminaram o secundário nos três anos esperados. O valor
        está
        <span class="underline">
            {100 - percentSuccessfulStudents - (100 - expectedSuccessfulStudents) < 0 ? 'abaixo do' : 100 - percentSuccessfulStudents - (100 - expectedSuccessfulStudents) == 0 ? 'em linha com o' : 'acima do'}</span>
        esperado para alunos de contexto semelhante.
    </p>
{/if}
<svg
    width={screenSize}
    height={screenHeight}
    xmlns="http://www.w3.org/2000/svg">
    {#if step > 3}
        <line
            x1={endingArea}
            y1={screenHeight / 2}
            x2={endingArea}
            y2={screenHeight / 4}
            stroke="white"
            stroke-dasharray="5,5" />
    {/if}
    {#each newArray as point, index}
        <Stripe
            x={point.x}
            y={point.y}
            index={point.number}
            type={point.type}
            endingX={screenSize - 200}
            endingY={screenHeight / 4}
            {percentSuccessfulStudents}
            {step} />
    {/each}
    {#if expectedSuccessfulStudents !== null || step === 3}
        <RefBar
            expectedSuccessfulStudents={expectedSuccessfulStudents === null ? 90 : expectedSuccessfulStudents}
            {screenHeight}
            {screenSize} />
    {/if}
</svg>
