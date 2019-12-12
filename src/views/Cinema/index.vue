<template>
  <div id="main">
    <Header title="喵喵影院" />
    <div class="content">
      <div class="cinema">
        <div>全城</div>
        <div>品牌</div>
        <div>特色</div>
      </div>
      <CiList />
    </div>
    <TabBar />
  </div>
</template>
<script>
import Header from "@/components/Header";
import TabBar from "@/components/TabBar";
import CiList from "@/components/CiList";
export default {
  name: "Cinema",
  components: {
    Header,
    TabBar,
    CiList
  }
};
</script>
<style scoped>
#content .cinema {
  width: 100%;
  height: 45px;
  border-bottom: 1px solid #e6e6e6;
  display: flex;
  justify-content: space-between;
}
.cinema div {
  float: left;
  display: flex;
  height: 100%;
  line-height: 45px;
}
</style>