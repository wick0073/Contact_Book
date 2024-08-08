<template>
    <div v-if="contact">
      <h1>{{ contact.firstName }} {{ contact.lastName }}</h1>
      <p>Email: {{ contact.email }}</p>
      <router-link :to="{ name: 'EditContact', params: { id: contact.id } }">Edit</router-link>
      <button @click="deleteContact">Delete</button>
      <router-link to="/">Back to Contact List</router-link>
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
  
      const deleteContact = () => {
        contacts.value = contacts.value.filter(c => c.id !== contact.value.id)
        router.push('/')
      }
  
      return {
        contact,
        deleteContact
      }
    }
  }
  </script>
  