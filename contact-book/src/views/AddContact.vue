<template>
    <div>
      <h1>Add New Contact</h1>
      <form @submit.prevent="addContact">
        <input v-model="firstName" placeholder="First Name" required />
        <input v-model="lastName" placeholder="Last Name" required />
        <input v-model="email" placeholder="Email" required />
        <button type="submit">Add</button>
      </form>
      <router-link to="/">Back to Contact List</router-link>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue'
  import { useRouter } from 'vue-router'
  import { useLocalStorage } from '@vueuse/core'
  import { v4 as uuidv4 } from 'uuid'
  
  export default {
    setup() {
      const router = useRouter()
      const contacts = useLocalStorage('contacts', [])
      const firstName = ref('')
      const lastName = ref('')
      const email = ref('')
  
      const addContact = () => {
        const newContact = {
          id: uuidv4(),
          firstName: firstName.value,
          lastName: lastName.value,
          email: email.value
        }
        contacts.value.push(newContact)
        router.push({ name: 'ContactDetails', params: { id: newContact.id } })
      }
  
      return {
        firstName,
        lastName,
        email,
        addContact
      }
    }
  }
  </script>
  