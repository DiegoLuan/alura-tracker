<template>
  <div class="box formulario">
    <div class="columns">
      <div
        class="column is-8"
        role="form"
        area-label="Formulário para criação de uma nova tarefa"
      >
        <!-- is-X - X colunas -->
        <input
          type="text"
          class="input"
          placeholder="Qual tarefa você deseja iniciar?"
          v-model="tarefa"
        />
      </div>
      <div class="column">
        <!-- Quando chamar o evento, vai chamar o método finalizar tarefa -->
        <Temporizador @aoTemporizadorFinalizado="finalizarTarefa" :tarefa="tarefa"/>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Temporizador from './Temporizador.vue'
import ITarefa from "@/interfaces/iTarefa";

export default defineComponent({
  name: "FormularioComponent",
  components: {
    Temporizador
  },
  emits: ['aoSalvarTarefa'],
  data(){
    return {
      tarefa: '',
      lista: [] as ITarefa[]
    }
  },
  methods: {
    //void --> Retorna nada, parametro vai receber o que foi passado no payload do evento
    finalizarTarefa(tempoDecorrido: number) : void {

      this.$emit('aoSalvarTarefa', {
        duracaoEmSegundos: tempoDecorrido,
        descricao: this.tarefa,
        id: Date.now()
      })

      this.tarefa = ''
    }
  },

});
</script>

<style>
.formulario {
  color: var(--texto-primario);
  background-color: var(--bg-primario);
}
</style>