<template>
  <div class="relative">
    <NuxtLayout>
      <NuxtPage />
    </NuxtLayout>

    <UNotifications />
    <UModals />
    <div v-if="loadingApp" class="bg-white fixed left-0 top-0 w-full h-full z-[9999]"><Loader /></div>
  </div>
</template>

<script setup>
import Loader from '@/components/ui/Loader.vue';
import { useAuthStore } from '@/stores/AuthStore';

const authStore = useAuthStore();
const loadingApp = ref(false);

async function loadAppData() {
  loadAppData.value = true;
  try {
    await authStore.getMe();
  } finally {
    loadAppData.value = false;
  }
}

if (localStorage.getItem('token')) {
  loadAppData();
}

useSeoMeta({
  title: 'Townup',
  ogTitle: 'Townup',
  description: 'Townup',
  ogDescription: 'Townup',
  ogImage: `${origin}/preview.png`,
});
</script>
