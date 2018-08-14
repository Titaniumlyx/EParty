<template>
    <div class="cppartymem-container">
      <mt-header title="参评党员" fixed>
        <mt-button icon="back" @click="back" slot="left">
        </mt-button>
      </mt-header>

      <div class="ctn" v-for="user in users">
        <router-link :to ="'/pingyiPL?id='+user._id">
          <div class="mi">
            <img :src="user.header">
            <span>{{user.username}}</span>
          </div>

          <div class="ri">
            <span>{{user.branchName}}</span>
          </div>

        </router-link>
      </div>

    </div>
</template>

<script>
    export default {
        name: "cppartymem",
      data(){
        return{
          users:[{
            branchId: "",
            branchName: "",
            createIime: "",
            header: "",
            idCard: "",
            partyIdentity: "",
            partyStatus: "",
            updatetime: "",
            username: "",
            _id: "",
          }] ,
          branchs:[
            {}
          ],
        }
      },
      created(){
        this.getuserlist();
      },
      methods: {
        back(){
          this.$router.push("/discuss")
        },
        getuserlist() {
          this.$axios.get("getPartyman", {branchId:this.$route.query.id}).then(res => {
            this.users= res.data.data;
            // console.log(res);
          })
        }
      }
    }
</script>

<style scoped>
  .ctn{
    width: 97%;
    height: 54px;
    line-height: 54px;
    margin: 50px auto 0;
    font-size: 15px;
    color: #666666;
    border-bottom: 1px solid #bababa;
  }
  .ctn a{display: flex;}
  .ctn .mi {
    flex: 0.8;
  }
  .ctn .mi img{
    width: 32px;
    height: 32px;
  }
  .ctn .mi span{
    margin-left: 12px;
  }
  .ri{
    flex: 2.4;
    text-align: right;
  }
</style>
