<template>
  <div class="inputTag">
    <div class="tags">
      <div class="tag" v-for="(tag, index) in tags" :key="index">
        {{ tag }} <button @click="deleteTag(tag)">X</button>
      </div>
    </div>
    <form @submit.prevent="handleSubmit">
      <input
        class="input"
        type="text"
        v-model="currentValue"
        @keydown="handleKeyDown"
      />
    </form>
    <!-- <input type="text" v-model="currentValue" @keydown="handleKeyDown" /> -->
  </div>
</template>

<script>
export default {
  // props: ["onTagsChange"],
  emits: ["onTagsChange"],
  data() {
    return {
      currentValue: "",
      tags: [],
    };
  },
  methods: {
    handleKeyDown(e) {
      /* if (e.key === "Enter" && this.currentValue !== "") {
        this.tags.push(this.currentValue);
      } */
      if (e.key === "Backspace" && this.currentValue === "") {
        this.tags.pop();
        // this.onTagsChange(this.tags);
        this.$emit("onTagsChange", this.tags);
      }
    },
    handleSubmit(e) {
      if (this.currentValue !== "") {
        const exits = this.tags.some((item) => item === this.currentValue);
        if (!exits) {
          this.tags.push(this.currentValue);
          this.currentValue = "";
          // this.onTagsChange(this.tags);
        this.$emit("onTagsChange", this.tags);
        }
      }
    },
    deleteTag(tag) {
      this.tags = this.tags.filter((item) => item !== tag);
      // this.onTagsChange(this.tags);
      this.$emit("onTagsChange", this.tags);
    },
  },
};
</script>

<style scoped lang="scss">
.inputTag {
  display: inline-flex;
  border: solid 1px #000;
  align-items: center;
  border-radius: 5px;
  margin: 10px;
  height: 43px;

  .tags {
    display: flex;
    gap: 3px;
    padding: 5px;

    .tag {
      display: flex;
      padding: 5px;
      border: solid 1px #ccc;
      gap: 5px;
      align-content: center;
      border-radius: 15px;
    }
  }

  .input {
    border: none;
    outline: none;
    padding: 0 5px;
  }

  button {
    background-color: transparent;
    border: none;
    border-radius: 10px;
  }

  button:hover {
    cursor: pointer;
    background: #ff2030;
  }
}
.tags .tag {
  display: flex;
  padding: 5px;
  border: solid 1px #ccc;
  gap: 5px;
  align-content: center;
  align-items: center;
}
</style>
