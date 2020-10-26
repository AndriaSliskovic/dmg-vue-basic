<template>
  <div id="submitGroup">
    <button class="dmgButton" @click="onSubmitEvent">SAVE</button>
    <button class="dmgButton" @click="onPreviewEvent">PREVIEW</button>
  </div>
</template>

<script>
export default {
  name: "SubmitGroup",
  data() {
      return {
          loadedPart: false
      }
  },
  methods: {
    onSubmitEvent() {
      console.log("form is submited");
      this.$emit('submited',this.loadingPart)
    },
    onPreviewEvent() {
      this.loading = true;
      if (process.env.NODE_ENV === "development") {
        setTimeout(() => {
          this.loadingPart = true;
          this.$emit("loadedPart",this.loadingPart)
        }, 500);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
</style>