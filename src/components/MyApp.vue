<template>
  <div id="myApp">
    <h1>{{ title }}</h1>
    <div id="container">
        <div id="content_main">
            <func-bar :currentCity="currentCity" :currentTown="currentTown" :currentView="currentView"></func-bar>
            <data-view :currentCity="currentCity" :currentTown="currentTown" :rawData="rawData"></data-view>
        </div>
        <side-bar></side-bar>
    </div>
    <div id="footer">
    </div>
  </div>
</template>

<script>
import rawData from "/json/data.json";
import FuncBar from "./FuncBar";
import DataView from "./DataView";
import SideBar from "./SideBar";

export default {
  name: 'MyApp',
  props: {
    title: String,
    currentCity: String,
    currentTown: String,
    currentView: String
  },
  data() {
    return {
        rawData: rawData
    };
  },
  components: {
    FuncBar,
    DataView,
    SideBar
  },
  created() {
    // console.log(this.rawData);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
