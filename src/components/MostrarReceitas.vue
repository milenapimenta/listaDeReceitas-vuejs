<script lang="ts">
import { obterReceitas } from '@/http';
import type IReceita from '@/interfaces/IReceitas';
import CardReceitas from './CardReceitas.vue';
import BotãoPrincipal from './BotãoPrincipal.vue';
import type { PropType } from 'vue';
import { itensDeLista1EstaoEmLista2 } from '@/operacoes/listas';

    export default {
        props: {
            ingredientes: { type: Array as PropType<string[]>, required: true }
        },
        data() {
            return {
                receitasEncontradas: [] as IReceita[],
            }
        },
        async created() {
            const receitas = this.receitasEncontradas = await obterReceitas();

            this.receitasEncontradas = receitas.filter(receita => {
                const possoFazerReceita = itensDeLista1EstaoEmLista2(receita.ingredientes, this.ingredientes);
                return possoFazerReceita;
            });

        },
        components: {BotãoPrincipal, CardReceitas},
        emits: ['editarReceitas']
    }
</script>

<template>
    <section class="mostrar-receitas">
        <h1 class="cabecalho titulo-receitas">Receitas</h1>

        <p class="paragrafo-lg resultados-encontrados">
            Resultados encontrados: {{ receitasEncontradas.length }}
        </p>

        <div v-if="receitasEncontradas.length" class="receitas-wrapper">
        <p class="paragrafo-lg informacoes">
            Veja as opções de receitas que encontramos com os ingredientes que você tem por aí!
        </p>

        <ul class="receitas">
            <li v-for="receita of receitasEncontradas" :key="receita.nome">
            <CardReceitas :receita="receita" />
            </li>
        </ul>
        </div>

        <div v-else class="receitas-nao-encontradas">
        <p class="paragrafo-lg receitas-nao-encontradas__info">
            Ops, não encontramos resultados para sua combinação. Vamos tentar de novo?
        </p>

        <img src="../assets/imagens/sem-receitas.png"
            alt="Desenho de um ovo quebrado. A gema tem um rosto com uma expressão triste.">
        </div>

        <BotãoPrincipal texto="Editar receitas" @click="$emit('editarReceitas')" />
    </section>
</template>

<style scoped>
    .mostrar-receitas {
        display: flex;
        flex-direction: column;
        align-items: center;
        text-align: center;
        width: 80%;
    }

    .titulo-receitas {
        color: var(--verde-medio, #3D6D4A);
        margin-bottom: 1.5rem;
    }

    .resultados-encontrados {
        color: var(--verde-medio, #3D6D4A);
        margin-bottom: 0.5rem;
    }

    .receitas-wrapper {
        margin-bottom: 3.5rem;
    }

    .informacoes {
        margin-bottom: 2rem;
    }

    .receitas {
        display: flex;
        justify-content: center;
        gap: 1.5rem;
        flex-wrap: wrap;
    }

    .receitas-nao-encontradas {
        margin-bottom: 2rem;
    }

    .receitas-nao-encontradas__info {
        margin-bottom: 0.5rem;
    }

    @media only screen and (max-width: 767px) {
        .receitas-wrapper {
        margin-bottom: 2rem;
        }
    }
</style>