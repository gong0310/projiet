<template>
  <div id="highlight">
    <h3>格式化代码并高亮显示</h3>
    <div id="code-container">
      <div class="code-mac">
        <pre><code data-prismjs-copy="复制" data-prismjs-copy-success="复制成功!" class="language-js"></code></pre>
      </div>
      <div class="code-mac">
        <pre><code data-prismjs-copy="复制" data-prismjs-copy-success="复制成功!" class="language-css"></code></pre>
      </div>
      <div class="code-mac">
        <pre><code data-prismjs-copy="复制" data-prismjs-copy-success="复制成功!" class="language-html"></code></pre>
      </div>
    </div>
  </div>
</template>

<script>
import Prism from "prismjs";
import "prismjs/themes/prism-okaidia.css";
import "prism-themes/themes/prism-one-dark.css";
import "prismjs/plugins/toolbar/prism-toolbar";
import "prismjs/plugins/show-language/prism-show-language";
import "prismjs/plugins/copy-to-clipboard/prism-copy-to-clipboard";
import "prismjs/plugins/line-numbers/prism-line-numbers.js";
import "prismjs/plugins/line-numbers/prism-line-numbers.css";
const beautifyJS = require("js-beautify");

export default {
  name: "HighlightCode",
  data() {
    return {};
  },
  mounted() {
    // Add pre-mac element for Mac Style UI
    const container = document?.getElementById("code-container");
    const codeBlocks = container?.getElementsByTagName("pre");
    Array.from(codeBlocks).forEach((item) => {
      const preMac = document.createElement("div");
      preMac.classList.add("pre-mac");
      preMac.innerHTML = "<span></span><span></span><span></span>";
      item.parentElement.insertBefore(preMac, item);
      item.style.whiteSpace = "pre-wrap";
      item.classList.add("line-numbers"); // 加入 行數
    });
    //---------------------------------------------------------------------
    let htm =
      "<h3>Ecosystem</h3><ul><li>vue-router</li><li>vuex</li><li>vue-devtools</li><li>vue-loader</li></ul>";
    htm = beautifyJS.html_beautify(htm, {
      indent_size: 2,
      space_in_empty_paren: true,
      end_with_newline: true,
    });

    const html = Prism.highlight(htm, Prism.languages.html, "html");
    document.querySelector(".language-html").innerHTML = html;
    //---------------------------------------------------------------------

    let js =
      "let name = '小米';function setName(value) {return value + '手机';}setName(name);";
    js = beautifyJS(js, {
      indent_size: 2, //缩进两个空格
      space_in_empty_paren: true,
    });

    const jss = Prism.highlight(js, Prism.languages.javascript, "javascript");
    document.querySelector(".language-js").innerHTML = jss;
    //---------------------------------------------------------------------
    let cs = "h3 {margin: 40px 0 0;} ul {list-style-type: none;padding: 0;}";
    cs = beautifyJS.css_beautify(cs, {
      indent_size: 1,
    });

    const css = Prism.highlight(cs, Prism.languages.css, "css");
    document.querySelector(".language-css").innerHTML = css;
    Prism.highlightAll()
  },
  methods: {},
};
</script>

<style>
#highlight {
  width: 800px;
}
.code-mac {
  position: relative;
}
.code-toolbar {
  position: relative;
}

.toolbar {
  position: absolute;
  top: 10px;
  right: 10px;
  display: flex;
  font-size: 12px;
  align-items: center;
}
.copy-to-clipboard-button {
  border: none;
}
pre {
  padding-top: 2em !important;
}
.pre-mac {
  position: absolute;
  top: 10px;
  left: 10px;
  z-index: 99;
}
.pre-mac > span {
  float: left;
  width: 10px;
  height: 10px;
  border-radius: 50%;
  margin-right: 5px;
}
.pre-mac > span:nth-child(1) {
  background: red;
}
.pre-mac > span:nth-child(2) {
  background: sandybrown;
}
.pre-mac > span:nth-child(3) {
  background: limegreen;
}
</style>
