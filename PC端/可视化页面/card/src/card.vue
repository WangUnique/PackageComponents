<template>
  <el-card class="box-card">
    <!-- 除非想添加额外的需求，否则不需要通过具名插槽改变其他内容 -->
    <template #header>
      <div class="card-header">
        <!-- 通过props由父组件传递过来的title -->
        <span>{{ title }}</span>
      </div>
    </template>
    <div class="item">
      <!-- 默认的default插槽会被父组件中插入的组件替换 -->
      <slot></slot>
    </div>
  </el-card>
</template>

<script lang="ts" setup>
import { defineProps, withDefaults } from 'vue'

withDefaults(
  defineProps<{
    title: string
  }>(),
  {
    title: 'Title'
  }
)
</script>

<style lang="less" scoped>
.box-card {
  // & less中表示当前选择器的父级
  // scoped编译会在元素上添加 data-v-xxxxxxx 字样hash
  // :deep 深度选择器，为了使父组件的hash影响到子组件
  // template模板会渲染成class为 el-card__header 的div
  &:deep(.el-card__header) {
    padding: 10px 20px !important;
  }
}
// 设置title文字的样式
.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 30px;
}
// 可视化化图表的下外边距
.item {
  margin-bottom: 10px;
}
</style>
