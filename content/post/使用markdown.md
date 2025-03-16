## 快捷键

#### 窗口操作

- `command + 1`：收起展开目录
- `command + 2`：收起展开文档列表
- `command + 3`：切换编辑和预览
- `command + 4`：切换到演示模式

#### 文件操作

- `command + n`：新建文档
- `command + r`：重命名文档
- `command + d`：复制文档
- `command + o`：单独打开文档
- `command + delete`：删除文档
- `command + shift + n`：新建文件夹
- `command + shift + l`：自动排版
- `command + option + r`：在 Finder 中显示
- `command + option + i`：显示字数等文档属性


# 控制顺序也很简单

- Item 1：最后一个出现 <!-- .element: class="fragment" data-fragment-index="3" -->
- Item 2：第二个出现 <!-- .element: class="fragment" data-fragment-index="2" -->
- Item 3：第一个出现 <!-- .element: class="fragment" data-fragment-index="1" -->

---

# 展示代码也好弄

```js [1|2-4|5]
import { withTable，useTable } from 'table-render';
const Page = () => {
    const { refresh } = useTable();
}
export default withTable(Page)
```

---

# 来一个牛逼的效果

<p class="fragment">Fade in</p>
<p class="fragment fade-out">Fade out</p>
<p class="fragment highlight-red">Highlight red</p>
<p class="fragment fade-in-then-out">Fade in, then out</p>
<p class="fragment fade-up">Slide up while fading in</p>

---

<!-- .slide: data-background-iframe="https://miaoyan.app/" -->
<!-- .slide: data-background-interactive -->

---

<!-- .slide: data-background-gradient="radial-gradient(#36563C, #4A674F)" -->
<h1 style="color:#fff">希望可以伴你写出妙言❤️</h1>
