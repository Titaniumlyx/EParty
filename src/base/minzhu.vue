<template>
    <div class="minzhu-container">
      <mt-header title="掌上组织生活" fixed>
        <mt-button icon="back" @click="$router.back()" slot="left">
        </mt-button>
      </mt-header>

      <div class="minzhu-content">
        <div class="submitWrap">
          <div to="/personalsummary" @click="gzbutt" class="minzhu-item">个人总结</div>
          <router-link to="/discuss" class="minzhu-item">民主评议</router-link>
        </div>
      </div>

    </div>
</template>

<script>
  import { Toast } from 'mint-ui';
    export default {
        name: "minzhu",
      data(){
          return{}
      },
      methods:{
        gzbutt(){
          this.$axios.post("addPerSum").then(res=>{
            console.log(res);
            if(res.islogin==false){
              // Toast("没有登录，请登录..");
              this.$router.push({path:"/login",query:{mark:"minzhu"}});
            }
            else if(res.status==0||res.status==1||res.status==2){
              this.$router.push("/gzshenHe")
            }
            else{
              this.$router.push("/personalsummary")
            }
          })
        }
      }
    }
</script>

<style scoped>
  .minzhu-content{
    margin-top: 50px;
    overflow-y: auto;
    background: #fff;
  }
  .submitWrap{
    position: absolute;
    top: 35%;
    width: 100%;
  }
  .minzhu-item{
    display: block;
    text-align: center;
    width: 50%;
    height: 47px;line-height: 42px;
    background: #ef473a;
    border-color: transparent;
    border-radius: 4px;
    margin: 20px auto;
    color: #fff;font-size: 16px;
  }
</style>
