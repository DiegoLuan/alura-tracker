<template>
  <section class="mr-2">
    <strong class="display"> {{ tempoDecorrido }} </strong>
  </section>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "CronometroTarefa",
  props: {
    tempoSeg: {
      type: Number,
      default: 0
    },
  },
  //Computed vai monitorar uma informação e conforme essa informação for alterada, ele vai reagir e se atualizar
  computed: {
    //o String significa que esse método vai retornar uma string
    tempoDecorrido(): string {
      return new Date(this.tempoSeg * 1000).toISOString().substr(11, 8);
    },
  },
});
</script>

<style scoped>
  .display{
    color: var(--cronometro) !important;
  }
</style>