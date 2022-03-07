<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";
import useAuth from "../composable/useAuth";
import useError from "../composable/useError";


const { isAuthenticated, login } = useAuth();
const username = ref("");
const password = ref("");

const router = useRouter();

const logginIn = () => {
    login(username.value, password.value);
    if (isAuthenticated.value) {
        router.push("/");
    } else {
        setError("Invalid user or password");
        start();
    }
};

const {error, setError } = useError();
import { promiseTimeout, useTimeout } from "@vueuse/core";

const { ready, start } = useTimeout(3000, { controls: true });

</script>




<template>
<div class="flex justify-center flex-col space-y-12 items-center min-h-screen-nonav">
    Logged in: {{ isAuthenticated}}
<div class=" bg-gray-300 shadow-2xl justify-center overflow-hidden items-center rounded-lg flex">
<img class="h-64" src="../assets/bglogin.png" alt="Hello BG">
<form @submit.prevent="logginIn" class="flex flex-col space-y-4 p-4">
    <input type="text" class="border-2 p-2 rounded-lg " placeholder="UserName" v-model="username" />
    <input type="password" class="border-2 p-2 rounded-lg" placeholder="Password" v-model="password" />
    <button type="submit" @submit.prevent="logginIn" class="bg-pink-500 rounded-lg text-gray-500 py-2">Login</button>
</form>
</div>
<div
v-if="!ready && error"
 class="bg-red-300  w-1/4 p-4 text-red-800 rounded-lg absolute bottom-2 right-2 text-center">
    {{error}}
</div>
</div>
</template>