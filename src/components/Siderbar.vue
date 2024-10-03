<template>
  <v-navigation-drawer app>
    <v-list v-if="hasToken">
      <v-list-item
        v-for="item in menuItems"
        :key="item.title"
        @click="navigateTo(item.route)"
      >
        <v-list-item-title>
          <v-icon left>{{ item.icon }}</v-icon>
          {{ item.title }}
        </v-list-item-title>
      </v-list-item>
    </v-list>

    <template v-slot:append>
      <div class="pa-2">
        <v-btn block class="bg-deep-purple" v-if="hasToken" @click="logout">Logout</v-btn>
        <v-btn block class="bg-deep-purple" v-else @click="login">Login</v-btn>
      </div>
    </template>
  </v-navigation-drawer>
</template>

<script>
export default {
  data() {
    return {
      menuItems: [
        { title: 'Dashboard', route: '/dashboard', icon: 'mdi-view-dashboard' },
        { title: 'Settings', route: '/settings', icon: 'mdi-gavel' },
      ],
      hasToken: !!localStorage.getItem('token'), // Initialize hasToken based on localStorage
    };
  },
  watch: {
    // Watch for changes in localStorage token
    '$route'(to, from) {
      this.hasToken = !!localStorage.getItem('token');
    }
  },
  methods: {
    navigateTo(route) {
      this.$router.push(route);
    },
    logout() {
      // Add your logout logic here
      localStorage.removeItem('token'); // Remove token from localStorage
      this.hasToken = false; // Update hasToken
      this.$router.push('/login'); // Redirect to login page
    },
    login() {
      // Add your login logic here
      this.$router.push('/login'); // Redirect to login page
    }
  }
};
</script>