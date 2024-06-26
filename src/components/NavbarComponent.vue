<template>
  <q-header elevated class="bg-primary text-white" height-hint="98">
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
             color="primary"
             @click="accessGoogle" />

      <q-btn label="Salir"
             v-if="userGoogle"
             color="primary"
             @click="logoutGoogle" />

      <q-btn dense flat round icon="menu" @click="toggleRightDrawer" />
    </q-toolbar>
  </q-header>

  <q-drawer show-if-above v-model="rightDrawerOpen" side="right" bordered>
    <!-- drawer content -->
  </q-drawer>

</template>

<script>

import { inject, ref } from "vue";
import { GoogleAuthProvider, signInWithPopup, signOut } from "firebase/auth";
import { auth, db } from "src/firebase";


export default {
  name: "NavbarComponent",
  setup() {
    const rightDrawerOpen = ref(false);

    const userGoogle = inject('userGoogle')

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
    return {
      rightDrawerOpen,
      toggleRightDrawer,
      accessGoogle,
      logoutGoogle,
      userGoogle

    };
  }
};

</script>
