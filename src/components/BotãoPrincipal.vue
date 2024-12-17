<script lang="ts">
    export default {
    props: {
        texto: { type: String, required: true },
    }
    }
</script>

<template>
    <button class="paragrafo-lg botao-principal">
        {{ texto }}
    </button>
</template>


<style scoped>
    .botao-principal {
        background-color: var(--coral, #F0633C);
        color: white;
        border-radius: 50px;
        width: 250px;
        padding: 18px;
        font-weight: 700;
    }
</style>