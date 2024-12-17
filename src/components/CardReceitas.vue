<script lang="ts">
import type { PropType } from 'vue';
import IngredienteSelecionavel from './IngredienteSelecionavel.vue';
import type ICategoria from '@/interfaces/ICategoria';

    export default {
        props: {
            receita: { type: Object as PropType<ICategoria> , required: true }
        },
        components: { IngredienteSelecionavel },
        emits: ['adicionarIngrediente', 'removerIngrediente']
    }
</script>

<template>
    <div class="receita">
        <div class="receita__cabecalho">
            <img :src="`/imagens/receitas/${receita.imagem}`" alt="" class="receita__imagem">
            <p class="paragrafo receita__nome">
                {{receita.nome}}
            </p>
        </div>
    </div>
</template>

<style scoped>
    .receita {
      width: 19.5rem;
      border-radius: 1rem;
      background: var(--branco, #FFF);
      box-shadow: 4px 4px 10px 0px rgba(68, 68, 68, 0.05);
      height: 100%;
      display: flex;
      align-items: center;
      gap: 2rem;
    }

    .receita__cabecalho {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 0.5rem;
    }

    .receita__imagem {
      width: 19.5rem !important;
      border-radius: 1rem 1rem 0rem 0rem;
      object-fit: cover;
    }

    .receita__nome {
      text-align: center;
      font-weight: 700;
      padding: 2rem;
    }
</style>
