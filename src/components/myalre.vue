<template>
  <div class="my-container">
    <mt-header title="我的党建">
      <mt-button icon="back" @click="$router.back()" slot="left">
      </mt-button>
    </mt-header>

    <div class="up-t">
      <div class="hsc">
        <img src="../assets/touxi.png" alt="">
      </div>
      <div class="no-deng" @click="toLog">
        my name
      </div>
    </div>

    <div class="my-content">
      <div class="my-list" @click="infom">
        <img src="../assets/person.png" class="my-content-left">
        <span>个人信息</span>
        <i>></i>
      </div>
      <div class="my-list" @click="score">
        <img src="../assets/lxjf.png" class="my-content-left">
        <span>个人量化积分</span>
        <i>></i>
      </div>
      <div class="my-list" @click="modpwd">
        <img src="../assets/xgmm.png" class="my-content-left">
        <span>修改密码</span>
        <i>></i>
      </div>
      <div class="my-list" @click="payfee">
        <img src="../assets/icon3.png" class="my-content-left">
        <span>党费缴纳</span>
        <i>></i>
      </div>
    </div>

    <button class="exde">
      <input type="button" value="退出登录" class="buttonex" @click="escLogin" v-if="isShow">
    </button>

  </div>
</template>

<script>
  import { Toast } from 'mint-ui';
    export default {
        name: "myalre",
      data(){
          return{
            isShow:false
          }
      },
      methods:{
        toLog(){
          this.$router.push({path:"/login",query:{mark:"myalre"}});
        },
        infom(){
          this.$axios.post("outUsers").then(res=>{
            // console.log(res);
            if(res.islogin == false){
              Toast("没有登录，请登录..");
              this.$router.push({path:"/login",query:{mark:"perinfor"}});
            }else{
              this.$router.push({path:"/perinfor"});
            }
          })
        },
        score(){
          this.$axios.post("outUsers").then(res=>{
          // console.log(res);
          if(res.islogin == false){
            Toast("没有登录，请登录..");
            this.$router.push({path:"/login",query:{mark:"perscore"}});
          }else{
            this.$router.push({path:"/perscore"});
          }
        })
        },
        modpwd(){
          this.$axios.post("outUsers").then(res=>{
            // console.log(res);
            if(res.islogin == false){
              Toast("没有登录，请登录..");
              this.$router.push({path:"/login",query:{mark:"modifypwd"}});
            }else{
              this.$router.push({path:"/modifypwd"});
            }
          })
        },
        payfee(){
            this.$router.push({path:"/payfee"});
        },
        escLogin(){
          this.$axios.post("outUsers").then(res=>{
            // console.log(res);
              this.$router.push({path:'/login',query:{mark:"myalre"}});
          })
        },
        hide(){
          this.$axios.post("outUsers").then(res=>{
            console.log(res);
            if(res.islogin == false){
              this.isShow=false;
            }else{
              this.isShow=true;
            }
          })
        }
      },
      mounted(){
          this.hide();
      }
    }
</script>

<style scoped>
  @import "../../style/myalre.css";
</style>
