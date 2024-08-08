<template>
    <div class="mainContainer">
      <h1>Contact Book</h1>

        
      

        <div class="contactList">
            

            <ul>
                <div class="contactSearch">
                    <input v-model="search" placeholder="Search contacts..." />
                </div>

                <li v-for="contact in filteredContacts" :key="contact.id">
                    <router-link :to="{ name: 'ContactDetails', params: { id: contact.id }}">{{ contact.lastName }}, {{ contact.firstName }}</router-link>
                </li>

                
                
            </ul>
            <div class="addNewBtnContainer">
                    <router-link to="/add" class="addNewConatct">Add New Contact</router-link>
            </div>
        </div>
      
    </div>
</template>


  
  <script>
  import { ref, computed } from 'vue'
  import { useLocalStorage } from '@vueuse/core'
  
  export default {
    setup() {
      const search = ref('')
      const contacts = useLocalStorage('contacts', [])
      
      const filteredContacts = computed(() => {
        return contacts.value.filter(contact => 
          contact.firstName.toLowerCase().includes(search.value.toLowerCase()) ||
          contact.lastName.toLowerCase().includes(search.value.toLowerCase())
        ).sort((a, b) => a.lastName.localeCompare(b.lastName))
      })
  
      return {
        search,
        contacts,
        filteredContacts
      }
    }
  }
  </script>
  