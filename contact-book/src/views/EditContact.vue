<template>

  <div class="editContDetContainer">
    <div v-if="contact" class="editContDet">
      <h1>Edit Contact</h1>
      <form @submit.prevent="updateContact">
        <input v-model="contact.firstName" placeholder="First Name" required />
        <input v-model="contact.lastName" placeholder="Last Name" required />
        <input v-model="contact.email" placeholder="Email" required />
        <button type="submit">Update</button>
        <router-link :to="{ name: 'ContactDetails', params: { id: contact.id } }">Cancel</router-link>
      </form>
      
    </div>
  </div>

</template>
  
  <script>
  import { ref } from 'vue'
  import { useRoute, useRouter } from 'vue-router'
  import { useLocalStorage } from '@vueuse/core'
  
  export default {
    setup() {
      const route = useRoute()
      const router = useRouter()
      const contacts = useLocalStorage('contacts', [])
      const contact = ref(contacts.value.find(c => c.id === route.params.id))
  
      const updateContact = () => {
        const index = contacts.value.findIndex(c => c.id === contact.value.id)
        if (index !== -1) {
          contacts.value[index] = contact.value
          router.push({ name: 'ContactDetails', params: { id: contact.value.id } })
        }
      }
  
      return {
        contact,
        updateContact
      }
    }
  }
  </script>
  