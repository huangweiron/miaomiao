<template>
  <div>
    <input type="text" v-model="message" />
    <div>
      <ul>
        <li v-for="item in movieList" :key="item.id">
          <div class="pic">
            <img :src="item.img | setWH('80.100')" alt />
            <!-- :src="item.img | setWH('80.100')" -->
          </div>
          <div>
            <p>{{item.nm}}{{item.sc}}</p>
            <p>{{item.enm}}</p>
            <p>{{item.cat}}</p>
            <p>{{item.rt}}</p>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  name: "Search",
  data() {
    return {
      message: "",
      movieList: []
    };
  },
  methods:{
    canss(){
      if(typeof this.source==='function'){
        this.source('zongzhi')
      }
    }
  },
  watch: {
    message(newVal) {
      // console.log(newVal);
      this.axios.get("/api/searchList?cityId=10&kw=" + newVal).then(res => {
        var msg = res.data.msg;
        var movies = res.data.data.movies;
        if (msg && movies) {
          this.movieList = res.data.data.movies.list;
        }
      });
    }
  }
};
</script>
<style scoped>
</style>