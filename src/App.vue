<template>
  <div id="app">
    <h1>Metronomo</h1>
    <h4> Para alumnos de Casa de la Cultura</h4>
    <div  >
      <label  for="tempo">Tempo (BPM): </label>
      <input :disabled="isRunning" type="number" id="tempo" v-model="tempo">
    </div>
    <div>
      <button @click="startMetronome" :disabled="isRunning">Iniciar</button>
      <button @click="stopMetronome" :disabled="!isRunning">Detener</button>
    </div>
    <div class="pencil-container" :class="{  'topcolor': isAnimating , 'bottomcolor': !isAnimating}">
      <div class="pencil" :class="{ 'animate': isAnimating  }" >
        <div class="body"></div>
      <div class="tip"></div>
      <div class="eraser"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tempo: 85,
      isRunning: false,
      isAnimating: false,
      intervalId: null,
      isImpar: false,
    };
  },
  methods: {
    startMetronome() {
      this.isRunning = true;
      const interval = 60000 /( this.tempo *2); // Calcula el intervalo en milisegundos
      this.intervalId = setInterval(() => {
        this.playClick();
        this.animatePencil();
      }, interval);

      //disable input 


    },
    stopMetronome() {
      this.isRunning = false;
      clearInterval(this.intervalId);
      this.isAnimating = false;
    },
    playClick() {
      // Agrega aquí la lógica para reproducir el sonido del metrónomo
      // reproducir sonido cada 2 playClick

      if (!this.isImpar) {
       
        const audio = new Audio('src/assets/beat.wav');
        audio.play();
     
      } 
      this.isImpar = !this.isImpar;
      

    },
    animatePencil() {

      this.isAnimating = !this.isAnimating;
      
    },
    animationEnd() {
      // Esta función se llama al finalizar la animación
      this.isAnimating = false;


    },
  },
};
</script>

<style>
#app {
  max-width: 400px;
  margin: 0 auto;
}

button {
  padding: 10px;
  margin: 5px;
  cursor: pointer;
}

.h1 {
  color: #007BFF;
}

.pencil-container {
  height: 100px;
  position: relative;
  border-top: #807f7f 2px solid ;
  border-bottom: #807f7f 2px solid ;
}

.pencil {
  width: 200px;
  height: 20px;
  
  position: absolute;
  top: 0;
 
  margin: 20px auto;
  transition: transform 0.3s ease-in-out;
}

/* border-top red in pencil-container if exist the class animate in father */



.topcolor{
  border-bottom: #0015ff 2px solid ;
  border-top: #000000 2px solid ;
  
  
}
.bottomcolor{
  border-top: #FF0000 2px solid ;
  border-bottom: #000000 2px solid ;
  
  
}

.pencil .body {
      width: 150px;
      height: 20px;
      background-color: rgb(241, 146, 13);
      position: absolute;
      left: 20px;
      top: 50%;
      transform: translateY(-50%);
    }

    .pencil .tip {
      width: 0;
      height: 0;
      border-top: 10px solid transparent;
      border-bottom: 10px solid transparent;
      border-left: 20px solid #000000;
      position: absolute;
      left: 170px;
      top: 50%;
      transform: translateY(-50%);
    }

    .pencil .eraser {
      width: 10px;
      height: 20px;
      background-color: rgb(218, 16, 225);
      position: absolute;
      border-right: #807f7f 10px solid;
      left: 0;
      top: 50%;
      transform: translateY(-50%);
    }

.animate {
  transform: translateY(50px);


  
  
}
</style>