<!--
 * @Author: Bill Lee
 * @Date: 2020-04-14 20:40:52
 * @LastEditors: Bill Lee
 * @LastEditTime: 2020-04-18 16:15:41
 * @Description:
 -->

<template>
    <div class="list-item editingClass editing"><!-- 最外层容器-->
        <label class="checkbox"><!--自定义的多选框-->
            <input type="checkbox" v-model="item.checked"><!--item.checked-->
            <span class="checkbox-custom"></span>
        </label>
        <input type="text" v-model="item.text" placeholder="写点什么..."><!--绑定item.text-->
        <a class="delete-item"><!--删除图标-->
            <span class="icon-trash"></span>
        </a>
    </div>
</template>

<script>
export default {
// item 是todo的子组件,他接受一个对象item,来进行处理
  props: {
    item: {
      type: Object,
      default: () => {
        return {
          checked: false,
          text: '你好，世界'
        }
      }
    }
  }
}
</script>

<style lang="less">
@import '../common/style/list-items.less';
</style>
