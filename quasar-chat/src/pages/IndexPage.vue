<template>
  <q-page v-if="!userGoogle">
    <h3 class="text-center text-secondary">Debes iniciar sesion</h3>
  </q-page>

  <q-page v-else padding>
    <div class="q-pa-md row justify-center">
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
import { inject } from "vue";
import { auth, db } from "src/firebase";
import { ref } from "vue";

const q = query(collection(db, "chats"), orderBy("time"));
const unsubscribe = onSnapshot(q, (snapshot) => {
  // if (userGoogle.value) {
    snapshot.docChanges().forEach((change) => {
      if (change.type === "added") {
        console.log("Nuevo chat: ", change.doc.data());
        messages.value.push({
          id: change.doc.id,
          ...change.doc.data(),
        });
      }
    });
  
});

const userGoogle = inject("userGoogle"); // Traemos la sesion activa
const messages = ref([]);
</script>
