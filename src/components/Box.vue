<template>
  <!-- Uma outra forma de aplicar estilo a um componente HTML -->
  <div class="box has-text-weight-bold" :style="estilos">
    <slot/>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'BoxContent',
  data() {
    return {
      // Uma outra forma de aplicar estilo a um componente HTML
      estilos: {
        background:'#faf0ca',
      }
    }
  }
})
</script>

