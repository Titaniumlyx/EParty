<template>
  <div class="content">
    <mt-header title="审核状态" fixed>
      <mt-button icon="back" @click="back" slot="left">
      </mt-button>
    </mt-header>
    <img src="../assets/reviewing.png" class="img" v-if="data==2||data==0">
    <img src="../assets/checkbox.png" class="img" v-else="data==1">
    <p>{{msg}}</p>
    <mt-button class="button" @click="button"  v-if="data==0">关闭</mt-button>
    <mt-button class="button" v-else="data==1||data==2" @click="con">继续提交</mt-button>
  </div>
</template>

<script>
  export default {
    components:{
    },
    data(){
      return{
        data:{},
        msg:""
      }
    },
    created(){
      this.getreport()
    },
    methods: {
      back(){
        this.$router.push("/horlife")
      },
      con(){
        this.$router.push("/thoughtrep1")
      },
      button(){
        this.$router.push("/horlife")
      },
      getreport() {
        this.$axios.post("getIdea",{kind:1}).then(res => {
         console.log(res);
        this.data=res.type;
          if(res.type==1){
            this.msg=("审核通过")
            this.msg=this.msg
          }
          if(res.type==2){
            this.msg=("审核不通过")
          }
          if(res.type==0){
            this.msg=("正在审核")
          }
        })
      }
    }
  }
</script>

<style scoped>
  .content{
    /*i{*/
      /*text-align: left;*/
      /*position: fixed;*/
      /*left: 0;*/
      /*right: 0;*/
      /*top: 12px;*/
      /*z-index: 998;*/
      /*margin-left: 10px;*/
      /*color: white;*/
    /*}*/
    margin-top: 23px;
    text-align: center;}
  .content .img{
      height: 101px;
      width: 101px;
      margin-top: 50px;
    }
  .content p{
      font-size: 14px;
      margin: 10px;
      color: #666;
    }
  .content  .button{
      border-radius: 10px;
      font-size: 16px;
      width: 248px;
      height: 40px;
      color: white;
      background: #cd0200;
      margin-top: 94px;
    }
</style>
