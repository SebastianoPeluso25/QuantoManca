<script>
  import { onMount } from 'svelte';

  let playerY = 0;
  let isJumping = false;
  let obstacles = [];
  let gameRunning = false;
  let gameOver = false;
  let startTime = 0;
  let elapsedTime = 0;
  let bestTime = 0;
  const gravity = 1;
  const jumpSpeed = 2;
  let jumpPressed = false;

  const startGame = () => {
    playerY = 0;
    isJumping = false;
    obstacles = [];
    gameRunning = true;
    gameOver = false;
    startTime = Date.now();
    spawnObstacles();
    requestAnimationFrame(updateGame); // Avvia l'animazione
  };

  const handleJumpStart = () => {
    jumpPressed = true;
  };

  const handleJumpEnd = () => {
    jumpPressed = false;
  };

  const spawnObstacles = () => {
    const interval = setInterval(() => {
      if (!gameRunning) {
        clearInterval(interval);
        return;
      }
      obstacles = [
        ...obstacles,
        { x: 100, y: Math.random() * 380, width: 40, height: 40 }
      ];
    }, 2000);
  };

  const updateGame = () => {
    if (!gameRunning) return;

    // Aggiorna il giocatore
    if (jumpPressed) {
      playerY += jumpSpeed;
    } else {
      playerY = Math.max(0, playerY - gravity);
    }

    // Limita il giocatore all'altezza massima del contenitore
    playerY = Math.min(playerY, 380);

    // Aggiorna gli ostacoli
    obstacles = obstacles.map((obstacle) => ({
      ...obstacle,
      x: obstacle.x - 2
    }));

    // Controlla le collisioni
    obstacles.forEach((obstacle) => {
      const playerX = 10; // posizione X del giocatore
      const playerWidth = 40;
      const playerHeight = 40;

      if (
        obstacle.x < playerX + playerWidth &&
        obstacle.x + obstacle.width > playerX &&
        playerY < obstacle.y + obstacle.height &&
        playerY + playerHeight > obstacle.y
      ) {
        gameRunning = false;
        gameOver = true;
        elapsedTime = Math.floor((Date.now() - startTime) / 1000);
        
        if (elapsedTime > bestTime) {
          bestTime = elapsedTime;
          localStorage.setItem('bestTime', bestTime); // Salva il record nel localStorage
        }
      }
    });

    // Rimuovi gli ostacoli superati
    obstacles = obstacles.filter((obstacle) => obstacle.x > -10);

    // Aggiorna il timer
    elapsedTime = Math.floor((Date.now() - startTime) / 1000);

    // Continua l'animazione
    if (gameRunning) requestAnimationFrame(updateGame);
  };

  onMount(() => {
    // Recupera il record dal localStorage
    const savedBestTime = localStorage.getItem('bestTime', bestTime);
    if (savedBestTime) {
      bestTime = parseInt(savedBestTime, 10);
    }


    window.addEventListener('keydown', (e) => {
      if (e.code === 'Space') handleJumpStart();
    });
    window.addEventListener('keyup', (e) => {
      if (e.code === 'Space') handleJumpEnd();
    });
  });
</script>



<div>
  <div class="navbar">
    <a class="icon_home" href="/"><span class="material-symbols-outlined">
        home
        </span></a>
      <div class="scoreboard">
        <div>Tempo: {elapsedTime} s</div>
        <div>Record: {bestTime} s</div>
      </div>
</div>
  
  <div
    class="game-container"
    on:touchstart|preventDefault={handleJumpStart}
    on:touchend|preventDefault={handleJumpEnd}
    on:mousedown={handleJumpStart}
    on:mouseup={handleJumpEnd}
  >
    <div
      class="player"
      style="bottom: {playerY}px;"
    ></div>
    {#each obstacles as { x, y, width, height }, i}
      <div
        class="obstacle"
        style="left: {x}%; bottom: {y}px;"
      ></div>
    {/each}
    <div class="game-over {gameOver ? 'visible' : ''}">Game Over</div>
  </div>
  <div id="start-button" on:click={startGame} disabled={gameRunning}>
    {gameRunning ? 'Gioco in corso...' : 'Start'}
  </div>
</div>

<svelte:head>
  <link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@24,400,0,0" />

<link href="https://fonts.googleapis.com/css2?family=Fontdiner+Swanky&family=Gloria+Hallelujah&family=Permanent+Marker&display=swap" rel="stylesheet">
</svelte:head>

<style>
        :global(body){
        background-color: rgb(255, 131, 131);
        padding: 0;
        margin: 0;
        
    }

    .navbar{
      display: grid;
      grid-template-columns: 1fr 5fr;
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
    width: 90%;
    margin: auto;
    height: 400px;
    background: lightblue;
    border: 8px solid white;
    border-radius: 8px;
    overflow: hidden;
    position: relative;
  }

  .player {
    width: 200px;
    height: 80px;
    background-image: url('https://www.sociomamma.it/wp-content/uploads/2017/12/Babbo-Natale-con-slitta-1.png');
    background-size: cover;
    position: absolute;
    bottom: 0;
    left: 10px;
    transition: bottom 0.1s;
  }

  .obstacle {
    position: absolute;
    width: 40px;
    height: 40px;
    background-color: green;
/*     background-image: url('/grinch.png');
    background-size: cover; */
  }

  .scoreboard > div{
    background-color: #eeba0b;
    color: #003566;
    padding: 10px;
    border: 4px solid #bf211e;
    border-radius: 8px;
    text-transform: uppercase;
    font-weight: bolder;
    font-size: 20px;
  }

  .scoreboard {
    font-size: 16px;
    margin-top: 10px;
    display: flex;
    flex-direction: row;
    align-content: center;
    justify-content: space-around;
    column-gap: 8px;
    padding: 20px;
  }

  .game-over {
    font-size: 32px;
    width: max-content;
    color: red;
    padding: 10px;
    background-color: #de4a47;
    opacity: 2;
    border-left: 8px solid darkred;
    position: absolute;
    top: 50%;
    left: 50%;
    transition: cubic-bezier(0.175, 0.885, 0.32, 1.275);
    transform: translate(-50%, -50%);
    display: none;
    color: white;
    
  }

  .game-over.visible {
    display: block;
  }

  #start-button {
    margin-top: 10px;
    padding: 10px 20px;
    font-size: 16px;
    border: none;
    background-color: rgb(167, 2, 2);
    color: white;
    text-transform: uppercase;
    border-radius: 10px;
    width: max-content;
    margin: auto;
    cursor: pointer;
    margin-top: 20px;
    font-size: 20px;
    

  }
</style>


