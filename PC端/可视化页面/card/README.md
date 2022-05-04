## 封装可视化页面的载体 Card

### 使用效果展示![image-20220504195054471](https://github.com/WangUnique/PackageComponents/blob/master/PC%E7%AB%AF/%E5%8F%AF%E8%A7%86%E5%8C%96%E9%A1%B5%E9%9D%A2/assets/img/cart.png)

### template 代码展示

```vue
<template>
  <el-card class="box-card">
    <!-- 除非想添加额外的需求，非必要不通过具名插槽改变其他内容 -->
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
```

### setup 代码展示

```vue
<script lang="ts" setup>
import { defineProps, withDefaults } from "vue";
withDefaults(
  defineProps<{
    // 泛型的基本使用方法 对应props应为 {title: '...'}
    title: string;
  }>(),
  {
    title: "Title", // 默认值
  }
);
</script>
```

### css 代码展示

```css
<style lang="less" scoped>
/*
   & less中表示当前选择器的父级
   scoped编译会在元素上添加 data-v-xxxxxxx 字样hash
   :deep 深度选择器，为了使父组件的hash影响到子组件
   template模板会渲染成class为 el-card__header 的div
*/
.box-card {
  &:deep(.el-card__header) {
    padding: 10px 20px !important;
  }
}

/* 设置title文字的样式 */
.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 30px;
}

/* 可视化化图表的下外边距 */
.item {
  margin-bottom: 10px;
}
</style>
```

### 推荐文件放置路径

> src > base-ui > card

- `src:` vue/cli 的根目录
- `base-ui:` 通常用来放置多个项目都可以使用的模块，具有很强的通用性
- `card:` 见名知意的 filename 容易分辨
  - card 文件夹内部可以创建一个 `index.ts` 作为整个模块的出入口
  - 可以创建一个`src`目录放置`模块.vue`文件

### 使用方法

```html
<!-- :gutter   栅格间隔 -->
<el-row :gutter="10">
  <el-col :span="7">
    <wk-card title="title文字[0]"> </wk-card>
  </el-col>
  <el-col :span="10">
    <wk-card title="title文字[1]"> </wk-card>
  </el-col>
  <el-col :span="7">
    <wk-card title="title文字[2]"> </wk-card>
  </el-col>
</el-row>
<el-row :gutter="10">
  <el-col :span="12">
    <wk-card title="title文字[3]"> </wk-card>
  </el-col>
  <el-col :span="12">
    <wk-card title="title文字[4]"> </wk-card>
  </el-col>
</el-row>
```

### 时间及版本

> ​ 创建时间

- `2022年5月4日 四月初四 星期三`

> ​ 对应库/框架版本:

- `"vue": "^3.2.13"`
- `"element-plus": "^2.1.7"`
- `"typescript": "~4.5.5"`
- `"less": "^4.0.0"`
- `"less-loader": "^8.0.0"`
