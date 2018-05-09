<template>
  <div class="container">

    <div class="taskDetail-Navbar">
      任务详情
    </div>

    <div class="taskDetail-container">
      <div class="each-main-container">
        <div class="item-text">{{item.text}}</div>
        <div class="item-time">{{item.createTime}}</div>
      </div>
      <div class="each-container">
        <span class="detail-label">任务描述：</span>
        <span>{{item.details}}</span>
      </div>
      <div class="each-container">
        <span class="detail-label">状态：</span>
        <img v-bind:src="item.state === 'completed'? iconComplete : iconUnfinished" background-size="cover" />
      </div>
      <div class="each-container">
        <span class="detail-label">想法：</span>
        <span v-if="item.state === 'completed'">{{item.thought}}</span>
        <textarea v-if="item.state === 'active'" v-model="thought" id="123" rows="5" class="thought-text"></textarea>
      </div>
      <div class="each-container" v-if="item.state === 'completed'">
        <span class="detail-label">完成时间：</span>
        <span>{{item.completedTime}}</span>
      </div>
      <div class="button-container">
        <button @click="done(item)" v-if="item.state === 'active'" class="green-button">完成</button>
        <button @click="undo(item)" v-if="item.state === 'completed'" class="green-button">撤销</button>
        <button @click="deleteTask(item)" class="red-button">删除</button>
      </div>
    </div>

  </div>
</template>

<script>

export default {
  data () {
    return {
      iconComplete: require('../../../static/icon/complete_icon.png'),
      iconUnfinished: require('../../../static/icon/unfinished_icon.png'),
      thought: '',
      item: {
        id: '3',
        text: '煮饭',
        state: 'completed',
        details: 'do todolist',
        createTime: '2017/12/10 上午09:21:08',
        completedTime: '2017/12/11 上午09:50:13',
        thought: 'done well'
      }
    }
  },

  methods: {
    done (item) {
      // 完成任务
      var global = getApp()
      var formatTime = new Date().toLocaleString()
      console.log(item.id)
      global.todos.forEach((todo) => {
        console.log(todo.id)
        if (todo.id === item.id) {
          todo.state = 'completed'
          todo.thought = this.thought
          todo.completedTime = formatTime
        }
      })
      console.log(global.todos)
      this.thought = ''
      const url = '../index/main'
      wx.navigateTo({ url })
    },

    undo (item) {
      // 撤销任务
      var global = getApp()
      global.todos.forEach((todo) => {
        if (todo.id === item.id) {
          todo.state = 'active'
          todo.thought = ''
          todo.completedTime = ''
        }
      })
      const url = '../index/main'
      wx.navigateTo({ url })
    },

    deleteTask (item) {
      // 删除任务
      var global = getApp()
      var deleteIndex
      global.todos.forEach((todo, index) => {
        if (todo.id === item.id) {
          deleteIndex = index
        }
      })
      global.todos.splice(deleteIndex, 1)
      console.log('global.todos', global.todos)
      const url = '../index/main'
      wx.navigateTo({ url })
    }
  },

  onLoad (options) {
    this.item = JSON.parse(options.todoObj)
  }
}
</script>

<style scoped>
.taskDetail-Navbar {
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

.taskDetail-container {
  margin-top: 130rpx;
  width: 100%;
  padding: 20rpx;
  box-sizing: border-box;
}

.each-main-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-bottom: 20rpx;
  border-bottom: 3rpx solid #888;
}

.item-text {
  font-weight: bold;
  font-size: 50rpx;
}

.item-time {
  color: #C0C0C0;
  font-size: 30rpx;
}

.each-container {
  margin: 40rpx 0;
}

.detail-label {
  font-weight: bold;
  vertical-align: bottom;
}

img {
  width: 50rpx;
  height: 50rpx;
  margin: 0;
  padding: 0;
  vertical-align: bottom;
}

textarea {
  border: 3rpx solid #888;
  border-radius: 10rpx;
  margin: 15rpx 0;
  width: 100%;
  box-sizing: border-box;
}

.button-container {
  display: flex;
  justify-content: space-evenly;
}

button {
  color: #fff;
  width: 150rpx;
}

.green-button {
  background-color: #096;
}

.red-button {
  background-color: #d81e06;
}
</style>
