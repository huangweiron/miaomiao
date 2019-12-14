<template>
  <div class="city_list">
    <!-- <Scroller ref="city_list">
    <div>-->
    <div class="remen">
      <h2>热门城市</h2>
      <ul>
        <li v-for="item in hotList" :key="item.id">{{item.nm}}</li>
      </ul>
    </div>
    <div class="city_sort" ref="city_sort">
      <div v-for="item in cityList" :key="item.index">
        <h2>{{item.index}}</h2>
        <ul>
          <li v-for="itemList in item.list" :key="itemList.id">{{itemList.nm}}</li>
        </ul>
      </div>
    </div>
    <!-- </div>
    </Scroller>-->
    <div class="city_index">
      <ul>
        <li
          v-for="(item,index) in cityList"
          :key="item.index"
          @click="handleTuIndex(index)"
        >{{item.index}}</li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  name: "City",
  data() {
    return {
      cityList: [],
      hotList: []
    };
  },
  mounted() {
    this.axios.get("/api/CityList").then(res => {
      var msg = res.data.msg;
      if (msg === "ok") {
        var cities = res.data.data.cities;
        var { cityList, hotList } = this.formatCityList(cities);
        this.cityList = cityList;
        this.hotList = hotList;
      }
    });
  },
  methods: {
    formatCityList(cities) {
      var cityList = [];
      var hotList = [];
      for (var i = 0; i < cities.length; i++) {
        if (cities[i].isHot === 1) {
          hotList.push(cities[i]);
        }
      }
      for (var i = 0; i < cities.length; i++) {
        var firstLetter = cities[i].py.substring(0, 1).toUpperCase();
        if (toCom(firstLetter)) {
          //新添加index
          cityList.push({
            index: firstLetter,
            list: [{ nm: cities[i].nm, id: cities[i].id }]
          });
        } else {
          //累加到已有index中
          for (var j = 0; j < cityList.length; j++) {
            if (cityList[j].index === firstLetter) {
              cityList[j].list.push({ nm: cities[i].nm, id: cities[i].id });
            }
          }
        }
      }
      //排序
      cityList.sort((n1, n2) => {
        if (n1.index > n2.index) {
          return 1;
        } else if (n1.index > n2.index) {
          return -1;
        } else {
          return 0;
        }
      });
      function toCom(firstLetter) {
        for (var i = 0; i < cityList.length; i++) {
          if (cityList[i].index === firstLetter) {
            return false;
          }
        }
        return true;
      }
      return {
        cityList,
        hotList
      };
    },
    handleTuIndex(index) {
      var h2 = this.$refs.city_sort.getElementsByTagName("h2");

      this.$refs.city_sort.parentNode.scrollTop = h2[index].offsetTop;
      // this.$refs.city_list.tOScrollTo(-h2[index].offsetTop);
    }
  }
};
</script>
<style scoped>
.city_list {
  overflow: scroll;
  height: 600px;
  position: relative;
}
.city_sort {
  /* height: 100%; */
  position: absolute;
}
.city_index {
  position: fixed;
  right: 10px;
  top: 100px;
}
</style>