<template>
    <div class="dstoday-container">
      <mt-header title="党史上的今天" fixed>
        <mt-button icon="back" @click="$router.back()" slot="left">
        </mt-button>
      </mt-header>

      <div class="dstoday-wrap" v-html="item">

      </div>

    </div>
</template>

<script>
  import { Toast } from 'mint-ui';
    export default {
        name: "dstoday",
      data(){
        return{
        item:""
        }
      },
      methods:{
        getDs(){
          this.$axios.get("getData").then(res=>{
            if(res.code==400){
              Toast("没有登录，请登录..");
              this.$router.push({path:"/login",query:{mark:"dstoday"}});
            }
            console.log(res);
            // console.log(res.data);
            this.item=res.data;
          })
        }
      },
      mounted(){
        this.getDs();
      }
    }
</script>

<style>
  .dstoday-wrap{
    margin-top: 50px;
    padding: 8px;
  }
  .dstoday-wrap h2{
    font-size:22px;
    font-weight: 800;
    line-height: 1.2;
  }
  .dstoday-wrap p{
    font-size:18px;
    text-indent:2em;
    margin-top: 8px;
    margin-bottom: 8px;
    line-height: 1.2;
  }
</style>
