<script lang="ts">
import { getCategorias } from '@/http/index';
import type ICategoria from '@/interfaces/ICategorias';
import CardCategoria from './CardCategoria.vue';
import BotaoPrincipal from './BotaoPrincipal.vue';

export default{
  name: 'SelecionarIngredientes',
  components: {CardCategoria, BotaoPrincipal},
  emits: ['adicionarIngrediente','removerIngrediente', 'buscarReceitas'],

  data() {
      return {
          categorias: [] as ICategoria[]
      }
  },
  async created(){
    this.categorias = await getCategorias();
  }
}
</script>

<template>
    <section class="selecionar-ingredientes">
        <h1 class="cabecalho titulo-ingredientes">ingredientes</h1>
        <p class="paragrafo-lg instrucoes">Selecione abaixo os ingredientes que você quer usar nesta receita:</p>

        <ul class="categorias">
            <li v-for="categoria in categorias" v-bind:key="categoria.nome">
                <CardCategoria :categoria="categoria"
                  v-on:adicionar-ingrediente="$emit('adicionarIngrediente', $event)"
                  v-on:remover-ingrediente="$emit('removerIngrediente', $event)"
                />
            </li>
        </ul>
        
        <p class="paragrafo dica">*Atenção: consideramos que você tem em casa sal, pimenta e água.</p>

        <BotaoPrincipal texto="Buscar" v-on:click="$emit('buscarReceitas')" />
    </section>
</template>

<style scoped>
.selecionar-ingredientes {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.titulo-ingredientes {
  color: var(--verde-medio, #3D6D4A);
  display: block;
  margin-bottom: 1.5rem;
}

.instrucoes {
  margin-bottom: 2rem;
}

.categorias {
  margin-bottom: 1rem;
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.dica {
  align-self: flex-start;
  margin-bottom: 3.5rem;
}

@media only screen and (max-width: 767px) {
  .dica {
    margin-bottom: 2.5rem;
  }
}

</style>