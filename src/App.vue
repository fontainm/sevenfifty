<template>
  <div class="container-fluid h-100 text-center">
    <TextArea />
  </div>
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
