<template>
  <div class="is-flex is-align-items-center is-justify-content-left">
    <Cronometro :tempoSeg="tempoSeg" />
    <Button @acionar="iniciar" icone="fas fa-play" texto="play" :disabled="cronometroRodando"/>
    <Button @acionar="finalizar" icone="fas fa-stop" texto="stop" :disabled="!cronometroRodando"/>
    <!-- <button :disabled="!cronometroRodando" @click="finalizar" class="button">
      <span class="icon">
        <i class="fas fa-stop"></i>
      </span>
      <span>stop</span>
    </button> -->
  </div>
</template>

<script lang="ts">
import Button from './Button.vue'
import { defineComponent } from "vue";
import Cronometro from './Cronometro.vue'
export default defineComponent({
  name: "TemporizadorComponent",
  //Sinalizar que esse componente vai emitir uma lista de eventos em algum momento
  emits: ['aoTemporizadorFinalizado'],
  components: {
    Cronometro, 
    Button 
  },
  props: {
    tarefa: {
      type: String,
      default: ''
    }
  },
  data(){
    return {
      tempoSeg: 0,
      tempoMin: 0,
      tempoHora: 0,
      cronometro: 0,
      lista: [],
      cronometroRodando: false
    }
  },
  methods: {
    iniciar(){
      if(!this.tarefa){
        alert('Digite alguma tarefa para inicializar')
        return
      }
      this.cronometroRodando = true

      this.cronometro = setInterval(() => {
        this.tempoSeg += 1
        if(this.tempoSeg == 60){
          this.tempoMin += 1
          this.tempoSeg = 0
        }
      }, 100)
      
      console.log('Iniciando')
    },
    finalizar(){
      clearInterval(this.cronometro)

      this.cronometroRodando = false

      this.$emit('aoTemporizadorFinalizado', this.tempoSeg)//Payload = carga de dados

      this.tempoSeg = 0
      
    }
  }
});
</script>

<style>
</style>