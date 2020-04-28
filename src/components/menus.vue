<!--
 * @Author: Bill Lee
 * @Date: 2020-04-13 23:03:44
 * @LastEditors: Bill Lee
 * @LastEditTime: 2020-04-18 16:26:36
 * @Description:
 -->

<template>
    <div class="list-todos"> <!--菜单容器-->
        <a class="list-todo activeListClass list"  v-for="item in items" :key="item.title"> <!--单个菜单容器-->
            <span class="icon-lock" v-if="item.locked"></span> <!--锁的图标-->
            <span class="count-list" v-if="item.count>0">
                {{item.count}}
            </span> <!--数字-->
            {{item.title}} <!--菜单内容-->
        </a>
        <a class="link-list-new"> <!--新增菜单-->
            <span class="icon-plus"></span>
            新增
        </a>
    </div>
</template>

<script>
import {getTodoList, addTodo} from '../api/api'// 引入封装好的两个接口函数
export default {
  data () {
    return {
      items: [], // 菜单数据
      todoId: '' // 默认选中id
    }
  },
  created () {
    getTodoList({}).then(res => {
      const TODOS = res.data.todos // 数据都会返回在res.data里面。
      this.items = TODOS // 我的把菜单数据赋值给定义的this.items
      this.todoId = TODOS[0].id // 把菜单数据的默认的第一个对象的id赋值给默认选中的id
    })
  },
  methods: {
    goList (id) { // 点击菜单的时候，替换选中的id
      this.todoId = id
    },
    addTodoList () { // 点击新增按钮
      // 调用新增菜单接口，在接口调用成功再请求数据
      addTodo({}).then(data => {
        getTodoList({}).then(res => {
          const TODOS = res.data.todos
          this.todoId = TODOS[TODOS.length - 1].id
          this.items = TODOS
        })
      })
    }
  },
  watch: {
    'todoId' (id) {
      this.$route.push({name: 'todo', params: {id: id}})
      // 监听到用户的点击todoId的变化再跳转路由
    }
  }
}
</script>

<style lang="less">
@import '../common/style/menu.less';
</style>
