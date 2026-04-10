# 1. 渲染管线原理
![[Pasted image 20260409182138.png]]

| 术语                   | 作用                                      |
| -------------------- | --------------------------------------- |
| `Source`（数据源）        | 提供数据（创建或读取）                             |
| `Filters`（过滤器）       | 对数据进行算法处理（剪裁、平移、旋转等）                    |
| `Mapper`（映射器）        | 数据→图元（渲染管线、可视化管线的交汇点）                   |
| `Actor`（实体）          | 场景中的一个物体，绑定`Mapper`和`Property`（形状和外观）   |
| `Renderer`（渲染器）      | 管理`Light`、`Camera`、`Actor`（持有多个`Actor`） |
| `RenderWindow`（渲染窗口） | 连接浏览器`DOM`的容器，如`Canvas`（持有多个`Renderer`） |
| `Interactor` (交互器)   | 监听鼠标、键盘事件，更新相机位置或物体状态                   |

# 2. vtk.js架构

- **Datatypes (数据类型):** 图像数据、几何/非结构化数据
- **Filters (过滤器):** 变换或生成数据
- **Rendering (渲染):** 数据如何被着色、呈现和放置
- **Interaction (交互):** 控制场景视图或与场景中的 Actor（实体）进行交互
- **I/O (输入/输出):** 读取 [[#3. vtk数据文件]] 到 `vtk.js` 
- **Proxy (代理):** 一种抽象机制，用于集中处理典型的管线操作


# 3. vtk数据文件

| 后缀     | 全称                       | 数据类型   | 用途                    |
| ------ | ------------------------ | ------ | --------------------- |
| `.vti` | VTK ImageData XML        | 规则体数据  | 图像、体积、规则网格            |
| `.vtr` | VTK RectilinearGrid XML  | 正交直线网格 | 直角坐标网格                |
| `.vts` | VTK StructuredGrid XML   | 结构化网格  | 结构化网格                 |
| `.vtp` | VTK PolyData XML         | 多边形数据  | 多边形数据（**点、线、面、三角网格**） |
| `.vtu` | VTK UnstructuredGrid XML | 非结构化网格 | 非结构化网格                |

