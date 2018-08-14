<template>
    <div class="charaact-container">
      <mt-header title="特色活动">
        <mt-button icon="back" @click="$router.back()" slot="left">
        </mt-button>
      </mt-header>

      <div class="charaact-content">
        <router-link :to="'/xgnewItem?id='+item._id" class="newthree" v-for="item in arr" :key="item._id">
          <div class="newthree-left">
            <img :src="item.img">
          </div>
          <div class="newthree-right">
            <h3>{{item.title}}</h3>
            <div class="newthree-bar">
              <span>{{item.updateTime}}</span>
              <span class="newthree-counter">
              <i class="iconfont icon-icon_find"></i>
              {{item.eye}}
            </span>
            </div>
          </div>
        </router-link>
      </div>
      <div class="charaact-tail">
        <span>没有更多数据了...</span>
      </div>

    </div>
</template>

<script>
    export default {
        name: "charaact",
      data(){
        return{
          arr:[]
        }
      },
      methods:{
        getNews(){
          this.$axios.post("getNews",{type:8}).then(res=>{
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
  .charaact-content .newthree{
    position: relative;
    display: flex;
    width: 100%;
    height: 100px;
    padding: 10px;
    border-bottom: 1px solid #969696;
  }
  .newthree-left img{
    width: 80px;
    height: 80px;
    position: absolute;
    left: 8px;
    top: 8px;
  }
  .newthree-right{
    position: relative;
    height: 80px;
    margin-left: 87px;
  }
  .newthree-right h3{
    height: 48px;
    font-size: 16px;
    color: #222;
  }
  .newthree-bar{
    width: 100%;
    position: absolute;
    bottom: 0;
    left: 0;
    font-size: 10px;
  }
  .newthree-counter{
    float: right;
  }
  .newthree-counter i{
    color: #ccc;
    padding-right: 5px;
  }
  .charaact-tail{
    padding-top: 7px;
    text-align: center;
  }
  .charaact-tail span{
    font-size: 14px;
    color: #666;
  }
</style>
