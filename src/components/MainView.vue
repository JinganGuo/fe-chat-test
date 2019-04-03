<template>
  <div id="main" class="main-view">
    <div class="info" v-for="(item, index) of messageList" :key="index">

      <p class="time" v-if="isShowTime(index)">{{ getLocalTime(item.time) }}</p>

      <div :class="[item.name === 'Me' ? 'right-side' : 'left-side']">
        <div v-if="isShowAvatar(index)" class="user">
          <img :src="item.avatar" alt>
          <span>{{ item.name }}</span>
        </div>
        <p class="message">{{ item.text }}</p>
      </div>

    </div>
  </div>
</template>

<script>
export default {
  name: "MainView",
  props: {
    messageList: Array
  },
  methods: {
    /**
     * 时间戳转换成标准时间格式
     */
    getLocalTime(timestamp) {
      var date = new Date(parseInt(timestamp * 1000));
      var Y = date.getFullYear() + "-";
      var M =
        (date.getMonth() + 1 < 10
          ? "0" + (date.getMonth() + 1)
          : date.getMonth() + 1) + "-";
      var D = date.getDate() + " ";
      var h =
        (date.getHours() >= 10 ? date.getHours() : "0" + date.getHours()) + ":";
      var m =
        (date.getMinutes() >= 10
          ? date.getMinutes()
          : "0" + date.getMinutes()) + ":";
      var s =
        date.getSeconds() >= 10 ? date.getSeconds() : "0" + date.getSeconds();
      return Y + M + D + h + m + s;
    },
    /**
     * 判断是否需要展示用户头像
     */
    isShowAvatar(index) {
      const currentUser = this.messageList[index].name;
      const last = this.messageList[index - 1];
      const lastUser = last && last.name;

      return currentUser !== lastUser;
    },
    /**
     * 判断是否需要展示时间
     */
    isShowTime(index) {
      const currentTime = this.messageList[index].time;
      const last = this.messageList[index - 1];
      const lastTime = last && last.time;
      
      const gap = currentTime - lastTime; 

      if (gap >= 300 || isNaN(gap)) {
        return true;
      }
      return false;
    }
  },
  mounted() {
    const mainDOM = document.getElementById("main");
    mainDOM.scrollTop = mainDOM.scrollHeight;
  }
};
</script>

<style lang="scss" scoped>
.main-view {
  flex: 1;
  overflow-y: scroll;
  .info {
    box-sizing: border-box;
    .time {
      text-align: center;
      font-size: 12px;
      color: grey;
    }
    .user {
      margin-bottom: 5px;
    }
    .left-side {
      text-align: left;
      img {
        float: left;
      }
      p {
        margin-left: 40px;
      }
    }
    .right-side {
      text-align: right;
      img {
        float: right;
      }
      p {
        margin-right: 40px;
      }
    }
    img {
      width: 30px;
      margin-right: 10px;
    }
    span {
      line-height: 30px;
      font-weight: bold;
    }
    .message {
      display: inline-block;
      border: 1px solid lightblue;
      padding: 5px 10px;
      border-radius: 5px;
      margin-bottom: 5px;
    }
  }
}
</style>


