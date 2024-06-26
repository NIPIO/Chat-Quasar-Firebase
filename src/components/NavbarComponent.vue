<template>
  <q-header elevated class="bg-secondary text-white" height-hint="98">
    <q-toolbar>
      <q-toolbar-title>
        <q-avatar>
          <img alt=""
               src="https://cdn.quasar.dev/logo-v2/svg/logo-mono-white.svg">
        </q-avatar>
        Quasar Chat
      </q-toolbar-title>
      <q-btn label="Ingresar"
             v-if="!userGoogle"
             color="positive"
             @click="accessGoogle" />


      <q-btn v-if="userGoogle" dense flat round icon="menu" @click="toggleRightDrawer" />
    </q-toolbar>
  </q-header>

  <UserInfoComponent v-if="userGoogle" v-model="rightDrawerOpen" />
</template>

<script setup>

import { inject, ref } from "vue";
import { GoogleAuthProvider, signInWithPopup, signOut } from "firebase/auth";
import { auth } from "src/firebase";
import UserInfoComponent from "components/UserInfoComponent.vue";

const rightDrawerOpen = ref(false);

const userGoogle = inject("userGoogle");

const toggleRightDrawer = () => {
  rightDrawerOpen.value = !rightDrawerOpen.value;
};

const accessGoogle = () => {
  const provider = new GoogleAuthProvider();
  signInWithPopup(auth, provider)
    .catch(err => console.log(err));
};

const logoutGoogle = () => {
  signOut(auth)
    .catch(err => console.log(err));
};

</script>
