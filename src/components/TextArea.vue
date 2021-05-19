<template>
  <div class="container-fluid h-100 text-center">
    <div class="d-flex h-100 py-3 flex-column">
      <transition name="fade">
        <div v-show="showIntro" class="intro">
          Type what's on your mind...
        </div>
      </transition>
      <textarea
        ref="textarea"
        rows="100"
        class="textarea mb-auto"
        :style="{ fontSize: fontSize + 'px' }"
        @input="countWords"
        @blur="focusArea"
      />
      <div class="mt-auto pt-3">
        <div class="row">
          <h2 class="col-7 text-left">{{ wordCount }} / 750 words</h2>
          <h2 class="col-5 text-right">{{ parseFloat((wordCount / 750) * 100).toFixed(1) }} %</h2>
        </div>
        <b-progress class="progress" :value="wordCount" :max="750" height="2rem" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TextArea",

  data() {
    return {
      wordCount: 0,
      showIntro: true,
    };
  },

  computed: {
    fontSize() {
      return 18;
    },
  },

  mounted() {
    this.focusArea();
  },

  methods: {
    focusArea() {
      this.$refs.textarea.focus();
    },

    map(value, in_min, in_max, out_min, out_max) {
      return ((value - in_min) * (out_max - out_min)) / (in_max - in_min) + out_min;
    },

    countWords() {
      if (this.showIntro) {
        this.showIntro = false;
      }
      this.wordCount = this.$refs.textarea.value
        .trim()
        .split(" ")
        .filter((v) => v !== "").length;
    },
  },
};
</script>
