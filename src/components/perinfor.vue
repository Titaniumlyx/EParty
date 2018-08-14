<template>
    <div class="perinfor-container">
      <mt-header title="个人信息">
        <mt-button icon="back" @click="back" slot="left">
        </mt-button>
        <router-link to="/modiperin" slot="right">编辑</router-link>
      </mt-header>

      <div class="perinfor-content">
        <div class="perinfor-list" >
          <div class="info-item">
            <span>头像</span>
            <img :src="Info.avatar" alt="">
          </div>
          <div class="info-item">
            <span>姓名</span>
            <span>{{Info.userName}}</span>
          </div>
          <div class="info-item">
            <span>身份证</span>
            <span>{{Info.idNum}}</span>
          </div>
          <div class="info-item">
            <span>家庭住址</span>
            <span>{{Info.homeAddress}}</span>
          </div>
          <div class="info-item">
            <span>工作地址</span>
            <span>{{Info.workAddress}}</span>
          </div>
          <div class="info-item">
            <span>民族</span>
            <span>{{Info.nation}}</span>
          </div>
          <div class="info-item">
            <span>微信号</span>
            <span>{{Info.weChat}}</span>
          </div>
          <div class="info-item">
            <span>qq号</span>
            <span>{{Info.qqNumber}}</span>
          </div>
          <div class="info-item">
            <span>性别</span>
            <span>{{Info.sex}}</span>
          </div>
          <div class="info-item">
            <span>最高学历</span>
            <span>{{Info.education}}</span>
          </div>
          <div class="info-item">
            <span>职称</span>
            <span>{{Info.jobTitle}}</span>
          </div>
          <div class="info-item">
            <span>薪资水平</span>
            <span>{{Info.emolument}}</span>
          </div>
          <div class="info-item">
            <span>入党时间</span>
            <span>{{Info.enterPartyTime}}</span>
          </div>
          <div class="info-item">
            <span>党费最后缴纳时间</span>
            <span>{{Info.paymentTime}}</span>
          </div>
          <div class="info-item">
            <span>当前身份</span>
            <span>{{Info.partyStatus}}</span>
          </div>
        </div>
      </div>

    </div>
</template>

<script>
    export default {
        name: "perinfor",
      data(){
          return{
            Info:{}
          }
      },
      methods:{
        back(){
          this.$router.push({path:"/myalre"});
        },
          getUser(){
            this.$axios.get("getUsersinfo").then(res=>{
              console.log(res);
              this.Info=res.data
            })
          }
      },
      created(){
          this.getUser();
      }
    }
</script>

<style scoped>
@import "../../style/perinfor.css";
</style>
