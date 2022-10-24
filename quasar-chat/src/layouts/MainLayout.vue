<template>
  <q-layout view="hhr LpR lFr">
    <Navbar />

    <q-page-container>
      <router-view />
    </q-page-container>

    <Footer></Footer>
  </q-layout>
</template>

<script setup>
import Navbar from "src/components/Navbar.vue";
import { inject } from "vue";
import Footer from "src/components/Footer.vue";

const userGoogle = inject("userGoogle");
</script>
