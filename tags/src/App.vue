<template>
  <!-- <InputTag :onTagsChange="handleOnTagsChange" /> -->
  <InputTag @onTagsChange="handleOnTagsChange" />
</template>

<script>
import InputTag from "./components/InputTag.vue";
export default {
  name: "App",
  components: { InputTag },
  methods: {
    handleOnTagsChange(tags) {
      console.log(tags);
    },
  },
};
</script>

<style></style>
