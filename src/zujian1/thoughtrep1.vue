<template>
  <div class="personalsummary-container">
    <mt-header title="思想汇报" fixed>
      <mt-button icon="back" @click="back" slot="left">
      </mt-button>
    </mt-header>

    <div class="personalsummary-content">
      <div class="upload">
        <label id="imgwrap">
          <input type="file" name="file" accept="image/jpeg,image/png" @change="up" id="file-input">
          <img :src="img" v-if="img">
          <img src="../assets/upload.png" alt="">
        </label>
      </div>

      <div>
        <div class="personalsummary-submit">
          <div class="personalsummary-sub" @click="upLoad">提交审核</div>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
  import axios from 'axios';
  import {Toast} from 'mint-ui';
  export default {
    name: "thoughtrep1",
    data(){
      return{
        token:'',
        img:""
      }
    },
    methods:{
      back(){
        this.$router.push({path:"/horlife"})
      },
      up($event){
        console.log($event);
        var file=$event.target.files[0];
        var form=new FormData();
        form.append("file",file);
        form.append("token",this.token);

        axios.post("https://upload-z1.qiniup.com",form,{
          headers:{"Content-Type":"multipart/form-data"}
        }).then(res=>{
          console.log(res);
          this.img=res.data.url;
          console.log(this.img);
        })
      },
      getToken(){
        axios.get("http://up.yaojunrong.com/getToken").then(res=>{
          this.token=res.data.data;
        })
      },
      upLoad(){
        this.$axios.post("addIdea",{img:this.img, kind:1}).then(res=>{
          console.log(res);
          if( res.type==0){
            Toast("提交成功")
          }else{
            Toast("提交失败")
          }
        })
      }
    },
    created(){
      this.getToken();
    }
  }
</script>

<style scoped>
  .personalsummary-content{
    margin-top: 50px;
    overflow-y: auto;
    background: #fff;
  }
  .upload #imgwrap{
    display: flex;
    width: 6.33rem;
    height: 3.333rem;
    border-radius: 4px;
    margin: 1px;
    padding: 10px;
    margin-left: -9px;
  }
  #file-input{
    display: none;
  }
  .upload #imgwrap img{
    float: left;
    width: 150px;
    height: 150px;
    margin-left: 10px;
  }
  .personalsummary-submit{
    position: absolute;
    bottom: 70px;
    width: 100%;
    text-align: center;
  }
  .personalsummary-sub{
    display: block;
    height: 47px;line-height: 42px;
    text-align: center;
    border-color: transparent;
    border-radius: 4px;
    background: #ef473a;
    color: #fff;font-size: 16px;
    margin-top: 10px;margin-bottom: 10px;
    padding: 0 12px;
  }
</style>
