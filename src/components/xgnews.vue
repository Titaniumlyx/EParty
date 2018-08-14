<template>
  <div class="xgnews-container">
    <mt-header title="信工新闻眼" fixed>
      <mt-button icon="back" @click="$router.back()" slot="left">
      </mt-button>
    </mt-header>

    <div class="xgnews-wrap">
      <div class="xgnews-content" v-for="item in arr" :key="item._id">
        <router-link :to="'/xgnewItem?id='+item._id" class="new">
          <div class="new-left">
            <img :src="item.img" alt="">
          </div>
          <div class="new-right">
            <h3 v-text="item.title"></h3>
            <div class="new-bar">
              <span v-text="item.updateTime"></span>
              <span class="new-counter">
                <i class="iconfont icon-icon_find"></i>
                {{item.eye}}
              </span>
            </div>
          </div>
        </router-link>
      </div>
    </div>
    <div class="xgnews-tail">
      <span>没有更多数据了...</span>
    </div>

  </div>
</template>

<script>
    export default {
        name: "xgnews",
      data(){
          return{
            arr:[]
          }
      },
      methods:{
          getNews(){
            this.$axios.post("getNews",{type:1}).then(res=>{
              console.log(res)
              console.log(res.data);
              this.arr=res.data;
            })
          }
      },
      created(){
          this.getNews();
      }
    }
</script>

<style scoped>
  @import "../../style/xgnews.css";
</style>
