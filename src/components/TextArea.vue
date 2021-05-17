<template>
  <h1>Write 750 Words</h1>
  <textarea ref="textarea" class="textarea" rows="8" @input="countWords" />
  <h1>{{ wordCount }} / 750 words</h1>
  <h2>{{ parseFloat((wordCount / 750) * 100).toFixed(1) }} %</h2>
  <v-btn flat> Normal </v-btn>
</template>

<script>
export default {
  name: "HelloWorld",

  data() {
    return {
      wordCount: 0,
    };
  },

  methods: {
    countWords() {
      this.wordCount = this.$refs.textarea.value.trim().split(" ").length;
    },
  },
};
</script>
