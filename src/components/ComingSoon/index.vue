<template>
  <div>
    <ul>
      <li v-for="item in comingList" :key="item.id">
        <div class="pic">
          <img :src="item.img | setWH('80.100')" alt />
        </div>
        <div>
          <h2>{{item.nm}}</h2>
        </div>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: "ComingSoon",
  data() {
    return {
      comingList: []
    };
  },
  mounted() {
    this.axios.get("/api/movieComingList?cityId=10").then(res => {
      var msg = res.data.msg;
      console.log(msg);
      if (msg === "ok") {
        this.comingList = res.data.data.comingList;
        // console.log(this.comingList);
      }
    });
  }
};
</script>
<style scoped>
.pic {
  width: 80px;
  height: 100px;
}
.pic img {
  width: 100%;
  height: 100%;
}
</style>