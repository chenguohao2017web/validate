<template>
  <div id="app">
    <div class="container">
      <div class="form-warp">
        <div class="group">
          <label class="text" for="username">username:</label>
          <input type="text" 
                  v-model="username"
                  id="username" 
                  class="input user-input" 
                  placeholder="username/email"
          >
        </div>
        <div class="group">
          <label class="text" for="password">password:</label>
          <input type="password" 
                  v-model="password"
                  id="password" 
                  class="input user-input" 
                  placeholder="password"
          >
        </div>
        <button class="submit" @click="handleSubmit" >submit</button>
        <div class="bottom-group">
          <div class="skip-btn forget">fortget your password ?</div>
          <div class="skip-btn register">register</div>
        </div>
      </div>
      <!-- 弹出窗 -->
      <div :class="['modal',{fade:modal_is_show}]" v-show="modal_is_show" @click="handle_hide_modal"> 
        <div class="modal-title">ERROR !  </div>
        <div class="modal-body">{{err_msg}}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      err_msg: "",
      modal_is_show: false,
      username: "",
      password: ""
    };
  },
  methods: {
    handleSubmit() {
      let ret = this.vaildata();
      if (!ret) {
        this.modal_is_show = true;
      } else {
        alert('提交成功ajax')
      }
    },
    handle_hide_modal() {
      this.modal_is_show = false;
    },
    vaildata() {
      //返回false时 弹出错误信息  true
      let allNums_reg = /^\d{5,20}$/;
      let allEn_reg = /^[a-zA-Z]{5,20}$/;
      if (this.username == "") {
        this.err_msg = "username不能为空";
        return false;
      } else if (this.username.length < 5) {
        this.err_msg = "username必须英文和数字组合5-20位";
        return false;
      } else if (allNums_reg.test(this.username)) {
        this.err_msg = "username必须英文和数字组合5-20位";
        return false;
      } else if (allEn_reg.test(this.username)) {
        this.err_msg = "username必须英文和数字组合5-20位";
      } else if (this.password == "") {
        this.err_msg = "password不能为空";
        return false
      }else if (allNums_reg.test(this.password)) {
        this.err_msg = "password必须英文和数字组合";
        return false
      }else if (allEn_reg.test(this.password)) {
        this.err_msg = "password必须英文和数字组合";
        return false
      }else {
        return true
      }
    }
  }
};
</script>

<style lang="less" scoped>
.container {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: 20px;
  .form-warp {
    padding: 20px;
    width: 650px;
    background: rgba(0, 0, 0, 0.3);
    display: flex;
    flex-direction: column;
    .group {
      display: flex;
      align-items: center;
      margin-bottom: 20px;
      &:last-child {
        margin-bottom: 0;
      }
      .text {
        width: 150px;
        color: #fff;
        font-size: 28px;
        margin-right: 20px;
      }
      .input {
        padding-left: 10px;
        font-size: 28px;
        flex: 1;
        height: 80px;
        border: none;
        background: transparent;
        border-bottom: 1px solid rgba(250, 250, 250, 0.5);
        &:focus {
          outline: none;
        }
      }
    }
    .submit {
      margin-top: 30px;
      padding: 20px 0;
      background: #bf7070;
      border: none;
      border-radius: 10px;
      color: #fff;
      font-size: 28px;
      &:focus {
        outline: none;
      }
    }
    .bottom-group {
      margin-top: 20px;
      display: flex;
      justify-content: space-between;
      color: #fff;
      font-size: 28px;
      .skip-btn {
        padding: 20px 0;
      }
    }
  }
  .modal {
    position: absolute;
    top: 50%;
    left: 50%;
    width: 600px;
    background: #fff;
    box-shadow: 0 0 2px rgba(0, 0, 0, 0.3);
    transform: translate3d(-50%, -50%, 0);
    border-radius: 10px;
    overflow: hidden;
    &.fade {
      animation: fade 1s ease;
    }
    .modal-title {
      font-size: 30px;
      height: 80px;
      line-height: 80px;
      padding-left: 30px;
      background: #ccc;
      color: #9c9ca0;
    }
    .modal-body {
      padding: 30px;
      background: #fff;
      font-size: 36px;
      color: #666;
    }
  }
}
@keyframes fade {
  from {
    transform: translate3d(-50%, -70%, 0);
    opacity: 0;
  }
  to {
    transform: translate3d(-50%, -50%, 0);
    opacity: 1;
  }
}
</style>
