<template>
  <div id="header">
    <button>
      <chevron-left ></chevron-left>
      <p>BACK</p>
    </button>
    <h3>Megaphone header</h3>
    <span
      ><img :src="agentData.image" alt="icon" />
      <p class="agentName">{{ agentData.name }}</p>
    </span>
  </div>
</template>

<script>
import ChevronLeft from "vue-material-design-icons/ChevronLeft.vue";
export default {
  name: "Header",
  props: {
    agentData: {
      type: Object,
      default: {},
    },
  },
  components: {
    ChevronLeft,
  },
};
</script>

<style lang="scss" scoped>
</style>