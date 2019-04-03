<template>
  <div id="app">
    <header-view class="header"></header-view>
    <main-view :messageList="messageList"></main-view>
    <input-view class="footer" @handleBtn="handleBtn" @handleClean="handleClean"></input-view>
  </div>
</template>

<script>
import HeaderView from "./components/HeaderView";
import MainView from "./components/MainView";
import InputView from "./components/InputView";

import testData from "./fe-chat-test.json";

export default {
  name: "app",
  components: {
    MainView,
    HeaderView,
    InputView
  },
  data() {
    return {
      messageList: []
    };
  },
  methods: {
    /**
     * 处理发送消息按钮
     */
    handleBtn(value) {
      const data = new Date().getTime() / 1000;

      const newMessage = {
        avatar: "http://pnzhqn5pf.bkt.clouddn.com/%E8%AF%81%E4%BB%B6%E7%85%A7.jpg",
        name: "Me",
        text: value,
        time: data
      };

      window.scrollTo({
        top: document.body.scrollHeight,
        behavior: "smooth"
      });

      this.messageList.push(newMessage);
    },
    /**
     * 处理清除消息按钮
     */
    handleClean() {
      const isDelete = confirm('Are u sure clean messages?');
      if (isDelete) {
        this.messageList = [];
      }
    }
  },
  created() {
    this.messageList = Object.values(testData);
  }
};
</script>

<style lang="scss" scoped>
* {
  padding: 0;
  margin: 0;
}
#app {
  overflow-y: scroll;
  .header {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
  }
  .footer {
    position: fixed;
    bottom: 0;
    left: 0;
    margin-top: 30px;
  }
}
</style>
