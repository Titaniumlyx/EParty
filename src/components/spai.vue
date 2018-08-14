<template>
    <div class="spai-container">
      <mt-header title="随时随地拍">
        <mt-button icon="back" @click="$router.back()" slot="left">
        </mt-button>
      </mt-header>

        <div class="scroll-content" >
        <!--<div class="con-list" >-->
          <router-link :to="'/xgnewItem?id='+item._id" v-for="item in arr" :key="item._id" class="spai-item">
            <div class="sptu">
              <img :src="item.img">
            </div>
            <div class="spline">{{item.title}}</div>
          </router-link>
        <!--</div>-->
      </div>
      <!--<div class="spai-tail">-->
        <!--<span>没有更多数据了...</span>-->
      <!--</div>-->

    </div>
</template>

<script>
    export default {
        name: "spai",
      data(){
        return{
          arr:[]
        }
      },
      methods:{
        getNews(){
          this.$axios.post("getNews",{type:6}).then(res=>{
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
  @import "../../style/spai.css";
</style>
