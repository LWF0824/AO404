<template>
  <div>
    <div class="hello">
      <Guidebar></Guidebar>
    </div>
    <div id="page-content">
      <el-row>
        <el-col :span="6">
          <div class="grid-content">
            <div id="menu">
              <el-row class="tac">
                <el-col class="tac-menu">
                  <div id="menutitle"><h id="menu-title">个人主页</h></div>
                  <hr color=#EFEEEE SIZE=1>
                  <el-menu default-active="4-2" class="el-menu-vertical-demo" @open="handleOpen" @close="handleClose">
                    <el-menu-item index="1" @click="personalpage">
                      <i class="icon-person"></i>
                      <span slot="title">我的主页</span>
                    </el-menu-item>
                    <el-menu-item index="2" @click="followlist">
                      <i class="icon-follow"></i>
                      <span slot="title">我的关注</span>
                    </el-menu-item>
                    <el-menu-item index="3" @click="fanlist">
                      <i class="icon-fan"></i>
                      <span slot="title">我的粉丝</span>
                    </el-menu-item>
                    <el-submenu index="4">
                      <template slot="title">
                        <i class="icon-setting"></i>
                        <span>账号管理</span>
                      </template>
                      <el-menu-item-group>
                        <el-menu-item index="4-1" @click="userinfo">账号资料</el-menu-item>
                        <el-menu-item index="4-2" @click="accountsecurity">账号安全</el-menu-item>
                      </el-menu-item-group>
                    </el-submenu>
                  </el-menu>
                </el-col>
              </el-row>
            </div>
          </div>
        </el-col>
        <el-col :span="18">
          <div class="grid-content">
            <div id="user-info">
              <div id="info">账号安全</div>
              <hr color=#EFEEEE SIZE=1>
              <div id="photoblock"><p><img v-bind:src="pic" id="headphoto"></p></div>
              <div id="userinfo">
                <p>账&ensp;号&ensp;ID：{{user_id}}</p>
                <p>昵&emsp;&emsp;称：{{user_name}}</p>
                <p>密&emsp;&emsp;码：*</p>
                <el-button id="changeinfo" @click="pswDialogVisible = true">修改密码</el-button>
                <el-dialog title="修改资料" :visible.sync="pswDialogVisible" width="40%" center>
                  <div id="input-psw">
                    <p>请输入原密码&emsp;：<el-input placeholder="请输入原密码" v-model="inputOldpsw" show-password style="width: 300px"></el-input></p>
                    <p>请输入新密码&emsp;：<el-input placeholder="请输入新密码" v-model="inputNewpsw" show-password style="width: 300px"></el-input></p>
                    <p>再次输入新密码：<el-input placeholder="再次输入新密码" v-model="inputNewpswAgain" show-password style="width: 300px"></el-input></p>
                  </div>
                  <span slot="footer" class="dialog-footer">
                    <el-button @click="pswDialogVisible = false">取消修改</el-button>
                    <el-button type="primary" @click="confirmpswDialogVisible = true">提交修改</el-button>
                    <el-dialog title="提示" :visible.sync="confirmpswDialogVisible" width="25%" center append-to-body>
                      <span>确认提交修改？</span>
                      <span slot="footer" class="dialog-footer">
                        <el-button @click="confirmpswDialogVisible = false">取 消</el-button>
                        <el-button type="primary" @click="changePsw()">确 定</el-button>
                      </span>
                    </el-dialog>
                  </span>
                </el-dialog>
              </div>
            </div>
          </div>
        </el-col>
      </el-row>
    </div>
  </div>
</template>

<script>
import Guidebar from '@/components/Guidebar'
export default {
  name: 'AccountSecurity',
  components: {
    Guidebar
  },
  methods: {
    handleOpen(key, keyPath) {
      console.log(key, keyPath);
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath);
    },
    personalpage() {
      this.$router.push({path: '/PersonalPage'});
    },
    followlist() {
      this.$router.push('/FollowList');
    },
    fanlist() {
      this.$router.push({path: '/FanList'});
    },
    userinfo() {
      this.$router.push({path: '/UserInfo'});
    },
    accountsecurity() {
      this.$router.push({path: '/AccountSecurity'});
    },
    changePsw() {
      console.log(this.inputOldpsw,this.inputNewpsw,this.inputNewpswAgain),
      this.pswDialogVisible=false,
      this.confirmpswDialogVisible=false,
      this.$message({
          message: '修改密码成功！',
          type: 'success'
        });
    }
  },
  data() {
    return {
      user_id: 12345,
      user_name: '原神',
      pic: require('../../src/assets/mlogo.png'),
      inputOldpsw: '',
      inputNewpsw: '',
      inputNewpswAgain: '',
      pswDialogVisible: false,
      confirmpswDialogVisible: false
    }
  }
}
</script>

<style>
  .el-row {
    margin-bottom: 20px;
  }
  .el-col {
    border-radius: 4px;
    padding: 10px;
  }
  .grid-content {
    border-radius: 4px;
    min-height: 36px;
  }
  .row-bg {
    padding: 10px 0;
    background-color: #f9fafc;
  }
  #page-content {
    width: 1200px;
    margin: 0px auto;
    margin-top: 30px;
  }
  #user-info {
    border-style: solid;
    border-width: 2px;
    border-color: #e5e9f2;
    border-radius: 4px;
  }
  #info {
    font-size: 20px;
    margin-top: 15px;
    margin-left: 25px;
    margin-bottom: 10px;
  }
  #photoblock{
    text-align:center;
  }
  #headphoto {
    width: 120px;
  }
  #userinfo {
    margin-left: 360px;
    font-size: 18px;
    margin-bottom: 40px;
  }
  #changeinfo {
    margin-left: 20px;
    margin-top: 20px;
  }
  #input-psw {
    text-align:center;
    font-size: 16px;
  }

   /*菜单*/
  #menu {
    width: 250px;
    text-align:left
  }
  .tac-menu {
    padding: 0px;
    padding-bottom: 10px;
    border-style: solid;
    border-width: 2px;
    border-color: #DBD8D3;
    border-radius: 4px;
  }
  #menutitle{
    margin-top: 10px;
  }
  #menu-title {
    margin-left: 20px;
    font-size: 24px;
  }
  .icon-person {
    content: url(../../src/assets/user_pic.png);
    width: 18px;
    margin-left: 5px;
    margin-right: 10px;
  }
  .icon-follow {
    content: url(../../src/assets/follow_pic.png);
    width: 18px;
    margin-left: 5px;
    margin-right: 10px;
  }
  .icon-fan {
    content: url(../../src/assets/fan_pic.png);
    width: 18px;
    margin-left: 5px;
    margin-right: 10px;
  }
  .icon-setting {
    content: url(../../src/assets/setting_pic.png);
    width: 18px;
    margin-left: 5px;
    margin-right: 10px;
  }
</style>