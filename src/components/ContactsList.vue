<template>
  <div>
    <div class="buttons-container">
      <button type="button" class="rdm-contact-btn" @click="getRandomContact">
        Add Random Contact
      </button>
      <button type="button" class="sort-popularity-btn" @click="sortPopularity">
        Sort by popularity
      </button>
      <button type="button" class="sort-name-btn" @click="sortName">
        Sort by name
      </button>
    </div>

    <table class="table-container">
      <tr class="table-title">
        <th>Picture</th>
        <th>Name</th>
        <th>Popularity</th>
        <th>Won an Oscar</th>
        <th>Won an Emmy</th>
      </tr>
      <tr v-for="contact in contactsToShow" :key="contact.id">
        <td class="image-container">
          <img
            class="contact-image"
            :src="`${contact.pictureUrl}`"
            alt="Contact Image"
          />
        </td>
        <td>{{ contact.name }}</td>
        <td>{{ contact.popularity.toFixed([2]) }}</td>
        <td>
          <svg
            v-if="contact.wonOscar"
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            fill="currentColor"
            class="bi bi-trophy"
            viewBox="0 0 16 16"
          >
            <path
              d="M2.5.5A.5.5 0 0 1 3 0h10a.5.5 0 0 1 .5.5c0 .538-.012 1.05-.034 1.536a3 3 0 1 1-1.133 5.89c-.79 1.865-1.878 2.777-2.833 3.011v2.173l1.425.356c.194.048.377.135.537.255L13.3 15.1a.5.5 0 0 1-.3.9H3a.5.5 0 0 1-.3-.9l1.838-1.379c.16-.12.343-.207.537-.255L6.5 13.11v-2.173c-.955-.234-2.043-1.146-2.833-3.012a3 3 0 1 1-1.132-5.89A33.076 33.076 0 0 1 2.5.5zm.099 2.54a2 2 0 0 0 .72 3.935c-.333-1.05-.588-2.346-.72-3.935zm10.083 3.935a2 2 0 0 0 .72-3.935c-.133 1.59-.388 2.885-.72 3.935zM3.504 1c.007.517.026 1.006.056 1.469.13 2.028.457 3.546.87 4.667C5.294 9.48 6.484 10 7 10a.5.5 0 0 1 .5.5v2.61a1 1 0 0 1-.757.97l-1.426.356a.5.5 0 0 0-.179.085L4.5 15h7l-.638-.479a.501.501 0 0 0-.18-.085l-1.425-.356a1 1 0 0 1-.757-.97V10.5A.5.5 0 0 1 9 10c.516 0 1.706-.52 2.57-2.864.413-1.12.74-2.64.87-4.667.03-.463.049-.952.056-1.469H3.504z"
            />
          </svg>
        </td>
        <td class="trophy">
          <svg
            v-if="contact.wonEmmy"
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            fill="currentColor"
            class="bi bi-trophy"
            viewBox="0 0 16 16"
          >
            <path
              d="M2.5.5A.5.5 0 0 1 3 0h10a.5.5 0 0 1 .5.5c0 .538-.012 1.05-.034 1.536a3 3 0 1 1-1.133 5.89c-.79 1.865-1.878 2.777-2.833 3.011v2.173l1.425.356c.194.048.377.135.537.255L13.3 15.1a.5.5 0 0 1-.3.9H3a.5.5 0 0 1-.3-.9l1.838-1.379c.16-.12.343-.207.537-.255L6.5 13.11v-2.173c-.955-.234-2.043-1.146-2.833-3.012a3 3 0 1 1-1.132-5.89A33.076 33.076 0 0 1 2.5.5zm.099 2.54a2 2 0 0 0 .72 3.935c-.333-1.05-.588-2.346-.72-3.935zm10.083 3.935a2 2 0 0 0 .72-3.935c-.133 1.59-.388 2.885-.72 3.935zM3.504 1c.007.517.026 1.006.056 1.469.13 2.028.457 3.546.87 4.667C5.294 9.48 6.484 10 7 10a.5.5 0 0 1 .5.5v2.61a1 1 0 0 1-.757.97l-1.426.356a.5.5 0 0 0-.179.085L4.5 15h7l-.638-.479a.501.501 0 0 0-.18-.085l-1.425-.356a1 1 0 0 1-.757-.97V10.5A.5.5 0 0 1 9 10c.516 0 1.706-.52 2.57-2.864.413-1.12.74-2.64.87-4.667.03-.463.049-.952.056-1.469H3.504z"
            />
          </svg>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
import contactsData from "../contacts.json";
export default {
  name: "Contactlist",
  data() {
    return {
      contacts: contactsData,
      contactsToShow: [], // declaramos un array vacio
    };
  },
  created() {
    const nContacts = 5;
    if (this.contacts.length >= nContacts) {
      for (let i = 0; i < nContacts; i++) {
        // pop out the contact from the list when pushing it to the contact list
        this.contactsToShow.push(this.contacts.shift());
      }
    }
  },
  methods: {
    getRandomInt(min, max) {
      return Math.floor(Math.random() * (max - min + 1) + min);
    },
    getRandomContact() {
      if (this.contacts.length) {
        const rdmIndex = this.getRandomInt(0, this.contacts.length - 1); //get a random index from the list
        // as we are taking out the contacts we print, we don't need to check if it's already printed.
        const rdmContact = this.contacts[rdmIndex];
        this.contactsToShow.push(rdmContact);
        this.contacts.splice(rdmIndex, 1); // remove element from array
        console.log(this.contacts.length);
      } else {
        console.log("se acabo");
      }
    },
    sortPopularity() {
      this.contactsToShow = this.contactsToShow.sort(
        (a, b) => b.popularity - a.popularity
      );
    },
    sortName() {
      this.contactsToShow = this.contactsToShow.sort((a, b) =>
        a.name > b.name ? 1 : -1
      );
    },
  },
};
</script>

<style>
.contact-image {
  height: 100px;
}
.buttons-container {
  width: 60%;
  margin: 0 auto;
  display: flex;
  justify-content: space-evenly;
}
.table-container {
  margin: 20px auto;
  width: 60%;
  text-align: center;
}
.table-title {
  font-size: 30px;
  line-height: 3em;
}
.image-container {
  width: 20%;
}
</style>