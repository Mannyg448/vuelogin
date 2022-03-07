<script setup>
import useAuth from "../composable/useAuth";
const { isAuthenticated, user } = useAuth();
 </script>




<template>
<div class="flex justify-center flex-col space-y-12 items-center min-h-screen-nonav">
    <h2 v-if="!isAuthenticated" class="text-gray-500 font-extralight text-6xl">Welcome</h2>
     <h2 v-else class="text-gray-500 font-extralight text-6xl">Welcome {{user}}</h2>
<img src="../assets/bgindex.png" alt="Hello BG">
</div>
</template>