<template>
  <q-header elevated class="bg-primary text-white">
    <q-toolbar>
      <q-toolbar-title>
        <q-avatar>
          <img src="https://cdn.quasar.dev/logo-v2/svg/logo-mono-white.svg" />
        </q-avatar>
        QuasarChatBot
      </q-toolbar-title>

      <q-btn
        label="Ingresar"
        color="warning"
        @click="accesGoogle"
        v-if="!userGoogle"
      ></q-btn>
      <q-btn
        label="Salir"
        color="warning"
        @click="logoutGoogle"
        v-if="userGoogle"
      ></q-btn>

      <q-btn
        dense
        flat
        round
        icon="menu"
        @click="toggleRightDrawer"
        v-if="userGoogle"
      />
    </q-toolbar>
  </q-header>

  <q-drawer
    show-if-above
    v-model="rightDrawerOpen"
    side="right"
    bordered
    v-if="userGoogle"
  >
    <!-- drawer content -->
  </q-drawer>
</template>

<script setup>
import { ref, inject } from "vue";
import { GoogleAuthProvider, signInWithPopup, signOut } from "firebase/auth";
import { auth } from "src/firebase";

const userGoogle = inject("userGoogle");
const rightDrawerOpen = ref(false);
const toggleRightDrawer = () => {
  rightDrawerOpen.value = !rightDrawerOpen.value;
};

const accesGoogle = () => {
  const provider = new GoogleAuthProvider();
  signInWithPopup(auth, provider).catch((e) => console.log(e));
};
const logoutGoogle = () => {
  signOut(auth).catch((e) => console.log(e));
};
</script>
