<script>
    import * as flow from '@tensorflow/tfjs';
    import Chart from '../components/chart.svelte';
    import { onMount } from "svelte";

    async function loadModel () {
        model = await flow.loadLayersModel('/bettersoftmaxJSON/model.json');
    }

    const box = () => {
        let e = document.createElement('div');

        e.style.width = '10px';
        e.style.height = '10px';
        e.style.backgroundColor = 'black';

        e.addEventListener('mouseenter', () => {
            if (isDrawing) {
                e.style.backgroundColor = 'white';
            }
        })

        return e;
    }

    const row = () => {
        let r = document.createElement('div');

        r.style.display = 'flex';
        r.style.flexDirection = 'row';
        for (let i = 0; i < 28; i++) {
            let b = box();
            r.appendChild(b);
        }

        return r;
    }

    function createBox () {
        for (let i = 0; i < 28; i++) {
            let r = row()
            container.appendChild(r);
        }
    }

    function clearScreen () {
        for (let i = 0; i < 28; i++) {
            for (let j = 0; j < 28; j++) {
                container.children[i].children[j].style.backgroundColor = 'black';
            }
        }
    }

    function getArray () {
        let array = Array.from({ length: 28 }, () => Array(28).fill(0));
        for (let i = 0; i < 28; i++) {
            for (let j = 0; j < 28; j++) {
                let value = window.getComputedStyle(container.children[i].children[j]).backgroundColor.match(/\d+/g);
                let [r, g, b] = value;
                let grayscale = (parseFloat(r) + parseFloat(g) + parseFloat(b)) / 3;
                array[i][j] = grayscale;
            }
        }
        return array;
    }

    function makegraph (distribution) {
        chart = new Chart ({
            target: document.body,
            props: {
                distribution: distribution
            }
        })
    }

    function predict () {
        let input = flow.tensor(getArray());
        let reshapedInput = input.reshape([1,28,28]);
        distribution = model.predict(reshapedInput).dataSync();
        makegraph(distribution);
        chart.$destroy();
    }

    let model, container, chart, isDrawing = false, distribution;

    onMount(() => {
        createBox();
        loadModel();
        container.addEventListener('click', () => {
            if (!isDrawing) {isDrawing = true;}
            else {isDrawing = false};
        });
        makegraph([0, 0, 0, 0, 0, 0, 0, 0, 0]);
    })
</script>

<div bind:this={container} id="container"></div>
<button id="predict" on:click={predict}>Predict</button>
<button id="clear" on:click={clearScreen}>Clear</button>
<button id="reset" on:click={() => {makegraph([0, 0, 0, 0, 0, 0, 0, 0, 0, 0]);chart.$destroy()}}>Reset distribution</button>

<style>
    :global(body) {
        background-color: orange;
    }
    #container {
        margin-top: 1%;
        margin-left: 40%;
        width: fit-content;
        border: 1px solid black;
    }
    button {
        background-color: orange;
        border: 1px solid white;
        color: white;
        padding: 0.5%;
    }
    button:hover {
        cursor: pointer;
        background-color: white;
        color: orange;
    }
    #predict {
        margin-top: 2%;
        margin-left: 42%;
    }
</style>