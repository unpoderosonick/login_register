<script setup>
import { ref } from 'vue';
import { createUserWithEmailAndPassword } from 'firebase/auth';
import { auth } from '@/firebaseConfig';

const email = ref('');
const password = ref('');
const errorMessage = ref('');

const register = async () => {
  errorMessage.value = ''; // Limpia errores anteriores
  try {
    const userCredential = await createUserWithEmailAndPassword(auth, email.value, password.value);
    console.log('Usuario registrado:', userCredential.user);
  } catch (error) {
    if (error.code === 'auth/email-already-in-use') {
      errorMessage.value = 'El correo ya está en uso. Por favor, usa otro correo.';
    } else {
      errorMessage.value = 'Error al registrar: ' + error.message;
    }
    console.error('Error al registrar:', error);
  }
};
</script>

<template>
  <div class="flex flex-col items-center justify-center h-screen bg-gray-50">
    <h1 class="text-2xl font-bold mb-4">Registro</h1>
    <form @submit.prevent="register" class="flex flex-col gap-4">
      <input v-model="email" type="email" placeholder="Correo" class="p-2 border rounded" />
      <input v-model="password" type="password" placeholder="Contraseña" class="p-2 border rounded" />
      <button type="submit" class="bg-blue-500 text-white p-2 rounded">Registrar</button>
    </form>
    <p v-if="errorMessage" class="text-red-500 mt-4">{{ errorMessage }}</p>
  </div>
</template>
