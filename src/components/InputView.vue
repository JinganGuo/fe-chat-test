<template>
  <div class="input-view">
    <input v-model="value" type="text" @keyup.enter="sendMessage" placeholder="Please input...">
    <button @click.enter="sendMessage">Send</button>
    <button class="clean" @click="cleanMessage">Clean</button>
  </div>
</template>

<script>
export default {
  name: 'InputView',
  data() {
    return {
      value: ''
    }
  },
  methods: {
    sendMessage() {
      this.$emit('handleBtn', this.value);
      this.value = '';
    },
    cleanMessage() {
      this.$emit('handleClean');
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
  .clean {
    font-size: 14px;
    background: lightgray;
  }
}
</style>


