### countdown 倒计时按钮

#### 概述

countdown 倒计时按钮组件用于提供一个可点击后进入倒计时状态的按钮，免去自己编写倒计时逻辑和样式。

#### 组件示例

<ele-xy-countdown-button style="margin-top:20px;" @click="sendCode" :send-status.sync="sendStatus"></ele-xy-countdown-button>

<script>
export default {
  data() {
    return {
      // 验证码发送状态，默认是 init，初始状态
      sendStatus: 'init',
    }
  },
  methods: {
    sendCode(val) {
      setTimeout(() => {
        let noError = true
        if (noError) {
          this.sendStatus = 'sended';
        } else {
          this.sendStatus = 'init';
        }
      }, 1000)
    }
  }
}
</script>

#### 代码示例

```html
<xy-countdown-button @click="sendCode" :send-status.sync="sendStatus" />
```

```javascript
export default {
  data() {
    return {
      // 验证码发送状态，默认是 init，初始状态
      sendStatus: 'init',
    }
  },
  methods: {
    sendCode(val) {
      // 模拟接口请求
      setTimeout(() => {
        if (hasNoError) {
          // 把状态设为 'sended'，按钮就会进入倒计时状态
          this.sendStatus = 'sended';
        } else {
          // 如果有错误，把状态设为 'init' 就可以恢复按钮状态
          this.sendStatus = 'init';
        }
      }, 1000)
    }
  }
}
```

#### API

| 属性 | 类型 | 说明 | 默认值 |
| ------| ------ | ------ | :------: |
| sendStatus | String | 用于控制按钮状态。'init'： 初始状态；'sending'：发送中状态；'sended'：进入倒计时状态。| 'init' |
| click | Function | 按钮点击后触发的事件，你可以在这个事件中改变按钮状态 | Function |
| text | String | 设置按钮默认文字 | '获取验证码' |
