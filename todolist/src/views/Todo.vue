<template>
    <div class="box">
        <div class="header">
            <h3>TodoList</h3>
            <span @click="reset" title="点击重置Todolist">Reset</span>
        </div>
        <div class="content">
            <div class="content_left content_box">
                <div class="todo titlebox">正在进行<span class="tasknum">{{todolist.length}}</span></div>
                <ul>
                    <li v-for="(item,index) in todolist" :key="index" :item="item" :index="index">
                        <span class="iconfont uncheck" @click="checkboxChange(index)">&#xe8bb;</span>
                        <p>{{item}}</p>
                        <a @click="tododel(index)">-</a>
                    </li>
                </ul>
            </div>
            <div class="content_right content_box">
                <div class="finish titlebox">已经完成<span class="tasknum">{{finishlist.length}}</span></div>
                <ul>
                    <li v-for="(item,index) in finishlist" :key="index" :item="item" :index="index">
                        <span class="iconfont checked" @click="uncheckboxChange(index)">&#xe8ad;</span>
                        <p>{{item}}</p>
                        <a @click="finishdel(index)">-</a>
                    </li>
                </ul>
            </div>
        </div>
        <div class="footer">

        </div>
    </div>
</template>
<script>
export default {
  name: 'Todo',
  data() {
      return {
          todolist: ['6:30 起床', '6:40-7:00 洗漱10分钟，跑步10分钟', '7:10-7:30 吃饭','7:40-8:20 背单词','8:30-11:40 做训练','11:50-12:20 吃饭','12:20-13:00 午睡','13:00-17:00 做练习','17:00-17:30 跑步','17:30-18:00 吃晚饭','18:00-22:00 看书、做练习','22:00-23:00 锻炼、洗漱、洗澡','23:00-23:30 背单词','23:30-6:30 睡觉 (严格执行)'],
          finishlist: [],
          nowDate: 0
      }
  },
  methods: {
      checkboxChange(index) {
          this.finishlist.push(this.todolist[index])
          this.todolist.splice(index,1);
          this.save()
      },
      uncheckboxChange(index) {
          this.todolist.push(this.finishlist[index])
          this.finishlist.splice(index,1);
          this.save()
      },
      tododel(index) {
          this.todolist.splice(index,1);
          this.save()
      },
      finishdel(index) {
          this.finishlist.splice(index,1);
          this.save()
      },
      save() {
          let day = new Date().getDate();
          if(this.nowDate != day){
              this.nowDate = day
              this.todolist = ['6:30 起床', '6:40-7:00 洗漱,跑步', '7:10-7:30 吃饭','7:40-8:20 背单词','8:30-11:40 做训练','11:50-12:20 吃饭','12:20-13:00 午睡','13:00-17:00 做练习','17:00-17:30 跑步','17:30-18:00 吃晚饭','18:00-22:00 看书、做练习','22:00-23:00 锻炼,洗漱,洗澡','23:00-23:30 背单词','23:30-6:30 睡觉']
              this.finishlist = []
          }
          localStorage.setItem('todolist',JSON.stringify(this.todolist))
          localStorage.setItem('finishlist',JSON.stringify(this.finishlist))
          localStorage.setItem('nowDate',JSON.stringify(this.nowDate))
      },
      reset() {
          this.todolist = ['6:30 起床', '6:40-7:00 洗漱,跑步', '7:10-7:30 吃饭','7:40-8:20 背单词','8:30-11:40 做训练','11:50-12:20 吃饭','12:20-13:00 午睡','13:00-17:00 做练习','17:00-17:30 跑步','17:30-18:00 吃晚饭','18:00-22:00 看书、做练习','22:00-23:00 锻炼,洗漱,洗澡','23:00-23:30 背单词','23:30-6:30 睡觉']
          this.finishlist = []
          localStorage.setItem('todolist',JSON.stringify(this.todolist))
          localStorage.setItem('finishlist',JSON.stringify(this.finishlist))
      }
  },
  mounted() {
      if(localStorage.todolist){
          this.todolist = JSON.parse(localStorage.todolist)
      }
      if(localStorage.finishlist){
          this.finishlist = JSON.parse(localStorage.finishlist)
      }
      if(localStorage.nowDate){
          this.nowDate = JSON.parse(localStorage.nowDate)
      }
      this.save()
  }
}
</script>
<style scope>
    .box {
        font-size: 10%;
        display: flex;
        width: 100%;
        margin: 0 auto;
        flex-wrap: wrap;
        user-select: none;
    }
    .box .header {
        width: 100%;
        text-align: center;
    }
    .box .header span {
        position: absolute;
        top: 1%;
        right: 1%;
        color: rgb(68, 163, 187);
        display: block;
        width: 50px;
        height: 50px;
        line-height: 50px;
        text-align: center;
        background-color: yellow;
        border-radius: 10px;
        cursor: pointer;
    }
    .box .header span:hover {
        background-color: tomato;
    }
    .box .content {
        display: flex;
        width: 100%;
        justify-content: space-around;
        flex-wrap: wrap;
    }
    .box .content .content_box {
        width: 60%;
    }
    .box .content .content_box ul li {
        display: flex;
        height: 32px;
        line-height: 32px;
        background: #fff;
        position: relative;
        margin-bottom: 10px;
        padding: 0 45px;
        border-radius: 3px;
        border-left: 5px solid #629A9C;
        box-shadow: 0 1px 2px rgb(0 0 0 / 7%);
        opacity: 0.7;
        justify-content: flex-start;
        align-items: center;
    }
    .box .content .content_box ul li .uncheck {
        position: absolute;
        top: 1px;
        left: 14px;
        width: 22px;
        height: 22px;
        cursor: pointer;
    }
    .box .content .content_box ul li .checked {
        position: absolute;
        top: 1px;
        left: 14px;
        width: 22px;
        height: 22px;
        cursor: pointer;
    }
    .box .content .content_box ul li a {
        position: absolute;
        top: 4px;
        right: 5px;
        display: inline-block;
        width: 14px;
        border-radius: 14px;
        border: 6px double #FFF;
        background: #2cb1e3;
        line-height: 14px;
        text-align: center;
        color: #FFF;
        font-weight: bold;
        font-size: 14px;
        cursor: pointer;
    }
    .box .content .content_box .titlebox {
        position: relative;
        margin-bottom: 10px;
        font-weight: 600;
    }
    .box .content .content_box .tasknum {
        position: absolute;
        top: 2px;
        right: 5px;
        display: inline-block;
        padding: 0 5px;
        height: 20px;
        border-radius: 20px;
        background: #E6E6FA;
        line-height: 22px;
        text-align: center;
        color: #666;
        font-size: 14px;
    }
</style>