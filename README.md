# loader

## Introduction
A javascript js & css loader & show markdown library for browsers (IE9+).
- js-loader
- css-loader
- markdown-loader

## Demo
1. [loader](https://rawgit.com/softm/loader/master/loader.html)

2. [markdown highlight - showdonwjs](https://rawgit.com/softm/loader/master/markdown_highlight.html)

3. [markdown highlight - markedjs](https://rawgit.com/softm/loader/master/markdown_highlight_markedjs.html)

Usage
-----
```html
<!--
<script type="text/javascript" src="https://rawgit.com/softm/loader/master/loader.js"></script>
-->
<script type="text/javascript" src="//loader.js"></script>
<script type="text/javascript">
window.onload = function () {
    loader.js(
      [
          "https://rawgit.com/softm/loader/master/foo.js",
          "https://rawgit.com/softm/loader/master/bar.js",
          "https://rawgit.com/softm/loader/master/loader.css"
      ],
      [
        function(e) {
          console.log("1st",e);
        },
        function(e) {
          console.log("2nd",e);
        },
        function(e) {
          console.log("3rd",e);
        }
      ],
      false // default false
    );
}
</script>
<div class="hello">Hello loader</div>
```

## Documentation
1. example-1 ( load single )
```html
<script type="text/javascript">
    loader.js(
      "https://rawgit.com/softm/loader/master/foo.js",
      function(e) {
        console.log("this",e);
      };    
    });
</script>
```

2. example-2 ( load parallel synchronously )
```html
<script type="text/javascript">
window.onload = function () {
    loader.js(
      [
        "https://rawgit.com/softm/loader/master/foo.js",
        "https://rawgit.com/softm/loader/master/bar.js",
        "https://rawgit.com/softm/loader/master/loader.css"
      ],
      [
        function(e) {
         console.log("1st",e);
       },
        function(e) {
         console.log("2nd",e);
       },
        function(e) {
         console.log("3rd",e);
        }                  
      ],
      true
    });
}
</script>
<div class="hello">Hello loader</div>
```

3. example-3 ( load parallel asynchronously )
```html
<script type="text/javascript">
window.onload = function () {
    loader.js(
      [
        "https://rawgit.com/softm/loader/master/foo.js",
        "https://rawgit.com/softm/loader/master/bar.js",
        "https://rawgit.com/softm/loader/master/loader.css"
      ],
      [
        function(e) {
         console.log("1st",e);
       },
        function(e) {
         console.log("2nd",e);
       },
        function(e) {
         console.log("3rd",e);
        }
      ]
    );
  }
</script>
<div class="hello">Hello loader</div>
```

4. example-4 ( markdown highlighting syntax : https://rawgit.com/softm/loader/master/markdown_highlight.html )
   - showdownjs : http://demo.showdownjs.com/, https://github.com/showdownjs/showdown

```html
<script type="text/javascript">
window.onload = function () {
    loader.js(
        [
            "https://cdnjs.cloudflare.com/ajax/libs/showdown/1.8.6/showdown.min.js",
            "https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.12.0/highlight.min.js",
            "https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.12.0/styles/default.min.css"
        ],
        [
          function(e) {
            console.log("1st",e);
          },
          function(e) {
            console.log("2nd",e);
          },
          function(e) {
            console.log("3rd",e);
            var container = document.getElementById("contents");
            var containers = [container];
            var sd = new showdown.Converter();
            for (var i = 0; i < containers.length; i++) {
                containers[i].innerHTML = sd.makeHtml(containers[i].innerHTML);
                var codes = containers[i].querySelectorAll("pre code");
/*
                codes.forEach(function(code) {
                    hljs.highlightBlock(code);
                });
*/
                for(var j=0;j<codes.length;j++) {
                    var code = codes[j];
                         hljs.highlightBlock(code);
                }
            }
          }
        ],
        false // default false
    );
}
</script>
  <pre id="contents">
  ##Javascript
  ```javascript
  var s = "JavaScript syntax highlighting";
  alert(s);
  ```  </pre>
```
4. example-5 ( markdown highlighting syntax : https://rawgit.com/softm/loader/master/markdown_highlight_markedjs.html )
   - markedjs : https://marked.js.org

```html
<script type="text/javascript">
window.onload = function () {
    loader.js(
        [
            "https://cdn.jsdelivr.net/npm/marked/marked.min.js",
            "https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.12.0/highlight.min.js",
            "https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.12.0/styles/default.min.css"
        ],
        [
          function(e) {
            console.log("1st",e);
          },
          function(e) {
            console.log("2nd",e);
          },
          function(e) {
            console.log("3rd",e);
            var container = document.getElementById("contents");
            var containers = [container];
            for (var i = 0; i < containers.length; i++) {
                containers[i].innerHTML = marked(containers[i].innerHTML);                
                var codes = containers[i].querySelectorAll("pre code");
/*
                codes.forEach(function(code) {
                    hljs.highlightBlock(code);
                });
*/
                for(var j=0;j<codes.length;j++) {
                    var code = codes[j];
                         hljs.highlightBlock(code);
                }
            }
          }
        ],
        false // default false
    );
}
</script>
  <pre id="contents">
  ##Javascript
  ```javascript
  var s = "JavaScript syntax highlighting";
  alert(s);
  ```  </pre>
```
