<template>
  <div class="content">
    <mt-header title="评论" fixed>
      <mt-button icon="back" @click="back" slot="left">
      </mt-button>
    </mt-header>

    <div class="pl-wrap">
    <p>个人总结</p>
    <img :src="data.pic">

    <div class="foot">
      <input type="radio" value="0" name="choose" v-model="status">
      <label>优</label>
      <input  type="radio" value="1" name="choose" v-model="status">
      <label>良</label>
      <input type="radio" value="2" name="choose" v-model="status">
      <label>中</label>
      <input type="radio" value="3" name="choose" v-model="status">
      <label>差</label>
      <button @click="submit">提交</button>
    </div>
    </div>

  </div>
</template>

<script>
  import { MessageBox } from 'mint-ui';
  import { Toast } from 'mint-ui';
  export default {
    data(){
      return{
        discuss :[{
          _id:""
        }] ,
        data:[{
          pic:"",
          id:"",
        }],
        status:""
      }
    },
    created(){
      this.getdiscuss();
    },
    methods: {
      back(){
        this.$router.history.go(-1)
      },
      getdiscuss(){
        this.$axios.get("getDiscuss").then(res=>{
          // console.log(res.data);
          this.discuss=res.data
          this.getOther();
        })
      },
      getOther(){
        this.$axios.get("getOthers",
          {discussId:this.discuss._id,otherUserId:this.$route.query.id}).then(res=>{
          // console.log(res.data);
          this.data=res.data;
          if(res.data == null){
            Toast("该用户没有完善个人总结");
            this.$router.push("/discuss")
          }
        })
      },
      submit(){

        MessageBox.confirm('确定提交吗?').then(action => {
          this.$axios.post("addDiscuss",
            {id:this.data.id,status:this.status}).then(res=>{
            // console.log(res);
            Toast("提交成功")
            this.$router.push("/discuss")
          })
        })
      }
    }
  }
</script>

<style scoped >
  .content {
    text-align: center;
  }
  .pl-wrap{
    margin-top: 50px;
  }
  .content p {
      margin-top: 20px;
      text-align: center;
      font-size: 16px;
      margin-bottom: 20px;
    }
  .content img {
      width: 95%;
      height: 261px;
      margin: 5px;
    }
    .foot {
      margin: 0 auto;
      font-size: 14px;
      line-height: 40px;
      width: 95%;
      height: 40px;
      position: fixed;
      bottom: 2px;
      right: 0;
      left: 0;
    }
      label{
        margin-right: 20px;
      }
      button{
        background: white;
        color: red;
        border:1px solid red;
        border-radius: 5px;
      }
</style>
