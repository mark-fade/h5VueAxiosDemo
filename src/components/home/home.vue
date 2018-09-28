<!--  -->
<template>
  <div>
      

      <!-- 新闻列表 -->
      <section class="project-list" v-infinite-scroll="loadMore" infinite-scroll-disabled="busy" infinite-scroll-distance="20">
        <newslist
          :newslist = "news.item"
         >
        </newslist>
    </section>

  </div>
</template>

<script>
import { getnews } from "@/http/getData";
import newslist from "@/components/commen/newslist";

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
    }
  },
  components: {
    newslist
  }
};
</script>
<style lang='scss' scoped>
</style>