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
      >
        <template v-slot:append>
          <q-icon name="send" class="cursor-pointer" />
        </template>
      </q-input>
    </q-toolbar>
  </q-footer>
</template>

<script setup>
import { ref } from "vue";
const text = ref("");
</script>
