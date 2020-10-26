<template>
  <div id="wraper">
    <div id="header">
      <button>BACK</button>
      <h1>Megaphone header</h1>
      <span
        ><img :src="agentData.image" alt="icon" />
        <p class="agentName">{{ agentData.name }}</p>
      </span>
    </div>
    <div id="main">
      <div id="listItems">
        <ValidationObserver ref="observer" v-slot="{ handleSubmit, invalid }">
          <form @submit.prevent="handleSubmit(onSubmitEvent)" id="form">
            <div v-for="(item, index) in listingData" :key="index">
              <!-- <input type="text" v-model="item.value"/> -->
              <template v-if="item.type === 'text_field' && !item.hiden">
                <ValidationProvider
                  v-slot="{ errors }"
                  :name="item.label"
                  :vid="`${item.type}` + `${index}`"
                  :rules="item.rules"
                >
                  <label
                    v-if="item.value"
                    class="dmgLabel"
                    :for="`${item.type}` + `${index}`"
                  >
                    {{ item.label }}
                  </label>
                  <input
                    type="text"
                    v-model="item.value"
                    :disabled="item.disabled"
                    :id="`${item.type}` + `${index}`"
                    :placeholder="item.label"
                  />
                  <span v-show="errors">{{ errors[0] }}</span>
                </ValidationProvider>
              </template>
              <template v-if="item.type === 'text_area' && !item.hiden">
                <ValidationProvider
                  v-slot="{ errors }"
                  :name="item.label"
                  :vid="`${item.type}` + `${index}`"
                  rules="max:200"
                >
                  <label
                    v-if="item.value"
                    class="dmgLabel"
                    :for="`${item.type}` + `${index}`"
                  >
                    {{ item.label }}
                  </label>
                  <textarea
                    v-model="item.value"
                    :disabled="item.disabled"
                    :id="`${item.type}` + `${index}`"
                    :placeholder="item.label"
                  >
                  </textarea>
                  <span class="dmgVal" v-show="errors">{{ errors[0] }}</span>
                </ValidationProvider>
              </template>
            </div>
          </form>
        </ValidationObserver>
      </div>
      <div id="part">
        <img :src="partData.image" alt="kuca" />
      </div>
    </div>
    <div id="baseMain">
      <div id="submitGroup">
        <button class="dmgButton" @click="onSubmitEvent">SAVE</button>
        <button class="dmgButton" @click="onPreviewEvent">PREVIEW</button>
      </div>
      <div id="footer">
        <h2>2020 - Megaphone</h2>
      </div>
    </div>
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
    onSubmitEvent() {
      console.log("form is submited");
    },
    onPreviewEvent() {
      this.loading = true;
      if (process.env.NODE_ENV === "development") {
        setTimeout(() => {
          this.loading = false;
        }, 500);
      }
    },
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
