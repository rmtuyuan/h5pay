<template>
  <div id="app">
    <div class="id-box">
      <div>
        <h4>充值账户:</h4>
        <el-row>
          <el-col :span="18">
            <el-input v-model="id" type="tel" v-if="idCheck" placeholder="请输入全民ID" round></el-input>
            <div class="el-input" v-if="idChange" round="">
              <div class="container app-family-list-con clearfloat" >
                <div class="app-family-left"> <img src="http://qmwlzb-one.oss-cn-beijing.aliyuncs.com/img_1509602356819.jpg"
                    alt=""></div>
                <div class="app-family-mid">
                  <p>龙天下</p><span>ID1</span></div>
             
              </div>
          </div>
          </el-col>
          <el-col :span="6">
            <el-button type="" v-if="idCheck" @click="handleIDChange" round>确认</el-button>
            <el-button type="primary" v-if="idChange" @click="handleIDChange" round>切换账户</el-button>
          </el-col>
        </el-row>
      </div>
    </div>

    <el-button type="primary" @click="open">主要按钮</el-button>


  </div>
</template>

<script>
  export default {
    name: 'app',
    data() {
      return {
        id: '',
        idCheck: true,
        idChange: false
      }
    },
    methods: {
      open: function () {
        this.$confirm('全名直播', '标题', {
          confirmButtonText: '确定',
          $message: ({
            type: 'info'
          }),
          showCancelButton: false

        })
      },
      handleIDChange() {
        //
        this.idChange = !this.idChange;
        this.idCheck = !this.idCheck
      },
      handleIDCheck() {

      }
    }
  }

</script>

<style lang="scss">
  // $base-color:#fe416e;
  html {
    padding: 0;
    margin: 0;
  }

  body {
    margin: 0;
    padding: 0;
    width: 7.5rem;
    background: #f0f0f0;
  }

  .id-box {
    background: #fff;
    width: 100%;
    margin: .2rem auto;
    padding: .2rem 0;
  }
.id-box button.el-button.is-round{
  width: 80%;
  padding:12px 0;
  text-align: center;

}
  .id-box>div {
    width: 96%;
    margin: 0 auto;
  }

  .id-box h4 {
    font-size: .26rem;
    padding: 0;
    margin: 0;
    text-align: left;
  }

  .id-box button:focus {
    background: #fff;
  }

  .app-family-left{
    width: 44px;
  
    text-align: center;
     display: flex;
    display: -webkit-box;
    /* 老版本语法: Safari, iOS, Android browser, older WebKit browsers. */
    display: -moz-box;
    /* 老版本语法: Firefox (buggy) */
    display: -ms-flexbox;
    /* 混合版本语法: IE 10 */
    display: -webkit-flex;
    /* 新版本语法: Chrome 21+ */
    align-items: flex-end;
    -webkit-box-align: flex-end;
    -moz-align-items: flex-end;
    -webkit-align-items: flex-end;
    flex-direction: column;
     -moz-flex-direction: column;
    -webkit-flex-direction: column;
}
.app-family-icon{
    display:block;
    width: 24px;
    height: 16px;
   
}
.app-family-list-con{
    position: relative;
}
.app-family-list-con>div{
    float: left;
}

.app-family-left img{
    display:block;
    width: 41px;
    height: 41px;
    border-radius: 50%;
}

.app-family-mid{
    
    height: 100%;
    line-height: 0;
    margin-left: .1rem;
    padding-top: .35rem;
}
.app-family-mid p{
    width: 100%;
    margin: 0;
    font-size: .18rem;
    color: rgb(64,64,64);
    margin-bottom: .15rem;
    margin-top: .1rem;
    font-weight: 600;
}
.app-family-mid span{
   font-size: .14rem;
}
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    width: 100%;
    margin: 0 auto;

    /*margin-top: 60px;*/
  }

  .el-message-box {
    width: 80%; // background: #fe416e;
  }

</style>
