<template>
  <q-footer elevated class="bg-secondary">
    <q-toolbar>
      <q-input
        class="full-width"
        dark
        dense
        standout
        label="Escriba su mensaje"
        @keyup.enter="sendText"
        v-model="text">
        <template v-slot:append>
          <q-icon
            name="send"
            type="submit"
            class="cursor-pointer"
            @click="sendText"
          />
        </template>
      </q-input>
    </q-toolbar>
  </q-footer>
</template>


<script setup>
import { addDoc, collection } from "firebase/firestore";
import { ref } from "vue";
import { db, auth } from "src/firebase";

const text = ref("");
const sendText = () => {
  addDoc(collection(db, "chats"), {
    text: text.value,
    uid: auth.currentUser.uid,
    time: Date.now(),
    displayName: auth.currentUser.displayName
  }).then(() => {
    text.value = "";
  }).catch(err => console.log(err));


};
</script>
