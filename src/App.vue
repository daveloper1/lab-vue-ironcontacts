<template>
  <div>
    <table>
      <tr>
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
      </tr>
      <tr v-for="contact in getContacts" :key="contact.id">
        <td>
          <img
            class="contact-image"
            :src="`${contact.pictureUrl}`"
            alt="Contact Image"
          />
        </td>
        <td>{{ contact.name }}</td>
        <td>{{ contact.popularity }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
import { computed } from "@vue/runtime-core";
import contactsData from "../src/contacts.json";
export default {
  name: "App",
  components: {},
  data() {
    return {
      contacts: contactsData,
    };
  },
  computed: {
    getContacts() {
      const nElements = 5;
      return this.contacts.slice(0, nElements);
    },
  },
};
</script>

<style>
.contact-image {
  height: 100px;
}
</style>