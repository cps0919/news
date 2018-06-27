<template>
  <div class="newsdetail" v-if="newlists">
    <div class="header border-px">
    <span @click="exitss(newlists)">返回</span>
    <span class="type">{{newlists.category}}</span>
  </div>
    <div class="title">
      <div class="name">{{newlists.title}}</div>
      <div class="name-bottom">
        <span class="author">{{newlists.author_name}}</span>
        <span class="date">{{newlists.date}}</span>
        <div class="btn" @click="btnschange(newlists)">{{!newlists.shows?"+关注":newlists.shows==1?"已关注":"+关注"}}</div>
      </div>
    </div>
    <div class="imgs">
      <img :src="newlists.thumbnail_pic_s" alt="">
      <img :src="newlists.thumbnail_pic_s02" alt="">
      <img :src="newlists.thumbnail_pic_s03" alt="">
    </div>

  </div>
</template>
<script>
  import scroll from "./../../base/scroll.vue"
  export default {
    components: {scroll},
    data(){
      return {
      }
    },
    computed:{
      newlists(){
        let Id=this.$route.params.Id
        let newslist=this.$store.state.newlist
        for(let i=0;i<newslist.length;i++){
          if(newslist[i].author_name==Id){
            return newslist[i]
          }
        }
      }
    },
    methods: {
      //路由到new界面
      exitss(item){
        this.$router.back(-1)
        if(item.shows==0){
          let newslist=this.$store.state.newlist
          for(let i=0;i<newslist.length;i++){
            if(newslist[i].author_name==item.author_name){
              newslist.splice(i,1,)
            }
          }
        }
      },
      // 关注
      btnschange(item){
        if(!item.shows){
          this.$set(item,"shows",1)
        }else {
          this.$set(item,"shows",0)

        }

      }
    }
  }
</script>
<style lang="stylus" scoped>
  @import "./../../commons/styl/base.styl"
  .newsdetail
    padding 0 10px
    .header
      width 100%
      line-height 60px
      border-1px(rgba(7, 17, 27, 0.1))
      .type
        position absolute
        left 50%
        width 50px
        margin-left -25px
        color rgba(7, 17, 27, 0.5)
    .title
      font-size 10px
      position relative
      margin-bottom 10px
      .name
        font-size 18px
        font-weight 700
        margin-bottom 10px
      .name-bottom
        position relative
        width 100%
        height 100%
        vertical-align middle
        .author
          color rgba(7, 17, 27, 0.7)
          font-size 10px
          font-weight 700
        .date
          color rgba(7, 17, 27, 0.7)
          font-size 10px
        .btn
          position absolute
          bottom 0px
          right 10px
          font-size 15px
          text-align center
          color rgba(255, 255, 255, 0.8)
          border-radius 20px
          height 20px
          width 60px
          line-height 20px
          font-weight 700
          background blue
    .imgs
      width 100%
      img
        padding 5px 0
        width 100%

</style>
