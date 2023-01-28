<template>
    <div class="form-wrapper">
    <form @submit.prevent="handleSubmit" class="form">
        <CustomInput
            id="name"
            v-model:inputValue="state.name.value"
            label="Name"
            class="red"
            :error="state.name.error"
            isRequired
            />
            <CustomInput
            id="email"
            v-model:inputValue="state.email.value"
            :error="state.email.error"
            label="Email"
            :isRequired="true"
            />
            <div class="checkbox-wrapper">
                <input type="checkbox" id="checkbox" v-model="state.terms.value"/>
            <label for="checkbox">Confirm terms</label>
            </div>
            <button type="submit" :disabled="!state.terms.value || isLodaing">Submit</button>
            <div class="succses" v-if="succsesMessage">{{ succsesMessage }} <button @click="succsesMessage = ''">Send Again</button></div>
    </form>
    </div>
</template>

<script lang="ts" setup>
import { reactive, ref } from 'vue';
import CustomInput from '../components/CustomInput.vue';
import  axios from 'axios';

const url = 'https://jsonplaceholder.typicode.com/posts';

const state = reactive({
    name: {
        value: '',
        error: '',
    },
    email: {
        value: '',
        error: '',
    },
    terms: {
        value: false,
        error: '',
    },
});

const userId = ref(1);
const succsesMessage = ref('');
const isLodaing = ref(false);

const isValidName = () => {
    if (!state.name.value) {
        state.name.error = 'Name is required';
        return false;
    } 
    if (state.name.value.length < 3) {
        state.name.error = 'Name is too short';
        return false;
    }
    state.name.error = '';
    return true;
};

const isValidEmail = () => {
    if (!state.email.value) {
        state.email.error = 'Email is required';
        return false;
    } 
    let email = new RegExp (/^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/);
    const isEmailValid = email.test(state.email.value);
    if (!isEmailValid) {
        state.email.error = 'Email is not valid';
        return false;
    }
    return true;
};

const submitData = async () => {
    const payload = {
        title: state.name.value,
        body: state.email.value,
        userId: userId.value,
    };
    try {
        isLodaing.value = true;
        setTimeout(() => {
            isLodaing.value = false;
        }, 2000);
        const response = await axios.post(url, payload);
        console.log("response",response);
        userId.value++;
        state.name.value = '';
        state.email.value = '';
        state.terms.value = false;

        succsesMessage.value = 'Data was sent';
        isLodaing.value = false;
    } catch (error) {
        console.log("error",error);
        isLodaing.value = false;
    }
    
};


const handleSubmit = () => {

    const isNameValid = isValidName();
    const isEmailValid = isValidEmail();
    
    if (!isNameValid || !isEmailValid) {
        return;
    }

    submitData();
};
</script>

<style>

@keyframes animateIn {
    0% {
        opacity: 0%;
    }
    30% {
        opacity: 60%;
    }
    100% {
        opacity: 100%;
    }
}
.succses {
    color: green;
    position: absolute;
    font-size: 40px;
    bottom: 300px;
    animation: animateIn 2s;
    flex-direction: column;
}
.checkbox-wrapper {
    display: inline-flex;
    align-items: center;
    margin-bottom: 16px;
    column-gap: 8px;
}
.form-wrapper {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
}
.form {
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
    width: 100%;
    max-width: 400px;
}
</style>