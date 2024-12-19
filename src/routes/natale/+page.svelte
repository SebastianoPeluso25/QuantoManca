<script>

    import Riquadri from '../../lib/components/riquadro.svelte';
    import Footer from '../../lib/components/footer.svelte';
    const Data_natale = new Date("2024-12-25T00:00:00");

    const giorno = 86400000;//24 * 60 * 60 * 1000;
    const ora = 3600000; //60 * 60 * 1000;
    const minuto = 60000; //60 * 1000;
    const secondo = 1000;

    let ms = 0, gg = 0,  hh = 0,  mm = 0,  ss = 0;

    let gg_intero = 0, hh_intero = 0, mm_intero = 0, ss_intero = 0;

    const timeout = () => {
        ms = Data_natale - new Date();


        gg = ms / giorno;
        gg_intero = Math.trunc(gg);
        hh = ((gg - gg_intero) * giorno) / ora;
        hh_intero = Math.trunc(hh);
        mm = ((hh - hh_intero) * ora) / minuto;
        mm_intero = Math.trunc(mm);
        ss = ((mm - mm_intero) * minuto) / secondo;
        ss_intero = Math.ceil(ss);
    } 

   timeout();
    let clock = setInterval(timeout, 1000);
    
    function clear_clock() {
        clearInterval(clock);
    }


    let bool = 0;



</script>
<svelte:head>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Permanent+Marker&display=swap" rel="stylesheet">
    <link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Bungee+Spice&family=Permanent+Marker&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@24,400,0,0" />
    <link href="https://fonts.googleapis.com/css2?family=Fontdiner+Swanky&family=Gloria+Hallelujah&family=Knewave&family=Lacquer&family=Permanent+Marker&display=swap" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Barrio&family=Fontdiner+Swanky&family=Gloria+Hallelujah&family=Knewave&family=Lacquer&family=Permanent+Marker&display=swap" rel="stylesheet">

</svelte:head>

<svelte:window on:beforeunload={clear_clock}/>

<div class="navbar">
    <a  href="/"><span class="material-symbols-outlined">
        home
        </span></a>
</div>

<div class="container">

    {#if bool == 0}
    <h1>Quanto manca al Natale ?</h1>

    <div class="counter">
        <Riquadri chiave="gg" numero={gg_intero} />
        <Riquadri chiave ="hh" numero={hh_intero} />
        <Riquadri chiave ="mm" numero={mm_intero} />
        <Riquadri chiave = "ss" numero={ss_intero} />
    </div>
    {:else}
    <div class="end_counter">

        <img src="https://img.freepik.com/free-photo/vertical-shot-christmas-tree-decorated-with-red-ribbons-balls_181624-25009.jpg" alt="">
        <h1>BUON NATALE !!!!</h1>
        
    </div>
    
    {/if}

</div>

<Footer />

<style>

    @media (max-width: 480px) {

        .container{

        display: grid;
        grid-template-columns: 1fr;
        grid-template-rows: 1fr 5fr;
        width: 80%;
        background-image: linear-gradient(to bottom, white, rgb(247, 105, 105), rgb(244, 82, 82), red);
        margin: auto;
        padding: 20px;
        text-align: center;
        border-radius: 20px;
        
        
        
        
        
    }

    footer{
        text-align: center;
        margin-top: 10%;
        font-size: small;
        }



    .counter {
        display: grid;
        
        

    }

    .navbar{
        width: 100%;
        margin: -10px;
        margin-bottom: 8%;
        
        
    }

    .material-symbols-outlined{
        font-size: 40px;
        color: black;
        font-weight: bold;
        background-color: #d90429;
        
        padding: 10px;
        border-bottom-right-radius: 30px;
        
        
    }

    .container  >h1{
        font-family: "Knewave", system-ui;
        text-transform: uppercase;
        color: #da1e37;
        font-size: 40px;
        margin-top: 10%;
    }

    .end_counter{
        font-family: 'Shantell Sans', cursive;
        height: 14vh;
        color: #9ef01a;
        
        
    }

    .end_counter > img{
        width: 100%;
        height: auto;
        border-radius: 20px;
    }
        
    }

    /*---------------*/


    @media (min-width: 481px) {

        footer{
        text-align: center;
        margin-top: 2%;
        }

    .navbar{
        width: 100%;
        margin: -10px;
        
        
    }

    .end_counter{
        font-family: 'Shantell Sans', cursive;
        margin-bottom: 8%;
        color: #9ef01a;
        font-size: 50px;
    }

    .end_counter > img{
        border-radius: 20px;
    }

    .material-symbols-outlined{
        font-size: 40px;
        color: black;
        font-weight: bold;
        background-color: #d90429;
        
        padding: 10px;
        border-bottom-right-radius: 30px;
        
        
    }



    .container{
        

        width: 80%;
        background-image: linear-gradient(to bottom, white, rgb(247, 105, 105), rgb(244, 82, 82), red);
        
        margin: auto;
        margin-top: 5%;
        padding: 20px;
        text-align: center;
        border-radius: 20px;
        
        
        
        
    }

    .container  >h1{
        text-align: center;
        font-family: "Barrio", system-ui;
        font-weight: 400;
        font-size: 50px;
        color: red;
        
    }


    .counter {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr 1fr;
    }

    }

    
</style>