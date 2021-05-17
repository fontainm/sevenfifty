<template>
  <v-app>
    <v-main>
      <TextArea />
    </v-main>
  </v-app>
</template>

<script>
import TextArea from "./components/TextArea.vue";

export default {
  name: "App",

  components: {
    TextArea,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.textarea {
  width: 90%;
  font-size: 2rem;
}
</style>
