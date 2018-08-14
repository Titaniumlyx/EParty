<template>
    <div class="memberhd-container">
      <mt-header title="党员云互动" fixed>
        <mt-button icon="back" @click="back" slot="left">
        </mt-button>
      </mt-header>

      <div class="memberhd-content">
        <div class="memberhd-list">
          <ul>

            <li class="memberhd-item" v-for="item in lists" :key="item._id">
              <div class="item-top clearfix">
                <div class="top-touxiang">
                  <img src="../assets/touxi.png" alt="">
                </div>
                <div class="top-zhong">
                  <div class="top-nickname">{{item.idNum}}</div>
                  <div class="top-time">
                    <div class="top-time1">
                      <i class="iconfont icon-shijian"></i>
                      <span>{{item.createTime}}</span>
                    </div>
                    <div class="top-time2">
                      <i class="iconfont icon-laba"></i>
                      <span>公开</span>
                    </div>
                  </div>
                </div>
                <div class="top-right">党员互动</div>
              </div>

              <div class="item-middle">{{item.content}}</div>

              <router-link :to="'/hfsth?id='+item._id" :key="item._id" class="item-bottom clearfix">
                <span class="bottom-hf">
                  <i class="iconfont icon-xiaoxi"></i>
                  <span>回复</span>
                </span>
              </router-link>
            </li>

          </ul>
        </div>

        <div class="fabu" @click="handleClick">
          <i class="iconfont icon-add"></i>
        </div>
      </div>

      <mt-popup v-model="popupVisible" position="bottom" modal=false class="memberhd-popup">
        <div class="memberhd-kuang">
          <form class="addsth">
            <textarea v-model="Text"></textarea>
            <div class="btns">
              <input type="button" value="发布" class="fb" @click="publish">
              <input type="button" value="取消" class="qx" @click="canc">
            </div>
          </form>
        </div>
      </mt-popup>

    </div>
</template>

<script>
  import { Toast } from 'mint-ui';
    export default {
        name: "memberhd",
      data(){
          return{
            popupVisible:false,
            lists:[],
            Text:""
          }
      },
      methods:{
        back(){
          this.$router.push({path:"/shouye"});
        },
        handleClick(){
          this.popupVisible=true
        },
        getList(){
          this.$axios.get("getList").then(res=>{
            console.log(res.data);
            this.lists=res.data;
            if(res.code == 400){
              Toast("没有登录，请登录..");
              this.$router.push({path:"/login",query:{mark:"memberhd"}});
            }
            for (var i=0;i<this.lists.length;i++){
              var createTime = res.data[i].createTime;
              var date = new Date(createTime);
              var Y = date.getFullYear() + '-';
              var M = (date.getMonth()+1 < 10 ? '0'+(date.getMonth()+1) : date.getMonth()+1) + '-';
              var D = date.getDate() + ' ';
              var h = date.getHours() + ':';
              var m = date.getMinutes() + ':';
              var s = date.getSeconds();
              console.log(Y+M+D+h+m+s);
              this.lists[i].createTime = Y+M+D+h+m+s;
            }
          })
        },
        publish(){
          this.$axios.post("addTie",{content:this.Text}).then(res=>{
            console.log(res);
            if (res.msg=="success"){
              this.$router.go(0);
            }
          })
        },
        canc(){
          this.popupVisible=false;
        }
      },
      created(){
          this.getList()
      }
    }
</script>

<style scoped>
  @import "../../style/memberhd.css";
</style>
