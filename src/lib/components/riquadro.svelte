<script>

    export let numero = 0;

    export let chiave;

    let tipo2txt = {
        gg: 'Giorni',
        hh: 'Ore',
        mm: 'Minuti',
        ss: 'Secondi'
    }

    

</script>

<div class="riquadro">
    <div class="count">{numero}</div>
    <div class="testo">{tipo2txt[chiave]}</div>
</div>




<style>

@media (max-width: 480px) {

    .riquadro{
        display: grid;
        width: 60%;
        background-color: red;
        grid-template-rows: 2fr 1fr;
        margin: auto;
        border: 8px solid white;
        --angle: 0deg;
	  border-image: conic-gradient(from var(--angle), red, rgb(255, 252, 78)) 1;
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

    .count{
        
        font-family: 'Black Ops One', cursive;
        font-size: 66px;
        color: #F9F871;
        text-shadow: 4px 4px 10px #051937;
        display: flex;
        align-items: center;
        justify-content: center;
        
}

.testo{
    font-family: 'Black Ops One', cursive;
    font-size: 38px;
    color: #F9F871;

}


}





/*----------------*/

@media (min-width: 481px) {

    .riquadro{
        display: grid;
        width: 80%;
        background-color: red;
        grid-template-rows: 2fr 1fr;
        margin: auto;
        border: 8px solid white;
        --angle: 0deg;
	  border-image: conic-gradient(from var(--angle), red, rgb(255, 252, 78)) 1;
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

    .count{
        
            font-family: 'Black Ops One', cursive;
            font-size: 18vh;
            color: #F9F871;
            text-shadow: 4px 4px 10px #051937;
            display: flex;
            align-items: center;
            justify-content: center;
            
    }

    .testo{
        font-family: 'Black Ops One', cursive;
        font-size: 38px;
        color: #F9F871;

    }

}

    





</style>