<template>
  <div id="app">
    <div v-if="!loaded">
      <pulse-loader
        :loading="true"
        color="blue"
        size="40px"
        class="centered"
      ></pulse-loader>
    </div>
    <!-- Main page -->
    <template v-else>
      <div id="wraper">
        <Header :agentData="agentData"></Header>
        <div id="main">
          <List :listingData="listingData"></List>
          <Part :partData="partData"></Part>
        </div>
        <div id="baseMain">
          <SubmitGroup
            @submited="onSubmitHandler"
            @loadedPart="onLoadedPart"
          ></SubmitGroup>
          <div id="footer">
            {{ new Date().getFullYear() }} — <strong>Megaphone</strong>
          </div>
        </div>
      </div>
      <!-- <AssetContainer /> -->
    </template>
  </div>
</template>



<script>
import { ref, reactive } from "@vue/composition-api";
import dataJson from "@/resources/dataSource.json";
//import AssetContainer from "@/components/AssetContainer.vue";
import PulseLoader from "vue-spinner/src/PulseLoader.vue";
import Header from "@/components/Header.vue";
import List from "@/components/List.vue";
import Part from "@/components/Part.vue";
import SubmitGroup from "@/components/SubmitGroup.vue";

export default {
  name: "App",
  components: {
    PulseLoader,
    Header,
    List,
    Part,
    SubmitGroup,
  },
  data() {
    return {
      loaded: false,
      apiKey: "TestKey",
      listingId: 2,
      AgentId: 1,
      statusId: 3,
      partID: 15,
      id: null,
      loading: true,
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
    getApiKey() {},
    getListingData() {},
    getAgentData() {},
    getStatusData() {},
    getPartData() {},
    onSubmitHandler(e) {
      console.log("part submited", e);
    },
    onLoadedPart(e) {
      console.log("onLoadedPart", e);
    },
  },

  mounted() {
    window.initiateAssetWidget = (assetId) => {
      if (assetId) {
        this.id = assetId;
        this.loaded = true;
      } else {
        this.id = null;
        this.loaded = false;
        throw new Error("Missing required parameter [assetId]");
      }
    };

    if (process.env.NODE_ENV === "development") {
      setTimeout(() => {
        window.initiateAssetWidget(2);
      }, 500);
    }
  },
};
</script>
<style scoped>
.centered {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
@import "./assets/html/megafon/css/style.css"
</style>
