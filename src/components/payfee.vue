<template>
    <div class="payfee-container">
      <mt-header title="缴纳党费" fixed>
        <mt-button icon="back" @click="$router.back()" slot="left">
        </mt-button>
      </mt-header>

      <div class="moneypay">
        <div class="choice">请选择支付方式</div>
        <div class="money-list">
          <!--微信-->
          <div class="money-item" @click="handleClick1">
            <i class="iconfont icon-weixin"></i>
            <span>微信</span>
            <i class="iconfont icon-jiantouyou"></i>
          </div>
          <mt-popup v-model="popupVisible1" modal=false class="popup">
            <p>微信支付</p>
            <img src="../assets/wechat.png">
          </mt-popup>
          <!--支付宝-->
          <div class="money-item" @click="handleClick2">
            <i class="iconfont icon-alipay"></i>
            <span>支付宝</span>
            <i class="iconfont icon-jiantouyou"></i>
          </div>
          <mt-popup v-model="popupVisible2" modal=false class="popup">
            <p>支付宝支付</p>
            <img src="../assets/alipay.png">
          </mt-popup>
        </div>
      </div>

    </div>
</template>

<script>
  export default {
    data(){
      return{
      popupVisible1:false,
      popupVisible2:false,
    }
    },
    methods: {
      handleClick1() {
        this.popupVisible1 = true;
      },
      handleClick2() {
        this.popupVisible2 = true;
      },
    }
  }
</script>

<style scoped>
.moneypay{margin-top: 50px}
.moneypay{
  margin-top: 44px;
}
.choice{
  font-size: 15px;
  padding: 20px 0 10px;
  color: #000;
}
.money-item{
  padding: 20px 54px 20px 61px;
  border: 1px solid #ddd;
  background-color: #fff;
  color: #444;
  position: relative;
  z-index: 2;
  display: block;
  margin: -1px;
  font-size: 16px;
}
.icon-weixin{
  color: #6cc143;
  left: 11px;
  display: flex;
  align-items: center;
  position: absolute;
  top: 0;
  height: 100%;
  font-size: 40px;
}
.icon-alipay{
  color: #1296db;
  left: 11px;
  display: flex;
  align-items: center;
  position: absolute;
  top: 0;
  height: 100%;
  font-size: 40px;
  padding: 0;
}
.icon-jiantouyou{
  width: 32px;
  text-align: center;
  line-height: 1;
  font-size: 21px;
  position: absolute;
  right: 11px;
  color: #ADB2B2;
}
.popup p{
  font-size: 20px;
  line-height: 2;
  text-align: center;
  color: #000;
}
.popup img{
  width: 300px
}
</style>
