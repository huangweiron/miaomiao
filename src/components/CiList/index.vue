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
          <p v-for="(num,key) in item.tag" v-if="num===1" :key="key">{{key | forma}}</p>
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
  },
  filters:{
    forma(key){

    }
  }
};
</script>
<style scoped>
</style>