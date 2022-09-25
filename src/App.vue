<template>
  <main class="columns is-gapless is-multiline" :class="{ 'modo-escuro':modoEscuroAtivo}">

    <div class="column is-one-quarter">
      <barraLateral @aoTemaAlterado="trocarTema" />
    </div>
    <div class="column is-three-quarter conteudo">
      <FormTarefa @aoSalvarTarefa="salvarTarefa" />
      <div class="lista">
        <Tarefa v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa" />
        <Box v-if="listaVazia">
          Você não tem tarefas!
        </Box>
      </div>
    </div>

  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import barraLateral from './components/BarraLateral.vue';
import FormTarefa from './components/form.vue';
import Tarefa from './components/Tarefa.vue'
import ITarefa from './interfaces/ITarefea'
import Box from './components/Box.vue';

export default defineComponent({
  name: "App",
  components: { barraLateral, FormTarefa, Tarefa, Box },
  data() {
    return {
      tarefas: [] as ITarefa[],
      modoEscuroAtivo: false

    }
  },
  methods: {
    salvarTarefa(tarefa: ITarefa) {
      this.tarefas.push(tarefa);
    },
    trocarTema(modoEscuroAtivo: boolean) {
      this.modoEscuroAtivo = modoEscuroAtivo;
    }
  },
  computed: {
    listaVazia(): boolean {
      return this.tarefas.length === 0
    }
  }


});
</script>

<style>
.lista {
  padding: 1.25rem;
}

main {
  --bg-primario: #ffff;
  --texto-primario: #000;
}

main.modo-escuro {
  --bg-primario: #2b2d42;
  --texto-primario: #ddd;
}

.conteudo {
  background-color: var(--bg-primario);
}
</style>
