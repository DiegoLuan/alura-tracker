<template>
  <Box>
    <div class="columns">
      <div class="column is-7">
        {{ tarefa.descricao }}
      </div>
      <div class="column is-4 display">
        <Cronometro :tempoSeg="tarefa.duracaoEmSegundos" />
      </div>
      <button @click="deletarTarefa(tarefa.id)" class="button">
        <span class="icon">
          <i class="fa-regular fa-trash-can" style="color: #000000;"></i>
        </span>
      </button>
    </div>
  </Box>
</template>

<script lang="ts">
import ITarefa from '@/interfaces/iTarefa';
import Cronometro from './Cronometro.vue'
import { defineComponent, PropType } from "vue";
import Box from './Box.vue';
export default defineComponent({
  name: "listaTarefas",
  components: {
    Cronometro,
    Box
  },
  emits: ['itemDeletado'],
  props: {
    tarefa: {
      //indicar que é um tipo específico de objeto, no caso, objeto do tipo ITarefa
      type: Object as PropType<ITarefa>,
      required: true
    },
    delete: {
      type: Function
    }
  },
  data() {
    return {
      efeito: false
    }
  },
  methods: {
    deletarTarefa(id : number) {
      this.$emit('itemDeletado', id)
    },
  }

});
</script>

<style scoped>
  .display{
    color: var(--cronometro);
  }
</style>