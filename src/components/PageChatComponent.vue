<template>
  <q-page>
    <div class="q-pa-md row justify-center" ref="chatRef">
      <div style="width: 100%; max-width: 600px">
        <template
          v-for="message in messages"
          :key="message.id"
        >
          <q-chat-message
            :text="[message.text]"
            :sent="message.uid === auth.currentUser.uid"
            :name="message.displayName"
          />
        </template>
      </div>
    </div>
  </q-page>
</template>

<script setup>
import { collection, query, onSnapshot, orderBy } from "firebase/firestore";
import { db, auth } from "src/firebase";
import { inject, ref } from "vue";


const userGoogle = inject("userGoogle");
const messages = ref([]);
const chatRef = ref(null);
const q = query(collection(db, "chats"), orderBy("time", "asc"));
const unsubscribe = onSnapshot(q, (snapshot) => {
  if (userGoogle.value) {
    snapshot.docChanges().forEach((change) => {
      if (change.type === "added") {
        messages.value.push({
          id: change.doc.id,
          ...change.doc.data()
        });

        setTimeout(() => {
          if (chatRef.value !== null) {
            //Reposicionamiento del chat
            window.scrollTo(0, chatRef.value.scrollHeight);
          }
        }, 0);
      }
    });
  }

});


</script>
