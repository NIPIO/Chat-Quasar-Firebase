<template>
  <q-layout view="hHr lpR fFr">
    <NavbarComponent />
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import NavbarComponent from "components/NavbarComponent.vue";
</script>
