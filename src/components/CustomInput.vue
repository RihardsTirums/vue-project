<template>
    <div class="input-wrapper">
        <label :for="props.id">{{ props.label }} <span class="required" v-if="props.isRequired">*</span></label>
        <input
            type="text"
            v-bind="$attrs"
            :value="inputValue"
            @input="updateValue"
            :id="props.id"
            :placeholder="props.placeholder"
            />
            <p v-if="error" class="error">{{ error }}</p>
    </div>
</template>

<script lang="ts" setup>
import { defineComponent } from 'vue';

interface Props {
    id: string;
    inputValue: string;
    placeholder?: string;
    label?: string;
    error?: string;
    isRequired?: boolean;
}

interface Emits {
    (e: 'update:inputValue', newValue: string): void;
}

const emit = defineEmits<Emits>();

const props = withDefaults(defineProps<Props>(), {
    isRequired: false,
});

const updateValue = (e: Event) => {
    emit('update:inputValue', (e.target as HTMLInputElement).value);
};
</script>

<script lang="ts">
export default defineComponent({
    inheritAttrs: false,
});
</script>

<style scoped>
input {
    width: 100%;
    padding: 0.5em;
    border: 1px solid #ccc;
    border-radius: 0.25em;
    margin-bottom: 0.5em;
    width: 100%;
    max-width: 400px;
}
p{
    color: red;
}
.required {
    color: red;
}
.input-wrapper {
    display: flex;
    flex-direction: column;
    row-gap: 0.5em;
    margin-bottom: 1em;
    align-items: start;
}
</style>

