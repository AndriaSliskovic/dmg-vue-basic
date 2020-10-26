<template>
  <div id="wraper">








 
  </div>
</template>

<script>
import dataJson from "@/resources/dataSource.json";
import data from "@/resources/data.json";
import { ValidationProvider, ValidationObserver, extend } from "vee-validate";
import { required, email, max } from "vee-validate/dist/rules";

//import ImagePicker from "@/components/ImagePicker.vue"
//import ImageUploadSimple from "@/components/ImageUploadSimple.vue"
//import ImageUpload from "@/components/ImageUpload.vue"

extend("max", max);
extend("email", email);
extend("required", {
  validate(value) {
    return {
      required: true,
      valid: ["", null, undefined].indexOf(value) === -1,
    };
  },
  computesRequired: true,
});

export default {
  name: "AssetContainer",
  components: {
    ValidationProvider,
    ValidationObserver,
  },
  data() {
    return {
      loading: false,
    };
  },
  props: {
    listingData: {
      type: Object,
      default: () => dataJson[0].listData,
    },
    agentData: {
      type: Object,
      default: () => dataJson[0].agentData1,
    },
    statusData: {
      type: Object,
      default: () => dataJson[0].statusData,
    },
    partData: {
      type: Object,
      default: () => dataJson[0].part,
    },
  },
  methods: {

    goBack() {
      window.history.back();
    },
  },
  computed: {},
};
</script>

<style lang="scss" scoped>
@import "../assets/html/megafon/css/style.css";
</style>
