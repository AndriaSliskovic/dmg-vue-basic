<template>
  <div id="listItems">

    <ValidationObserver ref="observer" v-slot="{ handleSubmit, invalid }">
      <form @submit.prevent="handleSubmit(onSubmitEvent)" id="form">
            <ImageUpload></ImageUpload>
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
</template>

<script>
import { ValidationProvider, ValidationObserver, extend } from "vee-validate";
import { required, email, max } from "vee-validate/dist/rules";
import ImageUpload from '@/components/ImageUpload.vue'

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
  name:"List",
  components:{
ValidationProvider,
ValidationObserver,
ImageUpload
  },
  props: {
    listingData: {
      type: Object,
      default: {},
    },
  },
};
</script>

<style lang="scss" scoped>
</style>