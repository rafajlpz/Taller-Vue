<template>
  <q-layout view="hhr LpR lFr">
    <Navbar />

    <q-page-container>
      <router-view />
    </q-page-container>

    <Footer v-if="userGoogle"></Footer>
  </q-layout>
</template>

<script setup>
import { inject } from "vue";
import Navbar from "src/components/Navbar.vue";
import Footer from "src/components/Footer.vue";

const userGoogle = inject("userGoogle");
</script>
