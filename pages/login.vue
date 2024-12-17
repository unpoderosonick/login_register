<template>
    <div class="flex flex-col items-center justify-center h-screen bg-gray-50">
      <h1 class="text-2xl font-bold mb-4">Iniciar Sesión</h1>
      <form @submit.prevent="login" class="flex flex-col gap-4">
        <input
          v-model="email"
          type="email"
          placeholder="Correo"
          class="p-2 border rounded"
        />
        <input
          v-model="password"
          type="password"
          placeholder="Contraseña"
          class="p-2 border rounded"
        />
        <button type="submit" class="bg-green-500 text-white p-2 rounded">
          Iniciar Sesión
        </button>
      </form>
      <p v-if="errorMessage" class="text-red-500 mt-4">{{ errorMessage }}</p>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import { useRouter } from '#app';
  import { signInWithEmailAndPassword } from 'firebase/auth';
  import { auth } from '@/firebaseConfig';
  
  // Variables reactivas
  const email = ref('');
  const password = ref('');
  const errorMessage = ref('');
  const router = useRouter();
  
  // Función para iniciar sesión
  const login = async () => {
    try {
      if (!email.value || !password.value) {
        errorMessage.value = 'Por favor, completa todos los campos.';
        return;
      }
  
      const userCredential = await signInWithEmailAndPassword(
        auth,
        email.value,
        password.value
      );
      console.log('Usuario logueado:', userCredential.user);
  
      // Redirigir al usuario a la página "home"
      router.push('/home');
    } catch (error) {
      // Manejar errores de Firebase
      if (error.code === 'auth/user-not-found') {
        errorMessage.value = 'No existe un usuario con este correo.';
      } else if (error.code === 'auth/wrong-password') {
        errorMessage.value = 'Contraseña incorrecta.';
      } else {
        errorMessage.value = 'Error al iniciar sesión: ' + error.message;
      }
      console.error('Error al iniciar sesión:', error);
    }
  };
  </script>
  