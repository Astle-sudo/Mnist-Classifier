<script>
    import { onMount } from "svelte";

    export let distribution;
    let idarr = ['id0', 'id1', 'id2', 'id3', 'id4', 'id5', 'id6', 'id7', 'id8', 'id9'];

    function drawGraph() {
        for (let i = 0; i < distribution.length; i++) {
            document.getElementById(idarr[i]).style.height = distribution[i] * 100 + "%";
        }
    }

    onMount(() => {
        drawGraph();
    })
</script>

<div class="outer-container">
    <div class="inner-container">
        <div id="id0"></div>
    </div>
    <div class="inner-container">
        <div id="id1"></div>
    </div>
    <div class="inner-container">
        <div id="id2"></div>
    </div>
    <div class="inner-container">
        <div id="id3"></div>
    </div>
    <div class="inner-container">
        <div id="id4"></div>
    </div>
    <div class="inner-container">
        <div id="id5"></div>
    </div>
    <div class="inner-container">
        <div id="id6"></div>
    </div>
    <div class="inner-container">
        <div id="id7"></div>
    </div>
    <div class="inner-container">
        <div id="id8"></div>
    </div>
    <div class="inner-container">
        <div id="id9"></div>
    </div>
</div>

<style>
    .outer-container {
        margin:  8% auto auto auto;
        height: 300px;
        width: 660px;
        display: flex;
        flex-direction: row;
        border-bottom: 2px solid white;
    }
    .inner-container {
        margin: 0 2%;
        display: flex;
        flex-direction: column;
        justify-content: end; 
    }
    #id0, #id1, #id2, #id3, #id4, #id5, #id6, #id7, #id8, #id9 {
        text-align: center;
        background-color: white;
        height: 0%;
        color: black;
        width: 40px;
        transition: height 2s;
    }
    #id0::after {
        color: white;
        position: absolute;
        left: 29%;
        top: 90%;
        display: block;
        content: '0';
    }
    #id1::after {
        color: white;
        position: absolute;
        top: 90%;
        left:33.75%;
        display: block;
        content: '1';
    }
    #id2::after {
        color: white;
        position: absolute;
        top: 90%;
        left:38.5%;
        display: block;
        content: '2';
    }
    #id3::after {
        color: white;
        position: absolute;
        top: 90%;
        left:43%;
        display: block;
        content: '3';
    }
    #id4::after {
        color: white;
        position: absolute;
        top: 90%;
        left:47.75%;
        display: block;
        content: '4';
    }
    #id5::after {
        color: white;
        position: absolute;
        top: 90%;
        left:52.25%;
        display: block;
        content: '5';
    }
    #id6::after {
        color: white;
        position: absolute;
        top: 90%;
        left:57%;
        display: block;
        content: '6';
    }
    #id7::after {
        color: white;
        position: absolute;
        top: 90%;
        left:61.5%;
        display: block;
        content: '7';
    }
    #id8::after {
        color: white;
        position: absolute;
        top: 90%;
        left:66%;
        display: block;
        content: '8';
    }
    #id9::after {
        color: white;
        position: absolute;
        top: 90%;
        left:70.75%;
        display: block;
        content: '9';
    }
</style>