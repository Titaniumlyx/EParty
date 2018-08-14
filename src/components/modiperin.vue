<template>
    <div class="modiperin-container">
      <mt-header title="修改个人信息">
        <mt-button icon="back" @click="$router.back()" slot="left">
        </mt-button>
        <div slot="right" @click="getModify">保存</div>
      </mt-header>

      <div class="modiperin-content">
        <form class="modiperin-list">
          <div class="info-item">
            <span>头像</span>
            <img :src="Info.avatar" alt="">
          </div>
          <div class="info-item">
            <span>姓名</span>
            <span><input type="text" name="username" id="username" v-model="Info.userName"></span>
          </div>
          <div class="info-item">
            <span>身份证</span>
            <span v-model="Info.idNum"></span>
          </div>
          <div class="info-item">
            <span>家庭住址</span>
            <span><input type="text" name="hometown" id="hometown" v-model="Info.homeAddress"></span>
          </div>
          <div class="info-item">
            <span>工作地址</span>
            <span><input type="text" name="address" id="address" v-model="Info.workAddress"></span>
          </div>
          <div class="info-item">
            <span>民族</span>
            <span><input type="text" name="nation" id="nation" v-model="Info.nation"></span>
          </div>
          <div class="info-item">
            <span>微信号</span>
            <span><input type="text" name="wxNum" id="wxNum" v-model="Info.weChat"></span>
          </div>
          <div class="info-item">
            <span>qq号</span>
            <span><input type="text" name="qqNum" id="qqNum" v-model="Info.qqNumber"></span>
          </div>
          <div class="info-item">
            <span>性别</span>
            <span class="sexopti" v-model="Info.sex">
              <input type="radio" name="sex" value="1"><i>男</i>
              <input type="radio" name="sex" value="0"><i>女</i>
            </span>
          </div>
          <div class="info-item">
            <span>最高学历</span>
            <span><input type="text" name="education" id="education" v-model="Info.education"></span>
          </div>
          <div class="info-item">
            <span>职称</span>
            <span><input type="text" name="jobRank" id="jobRank" v-model="Info.jobTitle"></span>
          </div>
          <div class="info-item">
            <span>薪资水平</span>
            <span><input type="number" name="salary" id="salary" v-model="Info.emolument"></span>
          </div>
          <div class="info-item">
            <span>入党时间</span>
            <span><input type="date" name="joinPartyTime" id="joinPartyTime" v-model="Info.enterPartyTime"></span>
          </div>
          <div class="info-item">
            <span>党费最后缴纳时间</span>
            <span><input type="date" name="lastPayTime" id="lastPayTime" v-model="Info.paymentTime"></span>
          </div>
          <div class="info-item">
            <span>当前身份</span>
            <span v-model="Info.partyStatus">
              <select name="partyStatus">
                <option value="2">党员</option>
                <option value="1">预备党员</option>
                <option value="0">积极分子</option>
              </select>
            </span>
          </div>
        </form>
      </div>

    </div>
</template>

<script>
    export default {
        name: "modiperin",
      data(){
          return{
            Info:{
              userName:"",idNum:"",homeAddress:"",workAddress:"",nation:"",weChat:"",qqNumber:"",sex:"",education:"",jobTitle:"",emolument:"",enterPartyTime:"",paymentTime:"",partyStatus:"",avatar:""}
          }
      },
      methods:{
        getUser(){
          this.$axios.get("getUsersinfo").then(res=>{
            console.log(res);
            this.Info=res.data
          })
        },
        getModify(){
          this.$axios.post("getModify",this.Info).then(res=>{
            console.log(res);
            if(res.code==200){
              this.$router.push({path:'/perinfor'})
            }
          })
        }
      },
      created(){
          this.getUser()
      }
    }
</script>

<style scoped>
  @import "../../style/modiperin.css";
  input[type=radio] {
    -webkit-appearance: radio;
  }
</style>
