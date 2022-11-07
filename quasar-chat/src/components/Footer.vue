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
        @keyup.enter="addText"
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
  
  if(!text.value.trim()){
    text.value = "";

    return console.log('mostrar alerta de mensaje vacio')
  }
  addDoc(collection(db, "chats"), {
    text: text.value,
    uid: auth.currentUser.uid,
    time: Date.now(),
    displayName: auth.currentUser.displayName,
  })
    .then(() => {
      console.log("Sonido");
      text.value = "";
    })

    .catch((e) => console.log(e));
};
</script>
