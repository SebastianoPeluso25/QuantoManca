<script>

import { onMount } from 'svelte';
import Footer from '../lib/components/footer.svelte';

let timer = 20; // Tempo iniziale in secondi
  let isExpired = false;

  // Recupera il tempo salvato o calcola se il timer è già scaduto
  onMount(() => {
    const savedTime = localStorage.getItem('timer');

    if (savedTime) {
      const { remainingTime, expirationTime } = JSON.parse(savedTime);
      const now = Date.now();

      if (now >= expirationTime) {
        isExpired = true; // Il timer è già scaduto
      } else {
        timer = Math.floor((expirationTime - now) / 1000); // Calcola il tempo rimanente
      }
    } else {
      // Salva l'ora di scadenza nel Local Storage
      const expirationTime = Date.now() + timer * 1000;
      localStorage.setItem(
        'timer',
        JSON.stringify({ remainingTime: timer, expirationTime })
      );
    }

    // Avvia il conto alla rovescia se il timer non è già scaduto
    if (!isExpired) {
      const interval = setInterval(() => {
        if (timer > 0) {
          timer--;
        } else {
          isExpired = true;
          clearInterval(interval);
        }
      }, 1000);
    }
  });
    

    

</script>

<svelete:head>
    <link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Permanent+Marker&display=swap" rel="stylesheet">

<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@24,400,0,0" />
<link href="https://fonts.googleapis.com/css2?family=Barrio&family=Fontdiner+Swanky&family=Gloria+Hallelujah&family=Knewave&family=Lacquer&family=Permanent+Marker&display=swap" rel="stylesheet">
</svelete:head>

<a href="/game">
  <div class="button-game" >
    Acchiappa il Babbo
  </div>
</a>

<a href="/game2">
  <div class="button-game" >
    Babbo GO !
  </div>
</a>

<div class="container">

    <h1>Quanto Manca ?</h1>

    <a href="/natale" class="neon-button">
        <button class="item natale" href="/natale">
        Al Natale ?

        <span class="material-symbols-outlined">
            arrow_forward_ios
            </span>
        </button>
    </a>

    <a href="/capodanno">
        <button class="item capodanno">
            all'anno nuovo ?

            <span class="material-symbols-outlined">
                arrow_forward_ios
            </span>
        </button>
    </a>

    
    
</div>



<Footer />




<style>

@media (max-width: 480px) {

  :global(body){
        background-color: rgb(255, 167, 167);
        
    }

    .container > h1{
        text-align: center;
        font-family: "Barrio", system-ui;
        font-weight: 400;
        color: red;
    }

    .button-game{
      margin: auto;
      width: max-content;
      margin-top: 4%;
      padding: 10px;
      border: 4px solid white;
      border-radius: 10px;
      background-color: red;
      color: white;
      font-size: 20px;
      padding: 14px;
      font-family: 'Permanent Marker', cursive;
      
    }

    .button-game:hover{
      cursor: pointer;
    }

    .container{
        width: 90%;
        
        margin: auto;
        display: grid;
        grid-template-columns: 1fr;
        grid-template-rows: 1fr 1fr;
        row-gap: 8vh;
        padding-bottom: 5vh;
        margin-top: 30%;
        align-items: center;
        
        background-color: #F3DFA2;
        border: 8px solid #faa307;
        border-radius: 20px;
        

        

    }

    

    

    footer{
        text-align: center;
        margin-top: 10%;
        font-size: 12px;
        }

    a{
        text-decoration: none;
        color: white;
    }

    .item:hover{
        cursor: pointer;
    }



    .item{
        width: 90%;
        border-radius: 20px;
        margin: auto;
        text-align: center;
        background-color: #D04027;
        padding: 8px;
        font-family: 'Permanent Marker', cursive;
        border: none;
        display: grid;
        grid-template-columns: 8fr 1fr;
        align-items: center;
        justify-content: center;
        color: white;
        font-size: 30px;
        border-bottom: 8px solid white;

    }


}

/*---------------*/
/*Orrizzontale*/

@media (min-width: 481px) {

  :global(body){
        background-color: rgb(255, 131, 131);
        
    }

    .container > h1{
        text-align: center;
        font-family: "Barrio", system-ui;
        font-weight: 400;
        font-size: 48px;
        color: red;
    }

    .button-game{
      margin: auto;
      width: max-content;
      margin-top: 4%;
      padding: 10px;
      border: 4px solid white;
      border-radius: 10px;
      background-color: red;
      color: white;
      font-size: 20px;
      padding: 14px;
      font-family: 'Permanent Marker', cursive;
      
    }

    .button-game:hover{
      cursor: pointer;
    }

    .container{
        width: 60%;
        
        margin: auto;
        display: grid;
        grid-template-columns: 1fr;
        grid-template-rows: 1fr 1fr 1fr;
        
        margin-top: 5%;
        padding: 40px;
        align-items: center;
        justify-content: center;
        background-color: #F3DFA2;
        
        
        border-radius: 20px;
        background-color: #F3DFA2;
        border: 8px solid #faa307;

    }



    

    footer{
        text-align: center;
        margin-top: 2%;
        font-size: 14px;
        }


    

    a{
        text-decoration: none;
        color: white;
    }

    .item:hover{
        cursor: pointer;
    }



    .item{
        width: 60%;
        border-radius: 20px;
        margin: auto;
        text-align: center;
        background-color: #D04027;
        padding: 8px;
        font-family: 'Permanent Marker', cursive;
        border: none;
        display: grid;
        grid-template-columns: 2fr 1fr;
        align-items: center;
        justify-content: center;
        color: white;
        font-size: 30px;
        border-bottom: 8px solid white;

    }
}



    



    
</style>