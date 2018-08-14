<template>
    <div class="showsf-container">
      <mt-header title="党员亮身份">
        <mt-button icon="back" @click="$router.back()" slot="left">
        </mt-button>
      </mt-header>

      <div class="showsf-wrap">
        <div class="showsf-content" v-for="item in arr" :key="item._id">
        <router-link :to="'/xgnewItem?id='+item._id" class="new2">
          <div class="new2-left">
            <img :src="item.img">
          </div>
          <div class="new2-right">
            <h3>{{item.title}}</h3>
            <div class="new2-bar">
              <span>{{item.updateTime}}</span>
              <span class="new2-counter">
              <i class="iconfont icon-icon_find"></i>
              {{item.eye}}
            </span>
            </div>
          </div>
        </router-link>
      </div>
      </div>

    </div>
</template>

<script>
    export default {
        name: "showsf",
      data(){
        return{
          arr:[]
        }
      },
      methods:{
        getNews(){
          this.$axios.post("getNews",{type:4}).then(res=>{
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
  .showsf-content .new2{
    position: relative;
    display: flex;
    width: 100%;
    height: 100px;
    padding: 10px;
    border-bottom: 1px solid #969696;
  }
  .new2-left img{
    width: 80px;
    height: 80px;
    position: absolute;
    left: 8px;
    top: 8px;
  }
  .new2-right{
    position: relative;
    height: 80px;
    margin-left: 87px;
  }
  .new2-right h3{
    height: 48px;
    font-size: 16px;
    color: #222;
  }
  .new2-bar{
    width: 100%;
    position: absolute;
    bottom: 0;
    left: 0;
    font-size: 10px;
  }
  .new2-counter{
    float: right;
  }
  .new2-counter i{
    color: #ccc;
    padding-right: 5px;
  }

</style>
