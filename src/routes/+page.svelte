<script>
    import data from "../data/data.json";
    import MovingStripe from "./MovingStripe.svelte";
    import ScrollyStripe from "./ScrollyStripe.svelte";
    import Select from "svelte-select";
    import Scrolly from "../lib/Scrolly.svelte";

    let value;
    const steps = [
        "<p>No ano lectivo 2018/19, mais de 60 mil alunos começaram o 10º ano em cursos científico humanísticos.</p>",
        "<p>A cada 100 alunos, 23 ficaram para trás, não concluindo o ensino obrigatório no período expectável. </p>",
        "<p>Os outros 77% terminaram nos três anos esperados, em 2020/21. Os dados são do Portal Infoescolas, do Ministério da Educação, que acompanha o percurso dos alunos ao longo do ciclo de escolaridade.</p>",
        "<p> Além de olhar para a percentagem dos alunos que concluem no tempo esperado também os compara com os estudantes com perfil semelhante.</p><p> O gráfico abaixo mostra a percentagem de estudantes em cada município que conclui o secundário em três anos e os que ficam para trás e compara esses valores com os de alunos com perfil semelhante.</p>",
        ,
    ];
    let selected = data[0];
    let screenSize;
    let screenHeight;

    const label = "Nome da NUTS II/ NUTS III / Município";
    const itemId = "Código da Região";

    // Create a writable store with the initial value
    function handleSubmit(e) {
        // selected = selected;
    }
</script>

<style>
    .entry {
        width: 70%;
        display: flex;
        justify-content: center;
        align-items: center;
        color: white;
        flex-direction: column;
        margin: auto;
        text-align: center;
    }
    h1 {
        font-size: 5rem;
    }
    .select-wrapper {
        width: 50%;
        margin: 0 auto;
    }

    .spacer {
        height: 100vh;
    }
    .small-spacer {
        height: 5vh;
    }

    .sticky {
        position: sticky;
        top: 10%;
        flex: 1 1 60%;
        width: 100%;
    }

    .section-container {
        margin-top: 1em;
        text-align: center;
        transition: background 100ms;
        display: flex;
    }

    .step {
        height: 80vh;
        display: flex;
        place-items: center;
        justify-content: center;
    }

    .step-content {
        font-size: 1rem;
        background: whitesmoke;
        color: #ccc;
        border-radius: 5px;
        padding: 0.5rem 1rem;
        display: flex;
        flex-direction: column;
        justify-content: center;
        transition: background 500ms ease;
        box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.2);
        text-align: left;
        width: 75%;
        margin: auto;
        max-width: 500px;
    }

    .step.active .step-content {
        background: white;
        color: black;
    }

    .steps-container {
        flex: 1 1 40%;
        z-index: 10;
    }
    /* Comment out the following line to always make it 'text-on-top' */
    .section-container {
        flex-direction: column-reverse;
    }
    .last {
        z-index: 10;
    }
</style>

<svelte:window bind:innerWidth={screenSize} bind:innerHeight={screenHeight} />
{#if screenSize !== undefined && screenHeight !== undefined}
    <div class="entry">
        <h1>Deixados para trás</h1>
        <p>
            Em 2020/21, mais de 60 mil alunos deviam ter terminado o ensino
            secundário nos três anos devidos. Mas quase um em cada quatro ficou
            para trás. Os gráficos abaixo revelam como se saem os diferentes
            municípios portugueses nesta métrica e onde é que os estudantes se
            saem pior (e melhor do que o esperado para o seu contexto).
        </p>
    </div>
    <div class="section-container">
        <div class="steps-container">
            <Scrolly bind:value>
                {#each steps as text, i}
                    <div class="step" class:active={value === i}>
                        <div class="step-content">
                            {@html text}
                        </div>
                    </div>
                {/each}
                <div class="spacer" />
            </Scrolly>
        </div>
        <div class="spacer" />
        <div class={value === 4 ? 'sticky last' : 'sticky'}>
            {#if value == 4}
                <div class="select-wrapper">
                    <Select
                        class="select"
                        {itemId}
                        items={data}
                        {label}
                        bind:value={selected}
                        on:change={handleSubmit} />
                </div>
                <div class="small-spacer" />
            {/if}
            <div class="screen-wrapper">
                {#key selected}
                    <MovingStripe
                        step={value}
                        {selected}
                        {screenHeight}
                        {screenSize} />
                {/key}
            </div>
        </div>
    </div>
{/if}
