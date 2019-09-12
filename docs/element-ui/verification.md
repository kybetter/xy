### verification 短信安全验证组件

#### 概述

verification 短信安全验证组件，用于在查看敏感信息前，需要让用户进行手机短信验证，成功后方可查看。

#### 组件示例

<div style="margin-top: 10px;">
  <ele-xy-verification
    v-model="code"
    telephone="13800000831"
    @sendCode="sendCode"
    :send-status.sync="sendStatus"
    @verifyCode="verifyCode"
  />
</div>

<script>
export default {
  data() {
    return {
      sendStatus: 'init',
      code: '',
    }
  },
  methods: {
    // 发送验证码
    sendCode() {
      setTimeout(() => {
        this.sendStatus = 'sended';
      }, 1000)
    },
    // 校验验证码
    verifyCode(code) {
      // 校验成功后，你可以重置按钮状态
      this.sendStatus = 'init';
      // 清空验证码表单
      this.code = '';
    }
  }
}
</script>

#### 代码示例

```html
<xy-verification
  v-model="code"
  telephone="13800000831"
  @sendCode="sendCode"
  :send-status.sync="sendStatus"
  @verifyCode="verifyCode"
/>
```

```javascript
export default {
  data() {
    return {
      sendStatus: 'init',
      // 用来设置验证码表单值
      code: '',
    }
  },
  methods: {
    // 发送验证码
    sendCode() {
      setTimeout(() => {
        this.sendStatus = 'sended';
      }, 1000)
    },
    // 校验验证码
    verifyCode(code) {
      //   ...
      // 校验成功后，你可以重置按钮状态
      this.sendStatus = 'init';
      // 清空验证码表单
      this.code = '';
    }
  }
}
```

#### API

| 属性 | 类型 | 说明 | 默认值 |
| ------ | :------: | ------ | :------: |
| v-model | String | 验证码表单值，用于设置默认值或清空表单，可选 | 无 |
| telephone | String | 手机号 | 空 |
| sendStatus | String | 用于控制发送验证码按钮状态。'init'： 初始状态；'sending'：发送中状态；'sended'：进入倒计时状态。 | 'init' |
| sendCode | Function | 发送短信的方法 | Function |
| verifyCode | Function | 验证短信验证码的方法 | Function |
