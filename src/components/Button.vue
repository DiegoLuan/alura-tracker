<template>
  <button :disabled="disabled" @click="acionar" class="button mr-2">
      <span class="icon">
        <i :class="icone"></i>
      </span>
      <span>{{texto}}</span>
    </button>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
export default defineComponent({
  name: 'ButtoAction',
  emits: ['Acionar'],
  props: {
    icone: { 
      type: String,
      required: true
    },
    texto: {
      type: String,
    },
    disabled: {
      type: Boolean
    }
  },
  methods: {
    acionar(){
      this.$emit('Acionar')
    }
  }
})
</script>

<style>

</style>