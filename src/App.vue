<script setup lang="ts">
import { Authenticator } from "@aws-amplify/ui-vue";
import "@aws-amplify/ui-vue/styles.css";
import dashboard from './components/Dashboard.vue';
</script>

<template>
  <main>
    <authenticator  :sign-up-attributes="['given_name', 'family_name']">
      <template v-slot="{ user, signOut }">
        <dashboard />
        <button @click="signOut">Sign Out</button>
      </template>
    </authenticator>
  </main>
</template>

