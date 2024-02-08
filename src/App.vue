<template>
  <v-app>
    <v-main>
        <v-container>
          <HomePage/>
        </v-container>
    </v-main>
  </v-app>
</template>

<script>
import HomePage from './pages/index';

export default {
  name: 'App',

  components: {
    HomePage,
  },

  data: () => ({
    //
  }),
};
</script>

<style scope>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  background-color: #2c3e50;
}
::-webkit-scrollbar {
  display: none;
}
</style>
