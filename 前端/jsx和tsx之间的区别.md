# jsx和tsx之间的区别
- 写 **JavaScript** 且用 HTML 语法 → **.jsx**
```jsx
function App() {
  return <div>Hello JSX</div>; // 直接写 HTML
}
```

- 写 **TypeScript** 且用 HTML 语法 → **.tsx**
```tsx
interface Props {
  name: string;
}

function App(props: Props) {
  return <div>Hello {props.name}</div>;
}
```

# 和 Vue 的关系
- Vue3 完全支持 **JSX / TSX**
- 官方推荐：**TSX**（因为 Vue3 用 TypeScript 写的）

写法对比：
```jsx（JS）
export default {
  render() {
    return <div>hello</div>
  }
}
```

```tsx（TS）
import { defineComponent } from 'vue'
export default defineComponent({
  render() {
    return <div>hello</div>
  }
})
```
