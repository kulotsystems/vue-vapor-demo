<template>
    <div id="app">
        <h1>PokéFinder</h1>

        <PokemonSearch @searched="fetchPokemon" />

        <div v-if="loading" class="status">loading…</div>
        <div v-else-if="error" class="status error">{{ error }}</div>
        <PokemonCard v-else-if="pokemon" :pokemon="pokemon" />
    </div>
</template>

<script setup vapor>
    import { ref } from 'vue'
    import PokemonSearch from './components/PokemonSearch.vapor.vue'
    import PokemonCard   from './components/PokemonCard.vapor.vue'

    const pokemon = ref(null)
    const loading = ref(false)
    const error   = ref(null)

    async function fetchPokemon(nameOrId) {
        loading.value = true
        error.value   = null
        pokemon.value = null

        try {
            const res  = await fetch(`https://pokeapi.co/api/v2/pokemon/${nameOrId}`)
            if (!res.ok) throw new Error('not found')
            pokemon.value = await res.json()
        }
        catch (err) {
            error.value = 'could not load that Pokémon'
        }
        finally {
            loading.value = false
        }
    }
</script>

<style scoped>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        text-align: center;
        margin: 2rem auto;
        max-width: 400px;
        padding: 0 1rem;
        box-sizing: border-box;
    }
    h1 {
        color: #3b4cca;
        margin-bottom: 1rem;
    }
    .status {
        margin-top: 1rem;
        font-size: 1.1rem;
        word-break: break-word;
    }
    .error {
        color: #d32f2f;
    }

    @media (max-width: 320px) {
        #app {
            margin: 1rem auto;
        }
    }
</style>
