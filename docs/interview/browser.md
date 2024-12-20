---
outline: deep
---
## V8引擎的原理

:::details
V8引擎是Google开发的开源JavaScript引擎，主要用于Chrome浏览器和Node.js。它通过将JavaScript代码编译为机器码来提高执行速度，并使用即时编译（JIT）技术来优化性能。

- V8引擎将JavaScript代码转换为机器码，以便更快地执行。
- 它使用了多种优化技术，如内联缓存和逃逸分析，以提高性能。
- V8还支持垃圾回收机制，自动管理内存，减少内存泄露的风险。

:::

## 也没有了解过热点代码

:::details
热点代码是指在程序执行过程中频繁被调用的代码段。V8引擎会优先优化这些代码，以提高整体性能。

- 热点代码通常是性能瓶颈，优化这些代码可以显著提高应用的响应速度。
- V8引擎会监测代码的执行频率，并对热点代码进行优化处理。
- 通过即时编译，V8能够在运行时对热点代码进行优化，提升执行效率。

:::

## WebKit、JSCore 与渲染引擎原理

::: details

- WebKit
  - **定义**: WebKit 是一个开源的网页浏览器引擎，最初由苹果公司开发，广泛用于 Safari 浏览器和 iOS 的 WebView 组件。
  - **组成**: WebKit 包含多个组件，其中最重要的是渲染引擎（负责将 HTML、CSS 和 JavaScript 转换为可视化的网页）和 JavaScript 引擎（负责执行 JavaScript 代码）。
  - **功能**:
    - 解析 HTML 和 CSS，构建 DOM（文档对象模型）和 CSSOM（CSS 对象模型）。
    - 处理 JavaScript 代码的执行，更新 DOM 和 CSSOM。
    - 渲染页面并处理用户交互。

- JSCore
  - **定义**: JSCore 是 WebKit 中的 JavaScript 引擎，负责执行 JavaScript 代码。
  - **功能**:
    - 解析和编译 JavaScript 代码，将其转换为可执行的机器代码。
    - 提供执行上下文，管理变量作用域和闭包。
    - 处理事件循环和异步操作，确保 JavaScript 代码的非阻塞执行。
  - **优化**: JSCore 采用了多种优化技术，如即时编译（JIT）和垃圾回收，以提高执行效率和内存管理。

- 渲染引擎原理
  - **工作流程**:
    1. **解析**: 渲染引擎首先解析 HTML 文档，构建 DOM 树。然后解析 CSS，构建 CSSOM。
    2. **渲染树**: 将 DOM 和 CSSOM 合并，生成渲染树，表示页面的可视化结构。
    3. **布局**: 计算每个节点的几何信息（位置和大小），确定如何在屏幕上呈现。
    4. **绘制**: 将渲染树中的节点绘制到屏幕上，生成最终的视觉效果。
    5. **重绘和重排**: 当 DOM 或 CSSOM 发生变化时，渲染引擎会进行重绘（更新视觉效果）和重排（重新计算布局）。

- WebKit 是一个综合性的浏览器引擎，包含 JSCore 作为其 JavaScript 执行引擎。渲染引擎负责将网页内容解析、布局和绘制到屏幕上。理解这些组件的工作原理有助于开发高效的 Web 应用和优化用户体验。
:::

## 用户从输入 URL 到页面加载完毕都经历了哪些步骤？

::: details
用户从输入 URL 到页面加载完毕的过程涉及多个步骤，主要包括以下几个阶段：

1. **URL 输入**:
   - 用户在浏览器的地址栏中输入 URL，并按下回车键。

2. **DNS 解析**:
   - 浏览器向 DNS（域名系统）服务器发送请求，将域名解析为对应的 IP 地址。这个过程可能涉及多个 DNS 服务器的查询。

3. **建立 TCP 连接**:
   - 一旦获得 IP 地址，浏览器与目标服务器建立 TCP 连接。对于 HTTPS 请求，还会进行 TLS 握手以建立安全连接。

4. **发送 HTTP 请求**:
   - TCP 连接建立后，浏览器向服务器发送 HTTP 请求，请求特定的资源（如 HTML 页面、图片、CSS 文件等）。

5. **服务器处理请求**:
   - 服务器接收到请求后，处理请求并生成响应。这个过程可能涉及数据库查询、业务逻辑处理等。

6. **返回 HTTP 响应**:
   - 服务器将处理结果（如 HTML 文档）作为 HTTP 响应返回给浏览器。

7. **浏览器接收响应**:
   - 浏览器接收到服务器的响应后，开始解析和处理响应内容。

8. **解析 HTML**:
   - 浏览器解析 HTML 文档，构建 DOM（文档对象模型）树。

9. **解析 CSS**:
   - 浏览器解析 CSS 文件，构建 CSSOM（CSS 对象模型）树。

10. **构建渲染树**:
    - 将 DOM 和 CSSOM 合并，生成渲染树，表示页面的可视化结构。

11. **布局计算**:
    - 计算每个节点的几何信息（位置和大小），确定如何在屏幕上呈现。

12. **绘制**:
    - 将渲染树中的节点绘制到屏幕上，生成最终的视觉效果。

13. **执行 JavaScript**:
    - 如果页面中包含 JavaScript，浏览器会执行这些脚本，可能会修改 DOM 或 CSSOM，导致重绘或重排。

14. **页面加载完毕**:
    - 当所有资源（如图片、样式表、脚本等）都加载完成，浏览器会触发 `load` 事件，表示页面加载完毕。

- 用户从输入 URL 到页面加载完毕的过程涉及 DNS 解析、TCP 连接建立、HTTP 请求和响应、HTML 和 CSS 解析、渲染树构建、布局计算、绘制以及 JavaScript 执行等多个步骤。
:::

## 浏览器渲染页面 Layout 分为几层，各个特点是什么？

::: details
浏览器渲染页面的过程通常可以分为以下几个主要层次，每一层都有其独特的特点和功能：

1. **HTML 解析层**:
   - **特点**:
     - 浏览器首先解析 HTML 文档，构建 DOM（文档对象模型）树。
     - DOM 树是一个表示文档结构的树形结构，节点对应于 HTML 元素。
     - 解析过程中，浏览器会处理标签、属性和文本内容。

2. **CSS 解析层**:
   - **特点**:
     - 浏览器解析 CSS 文件，构建 CSSOM（CSS 对象模型）树。
     - CSSOM 树表示样式信息，节点对应于 CSS 规则。
     - 解析过程中，浏览器会处理选择器、属性和样式值。

3. **渲染树构建层**:
   - **特点**:
     - 将 DOM 树和 CSSOM 树合并，生成渲染树。
     - 渲染树只包含可见的元素，排除那些 `display: none` 的元素。
     - 每个节点包含了元素的样式信息，准备进行布局计算。

4. **布局层 (Layout)**:
   - **特点**:
     - 计算每个节点的几何信息（位置和大小），确定如何在屏幕上呈现。
     - 这个过程也称为“重排”（Reflow），涉及到元素的尺寸、位置和相对关系。
     - 布局计算是一个重要的性能开销，尤其是在页面结构复杂时。

5. **绘制层 (Painting)**:
   - **特点**:
     - 将渲染树中的节点绘制到屏幕上，生成最终的视觉效果。
     - 这个过程涉及到颜色、文本、图像等的绘制。
     - 绘制操作通常是分层进行的，浏览器会将不同的层合成最终的图像。

6. **合成层 (Compositing)**:
   - **特点**:
     - 在现代浏览器中，绘制的内容可能会被分成多个层（如动画、视频等）。
     - 合成层负责将这些层合并成最终的图像，提升性能和流畅度。
     - 合成可以在 GPU 上进行，减少 CPU 的负担，提高渲染效率。

- 浏览器渲染页面的过程分为多个层次，包括 HTML 解析层、CSS 解析层、渲染树构建层、布局层、绘制层和合成层。每一层都有其独特的功能和特点，理解这些层次有助于优化网页性能和用户体验。
:::

## 页面布局中哪些操作会脱离文档流？

::: details
在网页布局中，某些 CSS 属性和操作会导致元素脱离文档流，从而影响其他元素的布局。以下是一些常见的会导致元素脱离文档流的操作：

1. **使用 `position` 属性**:
   - **绝对定位 (`position: absolute`)**:
     - 元素相对于最近的定位祖先（即 `position` 不为 `static` 的父元素）进行定位，脱离文档流，不占据空间。
   - **固定定位 (`position: fixed`)**:
     - 元素相对于视口进行定位，脱离文档流，始终固定在指定位置。
   - **粘性定位 (`position: sticky`)**:
     - 元素在特定的滚动位置时变为固定定位，脱离文档流，但在其容器内仍然占据空间。

2. **使用 `float` 属性**:
   - 当元素使用 `float` 属性（如 `float: left` 或 `float: right`）时，它会脱离文档流，其他元素会围绕它进行布局。浮动元素不再占据正常的文档流位置。

3. **使用 `display` 属性**:
   - **`display: none`**:
     - 元素完全从文档流中移除，不占据空间。
   - **`display: flex` 或 `display: grid`**:
     - 这些布局模型会改变子元素的布局方式，但不会使元素脱离文档流，除非结合其他属性使用。

4. **使用 `overflow` 属性**:
   - 当设置 `overflow: hidden`、`overflow: scroll` 或 `overflow: auto` 时，可能会影响元素的布局，尤其是在处理浮动或绝对定位的子元素时。

5. **使用 `margin` 属性**:
   - **负外边距 (`margin`)**:
     - 使用负外边距可能会导致元素重叠或脱离正常的文档流，影响周围元素的布局。

- 在页面布局中，使用绝对定位、固定定位、浮动、`display: none`、负外边距等操作会导致元素脱离文档流。这些操作会影响其他元素的布局和排列，因此在使用时需要谨慎考虑其对整体布局的影响。
:::

## transform 设置成 3D 和 flex、grid 布局是否会脱离文档流？

::: details
在 CSS 中，使用 `transform` 设置为 3D 变换和使用 `flex` 或 `grid` 布局的元素的行为如下：

1. **transform 设置为 3D**:
   - 当你对一个元素应用 `transform: translate3d(...)` 或其他 3D 变换时，该元素会脱离文档流。虽然它仍然占据空间，但其位置和布局会受到变换的影响。
   - 变换后的元素不会影响其他元素的布局，其他元素会按照正常的文档流进行排列。

2. **flex 布局**:
   - 使用 `display: flex` 的元素不会脱离文档流。相反，flex 容器会影响其子元素的布局方式。
   - Flex 子元素会根据 flex 属性（如 `flex-grow`、`flex-shrink` 和 `flex-basis`）进行排列和调整，但它们仍然占据文档流中的空间。

3. **grid 布局**:
   - 使用 `display: grid` 的元素同样不会脱离文档流。Grid 容器会影响其子元素的布局，允许在网格中进行排列。
   - Grid 子元素会根据网格定义的行和列进行布局，仍然占据文档流中的空间。

- **transform 3D**: 会影响元素的视觉呈现，但不会改变其在文档流中的占位。
- **flex 布局**: 不会脱离文档流，flex 容器和其子元素会根据 flex 属性进行布局。
- **grid 布局**: 同样不会脱离文档流，grid 容器和其子元素会根据网格定义进行布局。

:::
