<!--  -->
<template>
  <div class="home">

    <swiper :options="swiperOption" class="swiper-wrap" v-if="swiper.length">
      <swiper-slide v-for="(item,index) in swiper" :key="index" v-if="item.type!='web'">
        <span class="title">{{item.title}}</span>
        <img :src="item.thumbnail" alt="" @click="toCarousel(item.id)"/>
      </swiper-slide>
        <div class="swiper-pagination" slot="pagination" v-if="swiper.length>1"></div>
    </swiper>

    <!-- 新闻列表 -->
    <section class="project-list" v-infinite-scroll="loadMore" infinite-scroll-disabled="busy" infinite-scroll-distance="20">
      <newslist :newslist="news.item">
      </newslist>
    </section>

  </div>
</template>

<script>
import { getnews } from "@/http/getData";
import newslist from "@/components/commen/newslist";
import { swiper, swiperSlide } from "vue-awesome-swiper";

export default {
  data() {
    return {
      swiper: [],
      news: [],
      topic: [],
      page: 1,
      busy: true,
      loadernone: false, //没有数据提示
      swiperOption: {
        pagination: ".swiper-pagination",
        paginationClickable: true,
        spaceBetween: 30,
        centeredSlides: true,
        autoplay: 3000,
        perspective: 15,
        autoplayDisableOnInteraction: false,
        notNextTick: true
      },
      showBackStatus: false,
      transitionName: "router-slide"
    };
  },
  created() {
    this.init();
  },
  methods: {
    async init() {
      let response = await getnews(
        "TY43,FOCUSTY43,TYTOPIC",
        this.page++,
        "5.4.0"
      );
      response.data.forEach((obj, index) => {
        if (obj.item) {
          let type = obj.type;
          if (type == "focus") {
            this.swiper = obj.item;
          } else if (type == "list") {
            this.news = obj;
          } else if (type == "tytopic") {
            this.topic = obj;
          }
        }
      });
    },
    toCarousel(params) {}
  },
  components: {
    swiper,
    swiperSlide,
    newslist
  }
};
</script>
<style lang='scss' scoped>
.home {
  width: 100%;
}
.swiper-wrap {
  height: 360px;
  width: 100%;
  position: relative;
  img {
    height: 100%;
    width: 100%;
  }
  .title {
    position: absolute;
    bottom: 0;
    left: 0.266667rem;
    font-size: 16px; /*px*/
    color: #fff;
  }
}
</style>