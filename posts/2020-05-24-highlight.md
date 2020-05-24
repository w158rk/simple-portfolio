---
layout: post
title: highlight.js使用
excerpt: highlight.js使用
date: 2020-05-24
tags: highlight, post
author: Kyle
---

marked本身不支持代码高亮，所以我们用[highlight.js](https://highlightjs.org/)。

## 使用方法：

highlight.js支持的语言在[SUPPORTED_LANGUAGES](https://github.com/highlightjs/highlight.js/blob/master/SUPPORTED_LANGUAGES.md)。

例如C++:

```cpp 
int main() {
    printf("Simple Portfolio\n");
}
```

## marked文件修改方法：

```js
  Renderer.prototype.code = function(code, lang, escaped) {
    // ATTENTION: this is the code for highlight.js
    
    
    if (this.options.highlight) {
      const highlight = this.options.highlight;
      const validLang = !!(lang && hljs.getLanguage(lang));
      
      if(validLang) {
        var out = highlight(lang, code).value

        // solve the probelm of un-broken lines
        // use pre as the container

        return "<div class='container code'><pre>" + out + "</pre></div>"
      }

    }
  
    if (!lang) {
      return '<div class="container code"><pre><code>'
        + (escaped ? code : escape(code, true))
        + '</code></pre></div>';
    }
  
    return '<div class="container code"><pre><code>'
      + this.options.langPrefix
      + escape(lang, true)
      + '">'
      + (escaped ? code : escape(code, true))
      + '</code></pre></div>\n';
  };
```



