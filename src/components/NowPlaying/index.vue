<template>
  <div class="content" ref="content">
    <Scroller :handleToScroll="handleToScroll" :handleToTouchEnd="handleToTouchEnd">
      <ul>
        <li>{{pullDownMsg}}</li>
        <li v-for="item in movieList" :key="item.id">
          <div class="pic" @tap="handlis">
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
    </Scroller>
  </div>
</template>
<script>
// import BScroll from "better-scroll";
export default {
  name: "NowPlaying",
  data() {
    return {
      movieList: [],
      pullDownMsg: ""
    };
  },
  mounted() {
    this.axios.get("/api/movieOnInfoList?cityId=10").then(res => {
      var msg = res.data.msg;
      if (msg === "ok") {
        this.movieList = res.data.data.movieList;
        // this.$nextTick(() => {
        //   var scroll = new BScroll(this.$refs.content, {
        //     tap: true,
        //     probeType: 1
        //   });
        //   scroll.on("scroll", pos => {
        //     // console.log("sdf");
        //     if (pos.y > 30) {
        //       this.pullDownMsg = "更新中";
        //     }
        //   });
        //   scroll.on("touchEnd", pos => {
        //     if (pos.y > 30) {
        //       this.axios.get("/api/movieOnInfoList?cityId=10").then(res => {
        //         var msg = res.data.msg;
        //         if (msg === "ok") {
        //           this.pullDownMsg = "更新完毕";
        //           setTimeout(() => {
        //             this.movieList = res.data.data.movieList;
        //             this.pullDownMsg = "";
        //           }, 1000);
        //         }
        //       });
        //     }
        //   });
        // });
      }
    });
  },
  methods: {
    handlis() {
      console.log("adsf");
    },
    handleToScroll(pos) {
      if (pos.y > 30) {
        this.pullDownMsg = "更新中";
      }
    },
    handleToTouchEnd(pos) {
      if (pos.y > 30) {
        this.axios.get("/api/movieOnInfoList?cityId=10").then(res => {
          var msg = res.data.msg;
          if (msg === "ok") {
            this.pullDownMsg = "更新完毕";
            setTimeout(() => {
              this.movieList = res.data.data.movieList;
              this.pullDownMsg = "";
            }, 1000);
          }
        });
      }
    }
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