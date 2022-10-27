<template>
  <q-footer elevated class="bg-grey-8 text-white">
    <q-toolbar>
      <q-input
        class="full-width"
        dark
        dense
        standout
        v-model="text"
        label="Ingresar texto"
        @keyup=""
      >
        <template v-slot:append>
          <q-icon
            name="send"
            class="cursor-pointer"
            type="submit"
            @click="addText"
          />
        </template>
      </q-input>
    </q-toolbar>
  </q-footer>
</template>

<script setup>
import { ref } from "vue";
import { collection, addDoc } from "@firebase/firestore";
import { db, auth } from "src/firebase";

const text = ref("");

const addText = () => {
  console.log(text.value);
  addDoc(collection(db, "chats"), {
    text: text.value,
    uid: auth.currentUser.uid,
    time: Date.now(),
    displayName: auth.currentUser.displayName,
  })
    .then(() => console.log("Sonido"))
    .catch((e) => console.log(e));
};
</script>
