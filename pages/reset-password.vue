<template>
    <div class="flex flex-col items-center justify-center h-screen bg-gray-50">
      <h1 class="text-2xl font-bold mb-4">Recuperar Contraseña</h1>
      <form @submit.prevent="resetPassword" class="flex flex-col gap-4">
        <input
          v-model="email"
          type="email"
          placeholder="Correo electrónico"
          class="p-2 border rounded"
        />
        <button type="submit" class="bg-blue-500 text-white p-2 rounded">
          Enviar correo de recuperación
        </button>
      </form>
      <p v-if="successMessage" class="text-green-500 mt-4">{{ successMessage }}</p>
      <p v-if="errorMessage" class="text-red-500 mt-4">{{ errorMessage }}</p>
      <NuxtLink to="/login" class="text-blue-500 underline mt-4">
        Volver al inicio de sesión
      </NuxtLink>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import { sendPasswordResetEmail } from 'firebase/auth';
  import { auth } from '@/firebaseConfig';
  
  // Variables reactivas
  const email = ref('');
  const successMessage = ref('');
  const errorMessage = ref('');
  
  // Función para enviar correo de recuperación
  const resetPassword = async () => {
    successMessage.value = '';
    errorMessage.value = '';
  
    try {
      if (!email.value) {
        errorMessage.value = 'Por favor, ingresa tu correo.';
        return;
      }
  
      await sendPasswordResetEmail(auth, email.value);
      successMessage.value = 'Correo de recuperación enviado. Revisa tu bandeja de entrada.';
    } catch (error) {
      if (error.code === 'auth/user-not-found') {
        errorMessage.value = 'No existe un usuario con este correo.';
      } else {
        errorMessage.value = 'Error al enviar el correo: ' + error.message;
      }
      console.error('Error:', error);
    }
  };
  </script>
  