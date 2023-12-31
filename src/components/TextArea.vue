<template>
  <form
    autocomplete="off"
    spellcheck="false"
    class="d-flex h-100 py-3 flex-column"
  >
    <transition name="fade">
      <div v-show="showIntro" class="intro">
        {{ introText }}
      </div>
    </transition>
    <transition name="fade">
      <div v-show="finished" class="finish">
        {{ finishedText }}
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
      <div class="row text">
        <h2 class="col-8 text-left">
          <v-number :speed="200" v-model="wordCount" />
          <span> / 750 words </span>
        </h2>
        <h2 class="col-4 text-right">
          <v-number :speed="200" v-model="wordPercentage" />
          %
        </h2>
      </div>
      <b-progress
        class="progress"
        :value="wordCount"
        :max="750"
        height="2rem"
      />
    </div>
  </form>
</template>

<script>
import { VNumber } from "@maxflex/v-number";

export default {
  name: "TextArea",

  components: {
    VNumber,
  },

  data() {
    return {
      wordCount: 0,
      introText: "Type what's on your mind...",
      finishedText: "Well done!",
      showIntro: true,
      finished: false,
    };
  },

  watch: {
    wordCount() {
      this.finished = this.wordCount >= 750;
    },
  },

  computed: {
    fontSize() {
      return 18;
    },

    wordPercentage() {
      return parseFloat((this.wordCount / 750) * 100).toFixed(1);
    },
  },

  mounted() {
    this.focusArea();
    this.$refs.textarea.value = "";
  },

  methods: {
    focusArea() {
      this.$refs.textarea.focus();
    },

    map(value, in_min, in_max, out_min, out_max) {
      return (
        ((value - in_min) * (out_max - out_min)) / (in_max - in_min) + out_min
      );
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
