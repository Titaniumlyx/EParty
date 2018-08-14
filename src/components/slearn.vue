<template>
    <div class="slearn-container">
      <mt-header title="随时随地学">
        <mt-button icon="back" @click="$router.back()" slot="left">
        </mt-button>
      </mt-header>

      <div class="slearn-wrap">
        <div class="slearn-content" v-for="item in arr" :key="item._id">
        <router-link :to="'/xgnewItem?id='+item._id" class="newone">
          <div class="newone-left">
            <img :src="item.img" alt="">
          </div>
          <div class="newone-right">
            <h3 v-text="item.title"></h3>
            <div class="newone-bar">
              <span v-text="item.updateTime"></span>
              <span class="newone-counter">
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
        name: "slearn",
      data(){
        return{
          arr:[]
        }
      },
      methods:{
        getNews(){
          this.$axios.post("getNews",{type:5}).then(res=>{
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
  .slearn-content .newone{
    position: relative;
    display: flex;
    width: 100%;
    height: 100px;
    padding: 10px;
    border-bottom: 1px solid #969696;
  }
  .newone-left img{
    width: 80px;
    height: 80px;
    position: absolute;
    left: 8px;
    top: 8px;
  }
  .newone-right{
    position: relative;
    height: 80px;
    margin-left: 87px;
  }
  .newone-right h3{
    height: 48px;
    font-size: 16px;
    color: #222;
  }
  .newone-bar{
    width: 100%;
    position: absolute;
    bottom: 0;
    left: 0;
    font-size: 10px;
  }
  .newone-counter{
    float: right;
  }
  .newone-counter i{
    color: #ccc;
    padding-right: 5px;
  }

</style>
