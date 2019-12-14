<template>
  <div>
    <ul>
      <li v-for="item in cinemaList" :key="item.id">
        <div>
          <span>{{item.nm}}</span>
          {{item.sellPrice}}元
        </div>
        <p>{{item.addr}}</p>
        <p>{{item.distance}}</p>
        <div>
          <p v-for="(itemCard,key) in item.tag" :key="key">{{num}}</p>
        </div>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: "CiList",
  data() {
    return {
      cinemaList: []
    };
  },
  mounted() {
    this.axios.get("/api/cinemaList?cityId=10").then(res => {
      var msg = res.data.msg;

      if (msg === "ok") {
        this.cinemaList = res.data.data.cinemas;
        // console.log(this.cinemaList);
      }
    });
  }
};
</script>
<style scoped>
</style>