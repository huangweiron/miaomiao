<template>
  <div class="content">
    <ul>
      <li v-for="item in movieList" :key="item.id">
        <div class="pic">
          <img :src="item.img | setWH('80.100')" />
        </div>
        <div class="info_list">
          <h2>{{item.nm}}</h2>
          <p>
            评分
            <span>{{item.sc}}</span>
          </p>
          <p>
            主演
            <span>{{item.star}}</span>
          </p>
          <p>{{item.showInfo}}</p>
        </div>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: "NowPlaying",
  data() {
    return {
      movieList: []
    };
  },
  mounted() {
    this.axios.get("/api/movieOnInfoList?cityId=10").then(res => {
      var msg = res.data.msg;
      if (msg === "ok") {
        this.movieList = res.data.data.movieList;
      }
    });
  }
};
</script>
<style scoped>
body,
html {
  width: 100%;
  height: 100%;
}
.pic {
  width: 80px;
  height: 100px;
}
.pic img {
  width: 100%;
  height: 100%;
}
.content {
  width: 100%;
  height: 600px;
  position: relative;
  overflow: scroll;
}
#content ul {
  position: absolute;
}
/* #content ul li {
  
} */
</style>