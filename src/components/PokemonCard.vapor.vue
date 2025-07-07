<template>
    <div class="card">
        <img :src="props.pokemon.sprites.front_default" :alt="props.pokemon.name" />
        <h2>{{ props.pokemon.name }}</h2>
        <p>types: <span v-for="t in props.pokemon.types" :key="t.slot">{{ t.type.name }}</span></p>
        <p>abilities: <span v-for="a in props.pokemon.abilities" :key="a.slot">{{ a.ability.name }}</span></p>
    </div>
</template>

<script setup vapor>
    const props = defineProps({
        pokemon: Object
    })
</script>

<style scoped>
    .card {
        max-width: 320px;
        width: 100%;
        margin: 0 auto;
        padding: 1rem;
        border: 1px solid #ddd;
        border-radius: 8px;
        box-shadow: 0 2px 6px rgba(0,0,0,0.1);
        text-align: center;
        box-sizing: border-box;
    }

    .card img {
        width: 100px;
        height: 100px;
    }

    @media (max-width: 320px) {
        .card {
            padding: 0.5rem;
        }
        .card img {
            width: 80px;
            height: 80px;
        }
    }
</style>

