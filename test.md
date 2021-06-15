<!DOCTYPE html>
    <html>
    <head>
        <meta charset="UTF-8">
        <title>References</title>
        <style>
</style>
        <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.10.2/dist/katex.min.css" integrity="sha384-yFRtMMDnQtDRO8rLpMIKrtPCD5jdktao2TV19YiZYWMDkUR5GQZR/NOVTdquEx1j" crossorigin="anonymous">
<link href="https://cdn.jsdelivr.net/npm/katex-copytex@latest/dist/katex-copytex.min.css" rel="stylesheet" type="text/css">
        <link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/Microsoft/vscode/extensions/markdown-language-features/media/markdown.css">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/Microsoft/vscode/extensions/markdown-language-features/media/highlight.css">
<style>
            body {
                font-family: -apple-system, BlinkMacSystemFont, 'Segoe WPC', 'Segoe UI', system-ui, 'Ubuntu', 'Droid Sans', sans-serif;
                font-size: 14px;
                line-height: 1.6;
            }
        </style>
        <style>
.task-list-item { list-style-type: none; } .task-list-item-checkbox { margin-left: -20px; vertical-align: middle; }
</style>
        
        <script src="https://cdn.jsdelivr.net/npm/katex-copytex@latest/dist/katex-copytex.min.js"></script>
        
    </head>
    <body class="vscode-body vscode-light">
        <table>
<thead>
<tr>
<th>Macro</th>
<th>Definitions</th>
</tr>
</thead>
<tbody>
<tr>
<td>$&lt;</td>
<td>Source code hiện tại để compile, tương ứng với %.c và %.cpp, ví dụ: main.c, sum.c</td>
</tr>
<tr>
<td>$@</td>
<td>Target hiện tại tương ứng với $(OBJSDIR)/%.o, ví dụ: main.o, sum.o</td>
</tr>
<tr>
<td>$*</td>
<td>Tương tự $&lt; nhưng không có suffix, ví dụ: main, sum</td>
</tr>
<tr>
<td>$?</td>
<td>Danh sách dependency tương ứng với %.c $(HDRS), ví dụ: tương ứng với main.o là main.c và sum.h</td>
</tr>
</tbody>
</table>
<p><code>CFLAGS=-I.</code> : là danh sách kết hợp các flag của compliler.</p>
<ul>
<li><code>-I.</code> có nghĩa là include gcc sẽ thực hiện tìm kiếm trong thư mục hiện tại<code>.</code> để thêm file <code>hellomake.h</code>.</li>
</ul>
<p><code>LDFLASG=-L</code> : Linker Flags , dùng trong quá trình linking các thư viện.</p>
<h3 id="example">Example:</h3>
<pre><code class="language-makefile"><div>CC= gcc
objs:= <span class="hljs-variable">$(<span class="hljs-built_in">patsubst</span> %.c,%.o,$(<span class="hljs-built_in">wildcard</span> *.c)</span>)
TARGET:= main
CFLAGS += -I.
LDFLAGS += -L. -lm

<span class="hljs-meta"><span class="hljs-meta-keyword">.PHONY</span>: all</span>
<span class="hljs-section">all: <span class="hljs-variable">$(TARGET)</span> clean test </span>
<span class="hljs-variable">$(TARGET)</span>:<span class="hljs-variable">$(objs)</span>
   <span class="hljs-variable">$(CC)</span> -o <span class="hljs-variable">$(TARGET)</span> <span class="hljs-variable">$(objs)</span> <span class="hljs-variable">$(LDFLAGS)</span>

<span class="hljs-section">%.o: %.c</span>
   <span class="hljs-variable">$(CC)</span> -c <span class="hljs-variable">$^</span> -o <span class="hljs-variable">$@</span> <span class="hljs-variable">$(CFLAGS)</span>

<span class="hljs-meta"><span class="hljs-meta-keyword">.PHONY</span>: clean</span>
<span class="hljs-section">clean:</span>
   rm -rf *.o

<span class="hljs-meta"><span class="hljs-meta-keyword">.PHONY</span>: test</span>
<span class="hljs-section">test: <span class="hljs-variable">$(TARGET)</span></span>
   exec ./<span class="hljs-variable">$(TARGET)</span>

<span class="hljs-meta"><span class="hljs-meta-keyword">.PHONY</span>: valgrind</span>
<span class="hljs-section">valgrind:</span>
   exec valgrind ./<span class="hljs-variable">$(TARGET)</span>
   
<span class="hljs-meta"><span class="hljs-meta-keyword">.PHONY</span>: cppcheck</span>
<span class="hljs-section">cppcheck:</span>
   exec cppcheck ./main.c
</div></code></pre>
<h2 id="references">References</h2>
<ol>
<li><a href="http://eslinuxprogramming.blogspot.com/2015/06/makefile-part-2.html">Makefile Part 2</a></li>
<li><a href="https://hocarm.org/makefile-la-gi/">Makfile là gì?</a></li>
</ol>

    </body>
    </html>
