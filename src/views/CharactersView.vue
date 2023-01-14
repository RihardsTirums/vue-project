<template>
    <div>Characters page</div>
    <div v-if="state.isLoading" class="loading">LOADING...</div>
    <ul v-else>
        <li v-for="character in state.characters" :key="character.id">
            {{ character.id }}
            {{ character.name }}
            {{ character.status }}
            {{ character.species }}
            {{ character.type }}
            <img :src="character.image" alt="character image">
        </li>
    </ul>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { onMounted } from 'vue';
import { reactive } from 'vue';

interface Character {
    id: number;
    name: string;
    status: string;
    species: string;
    type: string;
    image: string;
}

const url = ref("https://rickandmortyapi.com/api/character/"); 

const state = reactive({
    characters: [] as Character[],
    isLoading: false,
})

onMounted(() => {
    state.isLoading = true;
    setTimeout(() => {
        fetch(url.value)
        .then(response => response.json())
        .then((data) => {
            state.characters = data.results;
            state.isLoading = false;
        })
        .catch(() => {
            state.isLoading = false;
        });
    }, 7000);
});



</script>

<style>
.loading {
    background-color: red;
}
img {
    width: 150px;
    height: 150px;
}

</style>