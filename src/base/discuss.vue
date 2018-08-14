<template>
    <div class="discuss-container">
      <mt-header title="民主评议" fixed>
        <mt-button icon="back" @click="back" slot="left">
        </mt-button>
      </mt-header>

      <div class="discuss-content">
        <div class="discuss-wrap">
          <p class="noteHead">评议须知</p>
          <div class="noteContent">
            <p v-html="discuss.content"></p>
            <p>{{discuss.contentText}}</p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
            <p></p>
          </div>

          <div class="noteChoice">
            <div class="clearfix">
              <div class="selectBtn">
                <select name="partyStatus" class="branchSelect fleft" v-model="branch_id">
                  <option :value="branch._id" v-for="branch in branchs">{{branch.label}}</option>
                </select>
              </div>
              <div class="nextBtn fleft" @click="btn">下一步</div>
            </div>
          </div>
        </div>
      </div>

    </div>
</template>

<script>
    export default {
        name: "discuss",
      data(){
        return{
          discuss:[
            {
              content: "",
              contentText: "",
              createdAt: "",
              title: "",
              updatedAt: "",
              _id: "",
            }
          ],
          branchs:[
            {}
          ],
          branch_id:""
        }
      },
      methods: {
        back(){
          this.$router.push("/minzhu")
        },
        btn(){
          this.$router.push({path: '/cppartymem?id='+this.branch_id})
        },
        getbranch(){
          this.$axios.get("getBranch").then(res => {
            this.branchs=res.data;
            // console.log(res);
          })
        },
        getdiscuss(){
          this.$axios.get("getDiscuss").then(res => {
            this.discuss=res.data
            // console.log(res.data);
          })
        }
      },
      created(){
        this.getdiscuss();
        this.getbranch();
      }
    }
</script>

<style scoped>
  @import "../../style/discuss.css";
</style>
