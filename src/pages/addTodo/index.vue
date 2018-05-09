<template>
  <div class="container">

    <div class="addtodo-Navbar">
      新建任务
    </div>

    <div class="taskForm-container">
      <div class="taskForm-name">
        <span class="input-label">任务名称：</span>
        <input type="text" v-model="name">
      </div>
      <div class="taskForm-describe">
        <span class="input-label">任务描述：</span>
        <textarea name="describe" v-model="describe" id="123" rows="5" class="describe-text"></textarea>
      </div>
      <button @click="Addtodo">提交</button>
    </div>

  </div>
</template>

<script>

export default {
  data () {
    return {
      name: '',
      describe: ''
    }
  },

  methods: {
    Addtodo () {
      // 添加item
      var global = getApp()
      var tempTime = new Date()
      var timeId = tempTime.getTime()
      var formatTime = tempTime.toLocaleString()
      var tempItem = {
        id: timeId,
        text: this.name,
        state: 'active',
        details: this.describe,
        createTime: formatTime,
        completedTime: '',
        thought: ''
      }
      global.todos.push(tempItem)
      this.name = ''
      this.describe = ''
      const url = '../index/main'
      wx.navigateTo({ url })
    }
  },

  created () {
    // 调用应用实例的方法获取全局数据
    // this.getUserInfo()
  }
}
</script>

<style scoped>
.addtodo-Navbar {
  width: 100%;
  font-weight: bold;
  padding: 0 20rpx;
  position: fixed;
  box-sizing: border-box;
  text-align: center;
  font-size: 40rpx;
  height: 120rpx;
  line-height: 120rpx;
  background-color: #2c2c2c;
  color: #fff;
  top: 0;
}

.taskForm-container {
  margin-top: 120rpx;
  width: 100%;
  padding: 20rpx;
  padding-top: 30rpx;
  box-sizing: border-box;
}

/* .taskForm-name {
  border: 1px solid red;
} */

.input-label {
  font-weight: bold;
  font-size: 35rpx;
}

.taskForm-describe {
  margin-top: 50rpx;
  /* border: 1px solid green; */
}

input,
textarea {
  border: 3rpx solid #888;
  border-radius: 10rpx;
  margin: 15rpx 0;
}

input {
  padding: 10rpx;
}

.describe-text {
  width: 100%;
  box-sizing: border-box;
}

button {
  margin-top: 40rpx;
  background-color: #E0E0E0;
}

</style>
