<template>
  <button
    class="xy-button xy-custom-button"
    :class="{ disabled: isDisable }"
    @click="onClick"
    :disabled="isDisable"
  >
    <span>{{ btnText }}</span>
  </button>
</template>

<script>
const countSecond = 60;

export default {
  name: 'XyCountdownButton',
  props: {
    text: {
      type: String,
      default: '获取验证码',
    },
    // 'init'： 初始状态；
    // 'sending'：发送中状态；
    // 'sended'：进入倒计时状态；
    sendStatus: {
      type: String,
      default: 'init',
    },
  },
  data() {
    return {
      timer: null,
      btnText: this.text,
      isDisable: false,
      countdown: countSecond,
      innerStatus: this.sendStatus,
    };
  },
  watch: {
    sendStatus(status) {
      this.innerStatus = status;
    },
    innerStatus(status) {
      if (status === 'sended') {
        this.setTimer();
      }
      if (status === 'init') {
        this.resetTimer();
      }
    },
  },
  methods: {
    onClick() {
      if (this.isDisable) return;
      this.btnText = '发送中';
      this.$emit('update:sendStatus', 'sending');
      this.innerStatus = 'sending';
      this.$emit('click', 'sending');
      this.isDisable = true;
    },

    setTimer() {
      clearInterval(this.timer);
      this.btnText = `${this.countdown}S后重新获取`;
      this.timer = setInterval(() => {
        if (this.countdown <= 1) {
          this.btnText = this.text;
          clearInterval(this.timer);
          this.$emit('update:sendStatus', 'init');
          this.isDisable = false;
        } else {
          this.btnText = `${(this.countdown -= 1)}S后重新获取`;
        }
      }, 1000);
    },

    resetTimer() {
      clearInterval(this.timer);
      this.countdown = countSecond;
      this.btnText = this.text;
      this.isDisable = false;
    },
  },
};
</script>
<style scoped lang="less">
button {
  text-transform: none;
  overflow: visible;
  font-family: inherit;
}

.xy-button {
  display: inline-block;
  line-height: 1;
  white-space: nowrap;
  cursor: pointer;
  background: #fff;
  border: 1px solid #dcdfe6;
  color: #606266;
  -webkit-appearance: none;
  text-align: center;
  box-sizing: border-box;
  outline: 0;
  margin: 0;
  transition: 0.1s;
  font-weight: 500;
  padding: 12px 20px;
  font-size: 14px;
  border-radius: 4px;
  user-select: none;
}

.xy-button:hover,
.xy-button:focus {
  color: #409eff;
  border-color: #c6e2ff;
  background-color: #ecf5ff;
}

.xy-button:active {
  color: #3a8ee6;
  border-color: #3a8ee6;
  outline: 0;
}

.xy-button.primary {
  background-color: #409eff;
  border-color: #409eff;
  color: #fff;
}

.xy-button.primary:active {
  background: #3a8ee6;
  border-color: #3a8ee6;
  outline: 0;
}

.xy-button.disabled {
  //color: rgba(0, 0, 0, 0.25);
  //background-color: #f5f5f5;
  //border-color: #d9d9d9;
  text-shadow: none;
  box-shadow: none;
  cursor: not-allowed;
}

.xy-custom-button {
  border: 1px solid #20a0ff;
  color: #20a0ff;
}
</style>
