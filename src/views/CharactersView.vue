<template>
    <div class="container">
        <h2 class="text-center mb-3 text-uppercase text-style mx-auto">Characters page</h2>
        <div v-if="state.isLoading" class="loading lds-hourglass d-flex mx-auto">LOADING...</div>
            <ul v-else class="ms-4">
                <li v-for="character in state.characters" :key="character.id" class="card m-2 ms-5 p-3 rounded-0 shadow cards-style text-white fs-4" style="width:10em;">
                    <img :src="character.image" alt="character image">
                    {{ character.id }}
                    {{ character.name }}
                    {{ character.status }}
                    {{ character.species }}
                    {{ character.type }}
                </li>
            </ul>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { onMounted } from 'vue';
import { reactive } from 'vue';
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap/dist/js/bootstrap.js'


onMounted(() => {
    fetchCharacters(url.value);
});

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

const fetchCharacters = (url:string) => {
    state.isLoading = true;
    setTimeout(() => {
        fetch(url)
        .then(response => response.json())
        .then((data) => {
            state.characters = data.results;
            state.isLoading = false;
        })
        .catch(() => {
            state.isLoading = false;
        });
    }, 7000);
}

</script>

<style>
.loading{
    color: white;
    font-size: 30px;
    font-weight: bold;
    text-shadow: 2px 2px 4px #000000;
}

.lds-hourglass {
  display: inline-block;
  position: relative;
  width: 80px;
  height: 80px;
}
.lds-hourglass:after {
  content: " ";
  display: block;
  border-radius: 50%;
  width: 0;
  height: 0;
  margin-left: 8px;
  box-sizing: border-box;
  border: 32px solid #fff;
  border-color: rgb(0, 212, 0) transparent rgb(0, 3, 177) transparent;
  animation: lds-hourglass 1.2s infinite;
}
@keyframes lds-hourglass {
  0% {
    transform: rotate(0);
    animation-timing-function: cubic-bezier(0.55, 0.055, 0.675, 0.19);
  }
  50% {
    transform: rotate(900deg);
    animation-timing-function: cubic-bezier(0.215, 0.61, 0.355, 1);
  }
  100% {
    transform: rotate(1800deg);
  }
}

img {
    width: 100px;
    height: 100px;
    margin-top: 8px;
    border: 0.5px solid white;
    border-radius: 5rem;
}

.cards-style{
    display:inline-block;
    background-color: rgba(42, 71, 44, 0.555);
    border: 0.5px solid rgb(2, 112, 66);
}

.text-style{
    color: rgb(0, 169, 199);
    font-size: 30px;
    font-weight: bold;
    text-shadow: 2px 2px 4px #000000;
}


</style>