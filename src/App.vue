<template>
  <!-- Columns -- Indica que terá varias colunas
  is-gapless -- Sem espaço entre as colunas
  is-multiline -- Permite várias linhas -->
  <main :class="{'modo-escuro': darkTheme}" class="columns is-gapless is-multiline">
    <div class="column is-one-quarter">
      <BarraLateral @aoTemaAlterado="trocarTema" />
    </div>
    <div class="column is-three-quarter conteudo">
      <Formulario @aoSalvarTarefa="salvarTarefa" class="mb-5" />

      <div class="lista">
        <div>
          <Tarefas @item-deletado="deletarTarefa" v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa"/>
        </div>
        <Box v-if="listaEstaVazia" class="lista">
          <span>Nenhuma tarefa adicionada :(</span>
        </Box>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import Box from './components/Box.vue'
import { defineComponent } from 'vue';
import BarraLateral from './components/BarraLateral.vue';
import Formulario from './components/Formulario.vue'
import Tarefas from './components/Tarefas.vue'
import ITarefa from './interfaces/iTarefa';

export default defineComponent({
  //lib http-server simula um servidor http e depois subir o arquivo HTML como se fosse um servidor
  name: 'App',
  data() {
    return {
      //Uma lista bem específica de tarefas
      tarefas: [] as ITarefa[],
      darkTheme: false,
      itemDeletado: null
    }
  },
  components: {
    BarraLateral,
    Formulario,
    Tarefas,
    Box
  },
  created() {
    const lista = localStorage.getItem('lista')
    
    if(lista){
      const listaConvertida = JSON.parse(lista)
      listaConvertida.map((item : ITarefa) => this.tarefas.push(item))
    }
    
  },
  computed: {
    listaEstaVazia(): boolean {
      return this.tarefas.length === 0
    }
  },
  methods: {
    salvarTarefa(tarefa: ITarefa) {
      this.tarefas.push(tarefa)
      localStorage.setItem('lista', JSON.stringify(this.tarefas))
    },
    trocarTema(modoEscuroAtivo : boolean){
      this.darkTheme = modoEscuroAtivo
    },
    // deletarTarefa(key : ITarefa){
    //   console.log(key)

    // }
    deletarTarefa(id : number){
      console.log('Olha aqui' , id)

      let filtro = this.tarefas.filter((item) => {
        return item.id !== id;
      }); 

      localStorage.setItem('lista', JSON.stringify(filtro))

      return (this.tarefas = filtro);
    }
  }
});
</script>

<style scoped>
.lista {
  padding: 1.25rem;
}

main {
  --bg-primario: #fff;
  --texto-primario: #000;
  --cronometro: #000
}

/* Quando existir uma classe modo-escuro, vai alterar o valor das variaveis acima */
main.modo-escuro {
  --bg-primario: #2b2d42;
  --texto-primario: #ddd;
  --cronometro: #F29F05

}

.conteudo {
  background-color: var(--bg-primario);
}

</style>
