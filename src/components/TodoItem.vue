<template>
    <div class="todo">
        <p>{{ isCompleted === true ? "Completed" : "Active" }}</p>
         <p>{{ task }}</p>
      <button @click="$emit('deleteTodo')">Delete</button>
    </div>
</template>

<script setup lang="ts">
interface Props {
    task: string;
    isCompleted: boolean;
}
const props = defineProps<Props>();

interface Emits {
    (e: "deleteTodo"): void;
}

const emit =  defineEmits<Emits>()


</script>

<style>

</style>