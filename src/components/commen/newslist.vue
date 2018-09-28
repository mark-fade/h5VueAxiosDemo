<!--  -->
<template>
  <section class="newslist">
    <div v-for="(item,index) in newslist" :key="index">
      <div class="newsitem">
        <img class="img" v-if="item.thumbnail" :src="item.thumbnail">

        <div class="cont">
          <span>{{item.title}}</span>
          <span class="time">{{item.updateTime}}</span>
          <span class="commentnum">{{item.commentsall}}</span>
        </div>
        
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {};
  },
  props: {
    newslist: {
      type: Array,
      default: function() {
        return [];
      }
    }
  },
  components: {},

  computed: {},

  mounted: {},

  methods: {}
};
</script>
<style lang='scss' scoped>
@import "../../style/mixin";
.home {
  width: 100%;
}
.newsitem {
  display: flex;
  justify-content: space-between;
  border-bottom: 1px solid #eee;
  padding: 5px;
  position: relative;
  .img {
    @include wh(5.28rem, 3.76rem);
    margin-right: 0.2rem;
  }
  .cont {
    text-align: left;
    flex: 1;
    position: relative;
    font-size: 14px; /*px*/
  }
  .time {
    position: absolute;
    bottom: 0;
    left: 0;
    font-size: 12px; /*px*/
  }
  .commentnum {
    position: absolute;
    bottom: 0;
    right: 0;
    font-size: 12px; /*px*/
  }
}
</style>