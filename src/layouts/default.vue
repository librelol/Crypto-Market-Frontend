<template>
  <v-app>
    <v-main>
      <template v-if="!hideSidebar">
        <Siderbar></Siderbar>
      </template>
      <v-container style="overflow-y: hidden; height: 100vh;">
        <router-view />
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup>
import { useRoute, useRouter } from 'vue-router';
import { computed, watch } from 'vue';

const route = useRoute();
const router = useRouter();
const hiddenSidebarPaths = ['/', '/login', '/register']; // Add paths where sidebar should not be shown

const hideSidebar = computed(() => hiddenSidebarPaths.includes(route.path));

// Watch for route changes and redirect if the path is not in hiddenSidebarPaths
watch(route, (newRoute) => {
  if (!hiddenSidebarPaths.includes(newRoute.path)) {
    router.push('/');
  }
});
</script>
