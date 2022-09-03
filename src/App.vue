<template>
  <div>
    <NavBar />
    <ContactsList />
  </div>
</template>

<script>
import { computed } from "@vue/runtime-core";
import ContactsList from "./components/ContactsList.vue";
import NavBar from "./components/NavBar.vue";
export default {
  name: "App",
  components: { ContactsList: ContactsList, NavBar: NavBar },
};
</script>

<style>

</style>