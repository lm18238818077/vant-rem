<template>
  <div class="apply">
    <van-nav-bar
      title="申请免费试用"
      left-arrow
      @click-left="onClickLeft"
    ></van-nav-bar>
    <div class="apply_top">
      <div class="title">申请免费试用</div>
    </div>
    <div class="wrap">
      <van-form @submit="onSubmit" :show-error="false">
        <div class="type">企业信息</div>
        <van-field
          v-model="form.name"
          name="企业名称"
          label="企业名称"
          placeholder="请输入企业名称"
          :rules="[{ required: true, message: '请填写企业名称' }]"
        ></van-field>
        <van-field
          v-model="form.contact_people"
          type="text"
          name="联系人"
          label="联系人"
          placeholder="请输入联系人姓名"
          :rules="[{ required: true, message: '请填写联系人姓名' }]"
        ></van-field>
        <div class="type">手机号验证</div>
        <van-field
          v-model="form.contact_mobile"
          name="手机号"
          label="手机号"
          placeholder="请输入手机号"
          :rules="[
            { required: true, message: '请填写手机号' },
            { validator, message: '请填写正确的手机号' },
          ]"
        ></van-field>
        <van-field
          v-model="form.code"
          type="number"
          name="验证码"
          label="验证码"
          placeholder="请输入验证码"
          :rules="[
            { required: true, message: '请填写验证码' },
            { pattern: /\d+/, message: '请填写正确的验证码' },
          ]"
        >
          <template #button>
            <span
              class="code"
              :class="disabled ? 'disabled' : ''"
              @click="sendcode"
              >{{ btntxt }}</span
            >
          </template>
        </van-field>

        <van-button block type="info" native-type="submit" class="button"
          >免费试用</van-button
        >
      </van-form>
    </div>
  </div>
</template>

<script>
import {
  Toast,
  NavBar,
  Form,
  Field,
  Button,
  Dialog,
} from "vant";

export default {
  components: {
    [NavBar.name]: NavBar,
    [Form.name]: Form,
    [Field.name]: Field,
    [Button.name]: Button,
    [Toast.name]: Toast,
    [Dialog.name]: Dialog,
  },

  data() {
    return {
      form: {
        name: "",
        contact_people: "",
        contact_mobile: "",
        code: "",
        area_num: "86",
      },
      disabled: false,
      time: 60,
      btntxt: "发送验证码",
    };
  },

  methods: {
    onClickLeft() {
      window.history.back();
    },
    validator() {
      return /^1[3456789]\d{9}$/.test(this.form.contact_mobile);
    },
    onSubmit() {
      fetch("https://api-lms3.9first.com/user/company", {
        method: "POST",
        body: JSON.stringify(this.form),
      })
        .then((response) => response.json())
        .then((json) => {
          if (json.status == 1) {
            Dialog.alert({
                title: "已提交试用",
                message:
                  '培训顾问会在24小时内与您联系，有疑问可拨打 <a class="blue" href="tel:0571-87765425">0571-87765425</a>',
                confirmButtonColor: "#007AFF",
              })
              .then(() => {
                window.history.back();
              });
          } else {
            Toast(json.errMsg);
          }
        })
        .catch(function () {});
    },
    sendcode() {
      if (this.disabled) return;
      if (!this.validator()) return;
      this.time = 60;
      this.timer();
      fetch("https://api-lms3.9first.com/user/sms", {
        method: "POST",
        body: JSON.stringify({
          scenario: "register",
          mobile: this.form.contact_mobile,
          area_num: "86",
        }),
      })
        .then((response) => response.json())
        .then(function (json) {
          if (json.status == 1) {
            Toast("已发送");
          } else {
            Toast(json.errMsg);
          }
        })
        .catch(function () {});
    },
    //发送手机验证码倒计时
    timer() {
      if (this.time > 0) {
        this.disabled = true;
        this.time--;
        this.btntxt = this.time + "秒后重新获取";
        setTimeout(this.timer, 1000);
      } else {
        this.time = 0;
        this.btntxt = "发送验证码";
        this.disabled = false;
      }
    },
  },
};
</script>

<style lang="less">
.apply .apply_top {
  height: 190px;
  overflow: hidden;
  background: #1890ff;
}
.apply .apply_top .title {
  font-size: 24px;
  text-align: center;
  margin-top: 32px;
  font-weight: 500;
  color: #ffffff;
}
.apply .wrap {
  width: 91%;
  box-sizing: border-box;
  margin: 0 auto;
  margin-top: -110px;
  background: #ffffff;
  box-shadow: 0px 4px 16px 8px rgba(0, 0, 0, 0.03);
  padding: 30px 16px;
  border-radius: 4px;
}
.apply .wrap .type {
  font-size: 14px;
  margin-bottom: 12px;
}
.apply .wrap .van-field {
  border-radius: 4px;
  background: #ecf0f3;
  padding: 15px 12px;
  margin-bottom: 12px;
}
.apply .wrap .code {
  color: #1890ff;
}
.apply .wrap .code.disabled {
  color: #b1b1b3;
}
.apply .wrap .button {
  text-align: center;
  border-radius: 4px;
}
</style>
