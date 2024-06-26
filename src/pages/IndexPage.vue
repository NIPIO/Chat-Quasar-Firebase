<template>
  <q-page v-if="!userGoogle">
    <h3 class="text-center text-secondary"> Debes iniciar sesión </h3>
  </q-page>
  <q-page v-else>
    <PageChat />
  </q-page>
</template>

<script setup>
import { inject } from "vue";
import PageChat from "components/PageChatComponent.vue";

const userGoogle = inject("userGoogle");

</script>
