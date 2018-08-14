<template>
   <div class="horlife-content">
     <router-link to="/shouye">
       <mt-header title="掌上组织生活">
         <mt-button icon="back"  slot="left"></mt-button>
       </mt-header>
     </router-link>

     <div class="abo-tu">
       <img src="../assets/timg.jpg" alt="">
     </div>

     <div class="h-life">
       <div class="row1">
         <router-link to="/polstudy" class="hor-option">
           <img src="../assets/icon1.png" alt="">
           <i>政治学习</i>
         </router-link>
         <div @click="btnsx" class="hor-option">
           <img src="../assets/icon2.png" alt="">
           <i>思想汇报</i>
         </div>
         <div @click="btnxd" class="hor-option">
           <img src="../assets/icon3.png" alt="">
           <i>心得总结</i>
         </div>
       </div>
       <div class="row2">
         <div @click="btnmz" class="hor-option">
           <img src="../assets/icon4.png" alt="">
           <i>民主评议</i>
         </div>
         <router-link to="/findognzt" class="hor-option">
           <img src="../assets/icon5.png" alt="">
           <i>流动党员找组织</i>
         </router-link>
       </div>
     </div>

   </div>
</template>

<script>
  import { Toast } from 'mint-ui';
    export default {
        name: "horlife",
      methods:{
        btnsx(){
          this.$axios.post("getIdea",{kind:1}).then(res=>{
            console.log(res)

            if(res.code == 400){
              Toast("没有登录，请登录..");
              this.$router.push({path:"/login",query:{mark:"horlife"}});
            }
            else if(res.type==0||res.type==1||res.type==2){
              this.$router.push("/shenHe")
            }
            else{
              this.$router.push("/thoughtrep1")
            }
          })
        },
        btnxd(){
          this.$axios.post("getIdea",{kind:2}).then(res=>{

            if(res.code == 400){
              Toast("没有登录，请登录..");
              this.$router.push({path:"/login",query:{mark:"horlife"}});
            }
            else if(res.type==0||res.type==1||res.type==2){
              this.$router.push("/xindesumm")
            }
            else{
              this.$router.push("/xindesum1")
            }
          })
        },
        btnmz(){
          // if(this.code == 400){
          //   Toast("没有登录，请登录..");
          //   this.$router.push({path:"/login",query:{mark:"horlife"}});
          // }else{
            this.$router.push({path:"/minzhu"});
          // }
        }
      }
    }
</script>

<style scoped>
  @import "../../style/horlife.css";
</style>
