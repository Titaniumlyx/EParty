<template>
    <div class="polstudy-container">
      <mt-header title="政治学习" fixed>
        <mt-button icon="back" @click="$router.back()" slot="left">
        </mt-button>
      </mt-header>

      <div class="polstudy-wrap">
        <div class="polstudy-content" v-for="item in arr" :key="item._id">
        <router-link :to="'/xgnewItem?id='+item._id" class="polstudynew">
          <div class="polstudy-left">
            <img :src="item.img">
          </div>
          <div class="polstudy-right">
            <h3>{{item.title}}</h3>
            <div class="polstudy-bar">
              <span>{{item.updateTime}}</span>
              <span class="polstudy-counter">
                <i class="iconfont icon-icon_find"></i>
                {{item.eye}}
              </span>
            </div>
          </div>
        </router-link>
      </div>
      </div>
      <div class="polstudy-tail">
        <span>没有更多数据了...</span>
      </div>

    </div>
</template>

<script>
    export default {
        name: "polstudy",
      data(){
        return{
          arr:[]
        }
      },
      methods:{
        getNews(){
          this.$axios.post("getNews",{type:3}).then(res=>{
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
  .polstudy-wrap{
    margin-top: 50px;
  }
  .polstudy-content{
    overflow-y: auto;
  }
  .polstudy-content .polstudynew{
    position: relative;
    display: flex;
    width: 100%;
    height: 100px;
    padding: 10px;
    border-bottom: 1px solid #969696;
  }
  .polstudy-left img{
    width: 80px;
    height: 80px;
    position: absolute;
    left: 8px;
    top: 8px;
  }
  .polstudy-right{
    position: relative;
    height: 80px;
    margin-left: 87px;
  }
  .polstudy-right h3{
    height: 48px;
    font-size: 16px;
    color: #222;
  }
  .polstudy-bar{
    width: 100%;
    position: absolute;
    bottom: 0;
    left: 0;
    font-size: 10px;
  }
  .polstudy-counter{
    float: right;
  }
  .polstudy-counter i{
    color: #ccc;
    padding-right: 5px;
  }
  .polstudy-tail{
    padding-top: 7px;
    text-align: center;
  }
  .polstudy-tail span{
    font-size: 14px;
    color: #666;
  }
</style>
