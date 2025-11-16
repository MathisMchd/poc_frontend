<template>
  <div class="page-container">
    <div class="custom-card">

      <h2 class="card-title">Sauvegarde un utilisateur</h2>

      <div class="p-fluid p-formgrid p-grid">

        <div class="p-field p-col-12">
          <label for="firstName">Prénom</label>
          <input
            id="firstName"
            type="text"
            class="p-inputtext"
            v-model="firstName"
            placeholder="Entrez votre prénom"
          />
        </div>

        <div class="p-field p-col-12">
          <label for="lastName">Nom</label>
          <input
            id="lastName"
            type="text"
            class="p-inputtext"
            v-model="lastName"
            placeholder="Entrez votre nom"
          />
        </div>
      </div>

      <div class="p-mt-3">
        <button class="save-button" @click="saveUser">
          <span class="pi pi-save" style="margin-right: 8px;"></span>
          Enregistrer
        </button>
      </div>

      <div v-if="message" class="response-message">
        {{ message }}
      </div>

    </div>
  </div>
</template>

<script setup>
import axios from 'axios'
import { ref } from 'vue'

const firstName = ref('')
const lastName = ref('')
const message = ref('')

const API_URL = 'http://localhost:3000'

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

<style scoped>
.page-container {
  min-height: 100vh;
  background: #f4f6f9;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 1rem;
}

.custom-card {
  width: 400px;
  text-align: center;
  background: #fff;
  border-radius: 12px;
  padding: 1.5rem 1.5rem 1rem;
  box-shadow: 0 2px 10px rgba(0,0,0,0.08);
}

.card-title {
  font-size: 1.4rem;
  font-weight: 600;
  color: #495057;
  margin-bottom: 1.5rem;
}

.p-field label {
  font-weight: 600;
  color: #495057;
  margin-bottom: 0.3rem;
  display: block;
  text-align: left;
}

.p-inputtext {
  width: 100%;
  border-radius: 8px;
  padding: 0.7rem;
  border: 1px solid #ccc;
  font-size: 1rem;
  box-sizing: border-box;
}

.p-inputtext:focus {
  outline: none;
  border-color: #42b983;
}

.save-button {
  width: 100%;
  border-radius: 8px;
  font-size: 1.1rem;
  padding: 0.8rem;
  background: #42b983;
  border: none;
  color: white;
  cursor: pointer;
  transition: background .2s;
}

.save-button:hover {
  background: #359268;
}

.response-message {
  font-size: 1rem;
  margin-top: 1.2rem;
  color: #2d8a34;
}
</style>
