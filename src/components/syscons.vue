<template>
    <div class="syscons-container">
      <mt-header title="制度建设">
        <mt-button icon="back" @click="$router.back()" slot="left">
        </mt-button>
      </mt-header>

      <div class="syscons-content">
        <router-link :to="'/xgnewItem?id='+item._id" class="newtwo" v-for="item in arr" :key="item._id">
          <div class="newtwo-left">
            <img :src="item.img">
          </div>
          <div class="newtwo-right">
            <h3>{{item.title}}</h3>
            <div class="newtwo-bar">
              <span>{{item.updateTime}}</span>
              <span class="newtwo-counter">
              <i class="iconfont icon-icon_find"></i>
              {{item.eye}}
            </span>
            </div>
          </div>
        </router-link>
      </div>
      <div class="syscons-tail">
        <span>没有更多数据了...</span>
      </div>

    </div>
</template>

<script>
    export default {
        name: "syscons",
      data(){
        return{
          arr:[]
        }
      },
      methods:{
        getNews(){
          this.$axios.post("getNews",{type:7}).then(res=>{
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
  .syscons-content .newtwo{
    position: relative;
    display: flex;
    width: 100%;
    height: 100px;
    padding: 10px;
    border-bottom: 1px solid #969696;
  }
  .newtwo-left img{
    width: 80px;
    height: 80px;
    position: absolute;
    left: 8px;
    top: 8px;
  }
  .newtwo-right{
    position: relative;
    height: 80px;
    margin-left: 87px;
  }
  .newtwo-right h3{
    height: 48px;
    font-size: 16px;
    color: #222;
  }
  .newtwo-bar{
    width: 100%;
    position: absolute;
    bottom: 0;
    left: 0;
    font-size: 10px;
  }
  .newtwo-counter{
    float: right;
  }
  .newtwo-counter i{
    color: #ccc;
    padding-right: 5px;
  }
  .syscons-tail{
    padding-top: 7px;
    text-align: center;
  }
  .syscons-tail span{
    font-size: 14px;
    color: #666;
  }
</style>
