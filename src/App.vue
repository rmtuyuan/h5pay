<template>
  <div id="app">
    <div class="id-box">
      <div>
        <h4>充值账户:</h4>
        <el-row align="center" type="flex">
          <el-col :span="18">
            <el-input onkeypress="return event.keyCode>=48&&event.keyCode<=57" v-model="id" type="tel" v-if="idCheck" placeholder="请输入全民ID" round></el-input>

            <div class="container app-family-list-con clearfloat" v-if="idChange">
              <div class="app-family-left"> <img src="http://qmwlzb-one.oss-cn-beijing.aliyuncs.com/img_1509602356819.jpg" alt=""></div>
              <div class="app-family-mid">
                <p>龙天下</p><span>ID1</span></div>

            </div>

          </el-col>
          <el-col :span="6">
            <el-button type="" v-if="idCheck" @click="handleIDCheck" round>确认</el-button>
            <el-button type="primary" v-if="idChange" @click="handleIDChange" round>切换账户</el-button>
          </el-col>
        </el-row>
      </div>
    </div>
    <div class="momey-list-box">
      <div class="momey-list">
        <el-row class="momey-list-row">
          <el-col :span="8" v-for="item in moneyList" :key="item.id">
            <div class="momey-list-col" :class="{active:item.id===moneyId}" @click="checkMoney(item.id,item.rmb)">
              <span v-text="item.id?item.diamond+'钻石':'自定义'"></span>
              <p v-if="item.id">￥{{item.rmb}}</p>
            </div>
          </el-col>

        </el-row>
        <el-row class="momey-list-row" v-if="money==0||moneyId==0">
          <el-col :span="6">
            <el-button type="text"><span class="text-gray">充值金额:</span></el-button>
          </el-col>
          <el-col :span="8">
            <el-input :maxlength="8" onkeypress="return event.keyCode>=48&&event.keyCode<=57" v-model.number="money" @keyup.native="moneyInput" type="tel" placeholder="请输入金额" round></el-input>
          </el-col>
          <el-col :span="2">
            <el-button type="text"><span class="text-gray">元</span></el-button>
          </el-col>
        </el-row>
        <el-row >
          <el-col :span="6">
            <el-button type="text"><span class="text-gray">应付金额:</span></el-button>
          </el-col>

          <el-col :span="2">
            <el-button type="text">{{money}} <span class="text-gray">元</span></el-button>
          </el-col>
        </el-row>
      </div>
    </div>
    <el-row>
      <el-col :span="24">
        <el-button type="" @click="open" :class="{active:money>0&&idChange}" class="submit-button">提交订单 ￥{{money}}</el-button>
      </el-col>
    </el-row>


  </div>
</template>

<script>
  export default {
    name: 'app',
    data() {
      return {
        id: '', //userId
        moneyId: 2, //moneyid
        idCheck: true, //
        idChange: false,
        money: 60, //money
        moneyList: [{
            id: 1,
            diamond: '60',
            rmb: '6'
          },
          {
            id: 2,
            diamond: '600',
            rmb: '60'
          },
          {
            id: 3,
            diamond: '6000',
            rmb: '600'
          },
          {
            id: 4,
            diamond: '60000',
            rmb: '6000'
          },
          {
            id: 0,
            diamond: '0',
            rmb: '0'
          }
        ]

      }
    },
    methods: {
      open: function () {
        if(this.idChange&&this.money>0){
          this.$confirm('确定充值', '', {
          confirmButtonText: '确定',
          $message: ({
            type: 'info'
          }),
          showCancelButton: false

        })
        }
        
      },
      //切换账号
      handleIDChange() {
        //
        this.idChange = !this.idChange;
        this.idCheck = !this.idCheck
      },
      // 确认账号
      handleIDCheck() {
        let userID = this.id;
        let idReg = /(^[1-9]\d*$)/;
        if (userID.length > 0) {
          if (idReg.test(userID)) {
            //$http 成功赋值 切换 
            this.idChange = !this.idChange;
            this.idCheck = !this.idCheck
          } else {
            //不是正整数
            this.$message({
              message: '请输入正确全民ID',
              type: 'error',
              duration: 1000
            });
          }
        } else {
          this.$message({
            message: '请输入全民ID',
            type: 'error',
            duration: 1000
          });
        }
      },
      //选择套餐 
      checkMoney(id, rmb) {
        this.moneyId = id;
        this.money = rmb;
      },
      //自定义输入金额
      moneyInput() {
      
    
      }

    }
  }

</script>

<style lang="scss">
  // $base-color:#fe416e;
  html,
  p {
    padding: 0;
    margin: 0;
  }

  body {
    margin: 0;
    padding: 0;
    width: 7.5rem;
    background: #f0f0f0;
    font-size: .16rem;
  }

  .id-box {
    background: #fff;
    width: 100%;
    margin: .2rem auto;
    padding: .2rem 0;
  }

  .id-box button.el-button.is-round {
    width: 80%;
    padding: 12px 0;
    text-align: center;
  }

  .id-box>div,
  .momey-list {
    width: 96%;
    margin: 0 auto;
  }

  .id-box h4 {
    font-size: .26rem;
    padding: 0;
    margin: 0;
    text-align: left;
    margin-bottom: .2rem;
  }

  .el-message {
    min-width: 80%;
    width: 80%;
  }

  .id-box button:focus {
    background: #fff;
  }

  .app-family-list-con {
    overflow: hidden;
    height: 100%;
    display: flex;
    align-items: flex-end;
  }

  .app-family-left {
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

  .app-family-icon {
    display: block;
    width: 24px;
    height: 16px;
  }

  .app-family-list-con {
    position: relative;
  }

  .app-family-list-con>div {
    float: left;
  }

  .app-family-left img {
    display: block;
    width: 41px;
    height: 41px;
    border-radius: 50%;
  }

  .app-family-mid {

    height: 41px;
    line-height: 0;
    margin-left: .1rem;
    margin-top: .1rem;
    text-align: left;
  }

  .text-gray {
    color: #666;
  }

  .text-red {
    color: #fe416e;
  }

  .app-family-mid p {
    width: 100%;
    margin: 0;
    font-size: .2rem;
    color: rgb(64, 64, 64);
    margin-bottom: .3rem;
    margin-top: .2rem;
    font-weight: 600;
  }

  .app-family-mid span {
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

  .momey-list-box {
    margin-top: .2rem;
    background: #fff;
    padding: .2rem 0;
  }

  .momey-list-col {
    width: 85%;
    height: .88rem;
    color: #fe416e;
    border-radius: .44rem;
    font-size: .16rem;
    text-align: center;
    margin: 0;
    border: 1px solid #d8dce5;
    padding: 0;
    display: flex;
    display: -webkit-box;
    /* 老版本语法: Safari, iOS, Android browser, older WebKit browsers. */
    display: -moz-box;
    /* 老版本语法: Firefox (buggy) */
    display: -ms-flexbox;
    /* 混合版本语法: IE 10 */
    display: -webkit-flex;
    /* 新版本语法: Chrome 21+ */
    align-items: center;
    justify-content: center;
    -webkit-box-align: center;
    -moz-align-items: center;
    -webkit-align-items: center;
    flex-direction: column;
    -moz-flex-direction: column;
    -webkit-flex-direction: column;

    -webkit-box-pack: center;
    -moz-justify-content: center;
    -webkit-justify-content: center;
    margin: .1rem 0;
  }

  .momey-list-col.active {
    background: #fe416e;
    color: #fff;
    border: 1px solid #fe416e;
  }

  .momey-list-row {
    margin: .3rem 0;
  }

  .submit-button {
    width: 90%;
    margin: .3rem;
    font-size: .36rem;
    box-sizing: border-box;
  }
  .submit-button{
    background: #ccc;
    border-radius: .4rem;
  }
   .submit-button:focus{
     background: #ccc;
    border-radius: .4rem;
    color: #666;
    border: 1px solid #ccc;
   }
   .submit-button.active{
      background: #fe416e;
      color: #fff;
   }
</style>
