# 组件间传数据

- **props：父 → 子**
- **emit：子 → 父**
props 和 emit 都是在【子组件】里声明、定义的，父组件只是 “传值 / 监听”

# `<script>` + export default 和 `<script setup>` 区别

```js
<script>
import { ref } from 'vue'
export default {
  name: 'VtkToolbar',
  props: { ... },
  emits: [ ... ],
  setup(props, { emit }) {
    const a = ref(1)
    function fn() {}
    return { a, fn } // 必须 return 才能模板用
  }
}
</script>
```

```js
<script>
import { ref } from 'vue'
export default {
  name: 'VtkToolbar',
  props: { ... },
  emits: [ ... ],
  setup(props, { emit }) {
    const a = ref(1)
    function fn() {}
    return { a, fn } // 必须 return 才能模板用
  }
}
</script>
```

| 功能                   | `<script>` 普通版 | `<script setup>` 语法糖 |
| -------------------- | -------------- | -------------------- |
| 是否要 `setup()`        | ✅ 必须写          | ❌ 不用写                |
| 是否要 `return`         | ✅ 必须           | ❌ 自动暴露               |
| 是否要 `export default` | ✅ 必须           | ❌ 不用                 |
| 接收 props             | `setup(props)` | `defineProps()`      |
| 触发 emit              | `{ emit }`     | `defineEmits()`      |
| 代码量                  | 多              | 少                    |
| this                 | 无              | 无                    |
| 官方推荐                 | 否（vue2老项目迁移用）  | ✅ 是（vue3推荐）          |

# 双击 index.html 打开vue 项目（Webpack 版）
## 1. 核心原理
`publicPath: './'`，本质就是把打包后所有 JS、CSS、图片的引用路径，从「绝对路径」改成「相对路径」。
- **绝对路径 (`/`)**：从根目录开始找
- **相对路径 (`./`)**：从当前目录（ `index.html` 所在文件夹）开始找

## 2. 解决步骤
1. 打开项目根目录的 **`vue.config.js`**。
2. 在导出的配置对象中，添加一行：
    ```js
    module.exports = {
      // 👇 关键配置：使用相对路径
      publicPath: './', 
      
      // 其他原有配置...
    }
    ```
3. 重新打包：在终端运行 `npm run build`。
4. 去 `dist` 文件夹，**直接双击 index.html** 。