<template>
    <div class="search">
        <input
            v-model="query"
            @keyup.enter="onSearch"
            placeholder="enter name or id"
        />
        <button @click="onSearch">search</button>
    </div>
</template>

<script setup vapor>
    import { ref } from 'vue'
    const query = ref('')
    const emit  = defineEmits(['searched'])

    function onSearch() {
        if (!query.value) return
        emit('searched', query.value.trim().toLowerCase())
    }
</script>

<style scoped>
    .search {
        display: flex;
        justify-content: center;
        margin-bottom: 1rem;
        gap: 0.5rem;
        flex-wrap: wrap;
    }

    .search input {
        flex: 1 1 50px;
        min-width: 0;
        padding: 0.5rem;
        font-size: 1rem;
        border: 1px solid #ccc;
        border-radius: 4px 0 0 4px;
    }

    .search button {
        flex: 0 0 auto;
        padding: 0.5rem 1rem;
        border: none;
        background-color: #ffcb05;
        cursor: pointer;
        border-radius: 0 4px 4px 0;
    }

    @media (max-width: 400px) {
        .search {
            flex-wrap: nowrap;
            gap: 0.25rem;
        }

        .search input {
            padding: 0.25rem 0.5rem;
            font-size: 0.9rem;
            flex: 1 1 auto;
        }

        .search button {
            padding: 0.25rem 0.5rem;
            font-size: 0.9rem;
            flex: 0 0 auto;
        }
    }
</style>



