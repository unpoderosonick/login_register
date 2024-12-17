<template>
    <div class="flex flex-col items-center justify-center h-screen bg-gray-50">
      <h1 class="text-2xl font-bold mb-4">¡Bienvenido, {{ user?.email }}!</h1>
      <p class="text-gray-700">Has iniciado sesión correctamente.</p>
      <button @click="logout" class="bg-red-500 text-white p-2 rounded mt-4">Cerrar sesión</button>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import { useRouter } from '#app';
  import { auth } from '@/firebaseConfig';
  import { onAuthStateChanged, signOut } from 'firebase/auth';
  
  // Variables reactivas
  const user = ref(null);
  const router = useRouter();
  
  // Escuchar cambios en el estado de autenticación
  onAuthStateChanged(auth, (currentUser) => {
    if (currentUser) {
      user.value = currentUser; // Asignar el usuario actual
    } else {
      router.push('/login'); // Redirigir al login si no está autenticado
    }
  });
  
  // Función para cerrar sesión
  const logout = async () => {
    try {
      await signOut(auth);
      router.push('/login'); // Redirigir al login después de cerrar sesión
    } catch (error) {
      console.error('Error al cerrar sesión:', error);
    }
  };
  </script>
  