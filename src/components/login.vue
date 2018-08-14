<template>
    <div class="container-login">
      <mt-header title="登录"  fixed>
        <mt-button icon="back" @click="$router.back()" slot="left">
        </mt-button>
      </mt-header>
        <div class="wrap">
          <div class="logo-wrap">
            <img src="../assets/logo.png" alt="">
          </div>

          <div class="form" >
            <div class="input-wrap">
              <input type="text" placeholder="身份证号" v-model="user.idNum">
            </div>
            <div class="input-wrap">
              <input type="password" placeholder="密码" v-model="user.pwd">
            </div>
            <div class="input-wrap">
              <mt-button size="large" @click="getLogin">登录</mt-button>
            </div>
          </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "login",
      data(){
        return{
          user:{
            idNum:'',
            pwd:''
          }
        }
      },
      methods:{
          getLogin(){
            console.log(this.user);
            this.changepath='/'+this.$route.query.mark;
            this.$axios.post("getLogin",this.user).then(res=>{
              console.log(res);
              // this.user=res.data;
              if(res.code==200){
                this.$router.push({path:this.changepath})
              }
             })
            // this.changepath='/'+this.$route.query.mark;
            // this.$axios.post("getLogin",this.user).then(res=>{
            //   this.$router.push({path:this.changepath})
            // })
      }
    }
    }
</script>

<style scoped>
  @import "../../style/login.css";
</style>
