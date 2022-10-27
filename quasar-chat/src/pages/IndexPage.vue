<template>
  <q-page v-if="!userGoogle">
    <h3 class="text-center text-secondary">Debes iniciar sesion</h3>
  </q-page>

  <q-page v-else padding>
    <div class="q-pa-md row justify-center">
      <div style="width: 100%; max-width: 400px">
        <q-chat-message :text="['hey, how are you?']" sent name="rafajlpz" />
        <q-chat-message :text="['doing fine, how r you?']" name="xaxa" />
      </div>
    </div>
  </q-page>
</template>

<script setup>
import { collection, query, onSnapshot } from "firebase/firestore";
import { inject } from "vue";
import { db } from "src/firebase";

const q = query(collection(db, "chats"));
const unsubscribe = onSnapshot(q, (snapshot) => {
  snapshot.docChanges().forEach((change) => {
    if (change.type === "added") {
        console.log("Nuevo chat: ", change.doc.data());
        messages.value.push ({
          id: change.doc.id,
          ...change.doc.data(),
        })
    }
  });
});

const userGoogle = inject("userGoogle"); // Traemos la sesion activa
const messages = ref([])
</script>
