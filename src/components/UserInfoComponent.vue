<template>
  <q-drawer
    :width="200"
    :breakpoint="400"
    side="right">
    <q-scroll-area style="height: calc(100% - 150px); margin-top: 150px; border-right: 1px solid #ddd">
      <q-list padding>
        <q-item clickable v-ripple>
          <q-btn label="Salir"
                 v-if="auth"
                 color="negative"
                 @click="logoutGoogle" />
        </q-item>
      </q-list>
    </q-scroll-area>

    <q-img class="absolute-top" src="https://cdn.quasar.dev/img/material.png" style="height: 150px">
      <div class="absolute-bottom bg-transparent">
        <q-avatar size="56px" class="q-mb-sm">
          <img alt="" :src="auth.currentUser.providerData[0].photoURL">
        </q-avatar>
        <div class="text-weight-bold">{{ auth.currentUser.displayName }}</div>
        <div>{{ auth.currentUser.email }}</div>
      </div>
    </q-img>


  </q-drawer>
</template>

<script setup>
import { signOut } from "firebase/auth";
import { auth } from "src/firebase";

console.log();
const logoutGoogle = () => {
  signOut(auth)
    .catch(err => console.log(err));
};
</script>
