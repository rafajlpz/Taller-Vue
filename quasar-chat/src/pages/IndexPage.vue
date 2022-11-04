<template>
  <q-page v-if="!userGoogle">
    <h3 class="text-center text-secondary">Debes iniciar sesion</h3>
  </q-page>

  <q-page v-else padding>
    <div class="q-pa-md row justify-center scrollChat" ref="chatRef">
      <div style="width: 100%; max-width: 400px">
        <template v-for="message in messages" :key="message.id">
          <q-chat-message
            :text="[message.text]"
            :sent="message.uid == auth.currentUser.uid"
            :name="message.displayName"
          />
        </template>
      </div>
    </div>
  </q-page>
</template>

<script setup>
import { collection, query, onSnapshot, orderBy } from "firebase/firestore";

import { auth, db } from "src/firebase";
import { ref, nextTick, inject, watchEffect } from "vue";

const userGoogle = inject("userGoogle"); // Traemos la sesion activa
const messages = ref([]);
const chatRef = ref(null);

watchEffect((onCleanup) => {
  if (userGoogle.value) {
    const q = query(collection(db, "chats"), orderBy("time"));
    const unsubscribe = onSnapshot(q, (snapshot) => {
      snapshot.docChanges().forEach(async (change) => {
        if (change.type === "added") {
          
          messages.value.push({
            id: change.doc.id,
            ...change.doc.data(),
          });
          await nextTick();
          chatRef.value.scrollTo(0, chatRef.value.scrollHeight);
        }
      });
    });
    onCleanup(unsubscribe)
  }
});
</script>

<style>
.scrollChat {
  height: calc(100vh - (60px + 60px));
  overflow-y: scroll;
}
</style>
