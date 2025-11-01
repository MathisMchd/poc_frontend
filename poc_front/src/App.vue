<template>
  <div class="p-d-flex p-jc-center p-ai-center" style="min-height: 100vh; background: #f8f9fa;">
    <Card style="width: 400px; text-align: center;">
      <template #title>👋 Gestion utilisateur</template>

      <template #content>
        <div class="p-fluid p-formgrid p-grid">
          <div class="p-field p-col-12">
            <label for="firstName">Prénom</label>
            <InputText id="firstName" v-model="firstName" placeholder="Entrez votre prénom" />
          </div>
          <div class="p-field p-col-12">
            <label for="lastName">Nom</label>
            <InputText id="lastName" v-model="lastName" placeholder="Entrez votre nom" />
          </div>
        </div>

        <div class="p-d-flex p-jc-center p-mt-3">
          <Button label="Enregistrer" icon="pi pi-save" @click="saveUser" />
        </div>

        <div v-if="message" class="p-mt-4 p-text-bold">
          {{ message }}
        </div>
      </template>
    </Card>
  </div>
</template>

<script setup>
import axios from 'axios'
import { ref } from 'vue'

const firstName = ref('')
const lastName = ref('')
const message = ref('')

const API_URL = 'http://localhost:3000' // URL du backend NestJS

const saveUser = async () => {
  try {
    await axios.post(`${API_URL}/user`, {
      firstName: firstName.value,
      lastName: lastName.value,
    })
    const res = await axios.get(`${API_URL}/hello`)
    message.value = res.data.message
  } catch (err) {
    console.error(err)
    message.value = 'Erreur de communication avec le serveur.'
  }
}
</script>
