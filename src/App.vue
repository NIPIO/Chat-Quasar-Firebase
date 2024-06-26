<template>
  <router-view />
</template>

<script setup>
import { onAuthStateChanged } from "firebase/auth";
import { auth } from "./firebase"
import { provide, ref } from "vue";

const userGoogle = ref()
provide('userGoogle', userGoogle)

onAuthStateChanged(auth, (user) => {
  userGoogle.value = user
  // if (user) {
  //   // User is signed in, see docs for a list of available properties
  //   // https://firebase.google.com/docs/reference/js/auth.user
  //   const uid = user.uid;
  //   // ...
  // } else {
  //   // User is signed out
  //   // ...
  // }
});

</script>
