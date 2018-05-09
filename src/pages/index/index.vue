<template>
  <div class="container">

    <div class="addtodo-Navbar">
      My Todos
      <span id="addtodo-icon" @click="TapToAddtodo">+</span>
    </div>

    <div class="taskList-container">
      <div class="tasklist-item" v-for="item in todos" v-bind:key="item.id" v-show="pageState === 'all' ? true : pageState === item.state" @click="TapToTodoDetail(item)">
        <div class="itemtext-container">
          <span class="item-text">{{item.text}}</span>
          <span class="item-time">{{item.createTime}}</span>
        </div>
        <div class="item-icon">
          <img v-bind:src="item.state === 'completed'? iconComplete : iconUnfinished" background-size="cover" />
        </div>
      </div>
    </div>

    <div class="addtodo-footer">
      <div class="footer-icon" @click="footerClickHandle('all')">
        <img v-bind:src="pageState === 'all' ? imgTaskFill : imgTask" background-size="cover" />
        <div class="footer-text">任务</div>
      </div>
      <div class="footer-icon" @click="footerClickHandle('completed')">
        <img v-bind:src="pageState === 'completed' ? imgCompleteFill : imgComplete" background-size="cover" />
        <div class="footer-text">已完成</div>
      </div>
      <div class="footer-icon" @click="footerClickHandle('active')">
        <img v-bind:src="pageState === 'active' ? imgUnfinishedFill : imgUnfinished" background-size="cover" />
        <div class="footer-text">未完成</div>
      </div>
    </div>

  </div>
</template>

<script>
import card from '@/components/card'

export default {
  data () {
    return {
      motto: 'Hello World',
      userInfo: {},
      iconComplete: require('../../../static/icon/complete_icon.png'),
      iconUnfinished: require('../../../static/icon/unfinished_icon.png'),
      imgTask: require('../../../static/icon/task.png'),
      imgTaskFill: require('../../../static/icon/task_fill.png'),
      imgComplete: require('../../../static/icon/complete.png'),
      imgCompleteFill: require('../../../static/icon/complete_fill.png'),
      imgUnfinished: require('../../../static/icon/unfinished.png'),
      imgUnfinishedFill: require('../../../static/icon/unfinished_fill.png'),
      pageState: 'all'
    }
  },

  components: {
    card
  },

  computed: {
    todos: function () {
      var global = getApp()
      return global.todos
    }
  },

  methods: {
    TapToAddtodo () {
      const url = '../addTodo/main'
      wx.navigateTo({ url })
    },

    TapToTodoDetail (item) {
      const url = '../TodoDetail/main?todoObj=' + JSON.stringify(item)
      wx.navigateTo({ url })
    },

    footerClickHandle (state) {
      this.pageState = state
      console.log(this.pageState)
    }
  },

  created () {
    var global = getApp()
    global.todos = [
      {
        id: '1',
        text: '编写todolist小程序',
        state: 'active',
        details: 'do todolist',
        createTime: '2017/12/10 上午10:25:53',
        completedTime: '',
        thought: ''
      },
      {
        id: '2',
        text: '学习小程序',
        state: 'active',
        details: 'own thingsown thingsown thingsown thingsown thingsown thingsown thingsown things',
        createTime: '2017/12/09 下午05:22:33',
        completedTime: '',
        thought: ''
      },
      {
        id: '3',
        text: '煮饭',
        state: 'completed',
        details: 'do todolist',
        createTime: '2017/12/10 上午09:21:08',
        completedTime: '2017/12/11 上午09:50:13',
        thought: 'done well'
      }
    ]
    this.todos = global.todos
  }
}
</script>

<style scoped>
.addtodo-Navbar,
.addtodo-footer {
  width: 100%;
  font-weight: bold;
  padding: 0 20rpx;
  position: fixed;
  box-sizing: border-box;
}

.addtodo-Navbar {
  font-size: 40rpx;
  height: 120rpx;
  line-height: 120rpx;
  background-color: #2c2c2c;
  color: #fff;
  top: 0;
}

#addtodo-icon {
  font-size: 1rem;
  color: #fff;
  float: right;
  right: 0;
}

.taskList-container {
  margin-top: 120rpx;
  width: 100%;
}

.tasklist-item {
  padding: 10rpx 20rpx;
  border-bottom: 3rpx solid #C0C0C0;
}

.itemtext-container {
  margin-top: 20rpx;
}

.item-text {
  font-weight: bold;
}

.item-time {
  color: #C0C0C0;
  font-size: 30rpx;
  float: right;
}

.item-icon {
  padding: 0;
  margin-top: 20rpx;
}

.item-icon img {
  width: 50rpx;
  height: 50rpx;
  margin: 0;
  padding: 0;
}

.addtodo-footer {
  font-size: 23rpx;
  background-color: #eee;
  bottom: 0;
  padding: 10rpx 20rpx;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  box-shadow: 0px 2rpx 15rpx #333;
}

.footer-icon {
  text-align: center;
}

.footer-icon img {
  width: 70rpx;
  height: 70rpx;
  margin: 0;
  padding: 0;
}

.footer-text {
  padding: 0;
  margin: 0;
}

</style>
