<template>
  <div id="myApp">
    <div id="container" class="section">
      <div id="container_inner" class="section_inner">
        <h1 id="page_title">{{ title }}</h1>
        <div id="content_wrapper">
            <div id="content_main">
                <data-view :regionData="regionData" :rawData="rawData"></data-view>
            </div>
            <side-bar></side-bar>
        </div>
      </div>
    </div>
    <div id="footer" class="section">
      <div id="footer_inner" class="section_inner">
        <p id="footer_company">CMoney 全耀財經資訊</p>
        <div id="foter_source">
          <span id="source_text">資料來源：</span>
          <a id="source_link" href="https://data.gov.tw/" target="_blank">政府資料開放平臺</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import rawData from "/json/data.json";
import regionData from "/json/region.json";
import DataView from "./DataView";
import SideBar from "./SideBar";

export default {
  name: 'MyApp',
  props: {
    title: String,
    currentView: String,
  },
  data() {
    return {
        rawData: rawData,
        regionData: regionData
    };
  },
  components: {
    DataView,
    SideBar
  },
  methods: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">


</style>
