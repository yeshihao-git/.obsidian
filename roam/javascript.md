#js
# JavaScript 是单线程的
`JavaScript` 本身是单线程，但运行环境是多线程。  

`JavaScript` 本身只有一个主线程， **但浏览器 / Node 不是单线程**（定时器、网络请求、`IO`、渲染、`Worker` 都是别的线程）它们干完活，把**结果丢到任务队列**，等主线程空了，再回来执行回调。

# JSX 和 TSX 之间的区别
- 写 `JavaScript` 且用 `HTML` 语法 → `.jsx`
```jsx
function App() {
  return <div>Hello JSX</div>; // 直接写 HTML
}
```

- 写 `TypeScript` 且用 `HTML` 语法 → `.tsx`
```tsx
interface Props {
  name: string;
}

function App(props: Props) {
  return <div>Hello {props.name}</div>;
}
```

- `vue3` 完全支持 `JSX / TSX`

# 开发、打包、部署、发布
1. **开发**：编写源代码

2. **打包（build / package）**： 源代码 → 浏览器能直接运行的代码，放入`dist` 文件夹
> **示例**：`.vue`、`.tsx`、`scss` 打包后变成 `js`/`css`/`html`   
> **打包工具**：vite、webpack、parcel 
> **树摇**：打包时自动把没用到的代码 “摇” 掉，只保留实际运行需要的代码

3. **部署（deploy）**： `dist` 文件夹 → 放到服务器上
> **示例**： 将打包产物放到阿里云/腾讯云服务器、GitHub Pages、Vercel 等平台

4. **发布（publish / release）**： 对外发布新版本