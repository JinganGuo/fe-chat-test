<template>
  <div class="input-view">
    <input v-model="value" type="text" @keyup.enter="sendMessage" placeholder="Please input...">
    <button :class="{disabled: disable}" @click.enter="sendMessage">Send</button>
    <button class="clean" @click="cleanMessage">Clean</button>
  </div>
</template>

<script>
export default {
  name: 'InputView',
  data() {
    return {
      value: '',
      disable: true
    }
  },
  methods: {
    sendMessage() {
      if (this.disable) {
        return;
      }
      this.$emit('handleBtn', this.value);
      this.value = '';
    },
    cleanMessage() {
      this.$emit('handleClean');
    }
  },
  watch: {
    value: function(val) {
      this.disable = val.length ? false : true;
    }
  }
}
</script>

<style lang="scss" scoped>
.input-view {
  display: flex;
  width: 100%;
  height: 40px;
  input {
    padding: 10px 5px;
    display: block;
    border: 2px solid #059fd3;
    width: 100%;
  }
  button {
    width: 100px;
    background: #059fd3;
    
    font-size: 16px;
    color: #ffffff;
  }
  .disabled {
    background: gray;
  }
  .abled {
    background: #059fd3;
  }
  .clean {
    font-size: 14px;
    background: lightgray;
  }
}
</style>


