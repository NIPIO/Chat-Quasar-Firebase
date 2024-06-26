<template>
  <q-layout view="hHr lpR fFr">
    <NavbarComponent />
    <q-page-container>
      <router-view />
      <InputChat v-if="userGoogle" />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import NavbarComponent from "components/NavbarComponent.vue";
import InputChat from "components/InputChatComponent.vue";
import { inject } from "vue";

const userGoogle = inject('userGoogle')
</script>
