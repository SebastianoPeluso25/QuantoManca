<script>
    import { onMount } from 'svelte';
  
    let score = 0;
    let x = 50; // posizione iniziale orizzontale
    let y = 50; // posizione iniziale verticale
    let interval;
  
    const moveImage = () => {
      // Posizioni casuali nel range della finestra
      x = Math.random() * 90; // % della larghezza
      y = Math.random() * 90; // % dell'altezza
    };
  
    const handleClick = () => {
      score++;
      moveImage();
    };
  
    onMount(() => {
      interval = setInterval(moveImage, 1000); // cambia posizione ogni secondo
      return () => clearInterval(interval); // pulizia
    });




  </script>

  <svelte:head>
    <link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@24,400,0,0" />

<link href="https://fonts.googleapis.com/css2?family=Fontdiner+Swanky&family=Gloria+Hallelujah&family=Permanent+Marker&display=swap" rel="stylesheet">
  </svelte:head>

  <div class="navbar">
    <a class="icon_home" href="/"><span class="material-symbols-outlined">
        home
        </span></a>
    <div class="score">Score {score}</div>
</div>

  <div class="game-container">
    
    <img
      src="https://www.sociomamma.it/wp-content/uploads/2017/12/Babbo-Natale-con-slitta-1.png"
      alt="Immagine da cliccare"
      class="image"
      style="top: {y}%; left: {x}%"
      on:click={handleClick}
    />
  </div>
  

  <style>

    @media(min-width:480px){

      :global(body){
        background-color: rgb(255, 131, 131);
        
    }
        h1{
        font-family: "Fontdiner Swanky", serif;
        text-align: center;
        
    }

    .header{
        display: grid;
        grid-template-columns: 2fr 1fr;
        justify-items: center;
        
    }

    .navbar > .score{
        
        width: max-content;
        padding: 10px;
        font-family: "Fontdiner Swanky", serif;
        font-size: 40px;
        
        border: 4px solid red;
    }

    .navbar{
      display: flex;
      flex-direction: row;
      justify-content: space-between;
        
        
    }

    .material-symbols-outlined{
        font-size: 40px;
        color: black;
        font-weight: bold;
        background-color: #d90429;
        
        padding: 10px;
        border-bottom-right-radius: 30px;
        
        
    }



    .game-container {
      position: relative;
      width: 90%;
      margin: auto;
      height: 90vh;
      overflow: hidden;
      background-color: #fce6ab;
      border: 8px solid;
      --angle: 0deg;

	
	border-image: conic-gradient(from var(--angle), red, rgb(255, 0, 0), rgb(255, 252, 78)) 1;
	
	animation: 10s rotate linear infinite;
    }

    @keyframes rotate {
	to {
		--angle: 360deg;
	}
}

@property --angle {
  syntax: '<angle>';
  initial-value: 0deg;
  inherits: false;
}


    .image {
      position: absolute;
      width: 200px;
      height: 100px;
      cursor: pointer;
      transition: all 0.3s ease;
    }
    }


    @media(max-width:480px){

    :global(body){
        background-color: rgb(255, 131, 131);
        
    }

        h1{
        font-family: "Fontdiner Swanky", serif;
        text-align: center;
        font-size: 30px;
        
    }

    .navbar{
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        
        
    }

    .material-symbols-outlined{
        font-size: 40px;
        color: black;
        font-weight: bold;
        background-color: #d90429;
        
        padding: 10px;
        border-bottom-right-radius: 30px;
        
        
    }

    .header{
        display: grid;
        width: 90%;
        margin: auto;
        grid-template-rows: 1fr 1fr;
        justify-items: center;
    }

    .navbar > .score{
        
        width: max-content;
        padding: 10px;
        font-family: "Fontdiner Swanky", serif;
        font-size: 30px;
        border: 4px solid red;
        border-radius: 20px;
        background-color: white;
    }



    .game-container {
      position: relative;
      width: 90%;
      margin: auto;
      height: 90vh;
      overflow: hidden;
      background-color: #fce6ab;
      border: 8px solid;
      --angle: 0deg;
	  border-image: conic-gradient(from var(--angle), red, rgb(255, 0, 0), rgb(255, 252, 78), purple) 1;
	  animation: 10s rotate linear infinite;
    }

    @keyframes rotate {
	to {
		--angle: 360deg;
	}
}

@property --angle {
  syntax: '<angle>';
  initial-value: 0deg;
  inherits: false;
}
    .image {
      position: absolute;
      width: 200px;
      height: 100px;
      cursor: pointer;
      transition: all 0.3s ease;
    }
    }


  </style>