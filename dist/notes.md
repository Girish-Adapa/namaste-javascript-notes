<!DOCTYPE html>
<html>
  <head>
    <title>title: Namaste JavaScript</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link type="text/css" rel="stylesheet" href="assets/style.css" />
    <link type="text/css" rel="stylesheet" href="assets/pilcrow.css" />
    <link type="text/css" rel="stylesheet" href="assets/hljs-github.min.css"/>
  </head>
<body><h2 id="title-namaste-javascript"><a class="header-link" href="#title-namaste-javascript"></a>title: Namaste JavaScript</h2>
<br>

<h1 id="episode-1--execution-context"><a class="header-link" href="#episode-1--execution-context"></a>Episode 1 : Execution Context</h1>
<ul class="list">
<li><p>Everything in JS happens inside the execution context. Imagine a sealed-off container inside which JS runs. It is an abstract concept that hold info about the env. within the current code is being executed.
<img src="../assets/execution-context.jpg" alt="Execution Context" title="Execution Context"></p>
</li>
<li><p>In the container the first component is <strong>memory component</strong> and the 2nd one is <strong>code component</strong></p>
</li>
<li><p>Memory component has all the variables and functions in key value pairs. It is also called <strong>Variable environment</strong>.</p>
</li>
<li><p>Code component is the place where code is executed one line at a time. It is also called the <strong>Thread of Execution</strong>.</p>
</li>
<li><p>JS is a <strong>synchronous</strong>, <strong>single-threaded</strong> language</p>
<ul class="list">
<li>Synchronous:- In a specific synchronous order.</li>
<li>Single-threaded:- One command at a time.</li>
</ul>
</li>
</ul>
<hr>

<br>

<hr>

<br>

<h1 id="episode-2--how-js-is-executed--call-stack"><a class="header-link" href="#episode-2--how-js-is-executed--call-stack"></a>Episode 2 : How JS is executed &amp; Call Stack</h1>
<ul class="list">
<li><p>When a JS program is ran, a <strong>global execution context</strong> is created.</p>
</li>
<li><p>The execution context is created in two phases.</p>
<ul class="list">
<li>Memory creation phase - JS will allocate memory to variables and functions.</li>
<li>Code execution phase</li>
</ul>
</li>
<li><p>Let&#39;s consider the below example and its code execution steps:</p>
</li>
</ul>
<pre class="hljs"><code><span class="hljs-keyword">var</span> n = <span class="hljs-number">2</span>;
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">square</span>(<span class="hljs-params">num</span>) </span>{
  <span class="hljs-keyword">var</span> ans = num * num;
  <span class="hljs-keyword">return</span> ans;
}
<span class="hljs-keyword">var</span> square2 = square(n);
<span class="hljs-keyword">var</span> square4 = square(<span class="hljs-number">4</span>);</code></pre><p>The very <strong>first</strong> thing which JS does is <strong>memory creation phase</strong>, so it goes to line one of above code snippet, and <strong>allocates a memory space</strong> for variable <strong>&#39;n&#39;</strong> and then goes to line two, and <strong>allocates a memory space</strong> for <strong>function &#39;square&#39;</strong>. When allocating memory <strong>for n it stores &#39;undefined&#39;</strong>, a special value for &#39;n&#39;. <strong>For &#39;square&#39;, it stores the whole code of the function inside its memory space.</strong> Then, as square2 and square4 are variables as well, it allocates memory and stores &#39;undefined&#39; for them, and this is the end of first phase i.e. memory creation phase.</p>
<p>So O/P will look something like</p>
<p class="img-container"><img src="../assets/phase1.jpg" alt="Execution Context Phase 1" title="Execution Context"></p>
<p>Now, in <strong>2nd phase</strong> i.e. code execution phase, it starts going through the whole code line by line. As it encounters var n = 2, it assigns 2 to &#39;n&#39;. Until now, the value of &#39;n&#39; was undefined. For function, there is nothing to execute. As these lines were already dealt with in memory creation phase.</p>
<p>Coming to line 6 i.e. <strong>var square2 = square(n)</strong>, here <strong>functions are a bit different than any other language. A new execution context is created altogether.</strong> Again in this new execution context, in memory creation phase, we allocate memory to num and ans the two variables. And undefined is placed in them. Now, in code execution phase of this execution context, first 2 is assigned to num. Then var ans = num * num will store 4 in ans. After that, return ans returns the control of program back to where this function was invoked from.</p>
<p class="img-container"><img src="../assets/phase2.jpg" alt="Execution Context Phase 2" title="Execution Context"></p>
<p>When <strong>return</strong> keyword is encountered, It returns the control to the called line and also <strong>the function execution context is deleted</strong>.
Same thing will be repeated for square4 and then after that is finished, the global execution context will be destroyed.
So the <strong>final diagram</strong> before deletion would look something like:</p>
<p class="img-container"><img src="../assets/final_execution_context.jpg" alt="Execution Context Phase 2" title="Execution Context"></p>
<ul class="list">
<li><p>Javascript manages code execution context creation and deletion with the the help of <strong>Call Stack</strong>.</p>
</li>
<li><p>Call Stack is a mechanism to keep track of its place in script that calls multiple function.</p>
</li>
<li><p>Call Stack maintains the order of execution of execution contexts. It is also known as Program Stack, Control Stack, Runtime stack, Machine Stack, Execution context stack.</p>
</li>
</ul>
<hr>

<br>

<hr>

<br>

<h1 id="episode-3--hoisting-in-javascript-variables--functions"><a class="header-link" href="#episode-3--hoisting-in-javascript-variables--functions"></a>Episode 3 : Hoisting in JavaScript (variables &amp; functions)</h1>
<ul class="list">
<li>Let&#39;s observe the below code and it&#39;s explaination:</li>
</ul>
<pre class="hljs"><code>getName(); <span class="hljs-comment">// Namaste Javascript</span>
<span class="hljs-built_in">console</span>.log(x); <span class="hljs-comment">// undefined</span>
<span class="hljs-keyword">var</span> x = <span class="hljs-number">7</span>;
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">getName</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;Namaste Javascript&quot;</span>);
}</code></pre><ul class="list">
<li><p>It should have been an outright error in many other languages, as it is not possible to even access something which is not even created (defined) yet But in JS, We know that in memory creation phase it assigns undefined and puts the content of function to function&#39;s memory. And in execution, it then executes whatever is asked. Here, as execution goes line by line and not after compiling, it could only print undefined and nothing else. This phenomenon, is not an error. However, if we remove var x = 7; then it gives error. Uncaught ReferenceError: x is not defined</p>
</li>
<li><p><strong>Hoisting</strong> is a concept which enables us to extract values of variables and functions even before initialising/assigning value without getting error and this is happening due to the 1st phase (memory creation phase) of the Execution Context.</p>
</li>
<li><p>So in previous lecture, we learnt that execution context gets created in two phase, so even before code execution, memory is created so in case of variable, it will be initialized as undefined while in case of function the whole function code is placed in the memory. Example:</p>
</li>
</ul>
<pre class="hljs"><code>getName(); <span class="hljs-comment">// Namaste JavaScript</span>
<span class="hljs-built_in">console</span>.log(x); <span class="hljs-comment">// Uncaught Reference: x is not defined.</span>
<span class="hljs-built_in">console</span>.log(getName); <span class="hljs-comment">// f getName(){ console.log(&quot;Namaste JavaScript); }</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">getName</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;Namaste JavaScript&quot;</span>);
}</code></pre><ul class="list">
<li>Now let&#39;s observe a different example and try to understand the output.</li>
</ul>
<pre class="hljs"><code>getName(); <span class="hljs-comment">// Uncaught TypeError: getName is not a function</span>
<span class="hljs-built_in">console</span>.log(getName);
<span class="hljs-keyword">var</span> getName = <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;Namaste JavaScript&quot;</span>);
};
<span class="hljs-comment">// The code won&#x27;t execute as the first line itself throws an TypeError.</span></code></pre><hr>

<br>

<hr>

<br>

<h1 id="episode-4--functions-and-variable-environments"><a class="header-link" href="#episode-4--functions-and-variable-environments"></a>Episode 4 : Functions and Variable Environments</h1>
<pre class="hljs"><code><span class="hljs-keyword">var</span> x = <span class="hljs-number">1</span>;
a();
b(); <span class="hljs-comment">// we are calling the functions before defining them. This will work properly, as seen in Hoisting.</span>
<span class="hljs-built_in">console</span>.log(x);

<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">a</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-keyword">var</span> x = <span class="hljs-number">10</span>; <span class="hljs-comment">// local scope because of separate execution context</span>
  <span class="hljs-built_in">console</span>.log(x);
}

<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">b</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-keyword">var</span> x = <span class="hljs-number">100</span>;
  <span class="hljs-built_in">console</span>.log(x);
}</code></pre><p>Outputs:</p>
<blockquote>
<p>10</p>
</blockquote>
<blockquote>
<p>100</p>
</blockquote>
<blockquote>
<p>1</p>
</blockquote>
<h2 id="code-flow-in-terms-of-execution-context"><a class="header-link" href="#code-flow-in-terms-of-execution-context"></a>Code Flow in terms of Execution Context</h2>
<ul class="list">
<li>The Global Execution Context (GEC) is created (the big box with Memory and Code subparts). Also GEC is pushed into Call Stack</li>
</ul>
<blockquote>
<p>Call Stack : GEC</p>
</blockquote>
<ul class="list">
<li><p>In first phase of GEC (memory phase), variable x:undefined and a and b have their entire function code as value initialized</p>
</li>
<li><p>In second phase of GEC (execution phase), when the function is called, a new local Execution Context is created. After x = 1 assigned to GEC x, a() is called. So local EC for a is made inside code part of GEC.</p>
</li>
</ul>
<blockquote>
<p>Call Stack: [GEC, a()]</p>
</blockquote>
<ul class="list">
<li>For local EC, a totally different x variable assigned undefined(x inside a()) in phase 1 , and in phase 2 it is assigned 10 and printed in console log. After printing, no more commands to run, so a() local EC is removed from both GEC and from Call stack</li>
</ul>
<blockquote>
<p>Call Stack: GEC</p>
</blockquote>
<ul class="list">
<li>Cursor goes back to b() function call. Same steps repeat.</li>
</ul>
<blockquote>
<p>Call Stack :[GEC, b()] -&gt; GEC (after printing yet another totally different x value as 100 in console log)</p>
</blockquote>
<ul class="list">
<li><p>Finally GEC is deleted and also removed from call stack. Program ends.</p>
</li>
<li><p>reference:</p>
</li>
</ul>
<p class="img-container"><img src="../assets/function.jpg" alt="Execution Context Phase 1" title="Execution Context"></p>
<hr>

<br>

<hr>

<br>

<h1 id="episode-5--shortest-js-program-window--this-keyword"><a class="header-link" href="#episode-5--shortest-js-program-window--this-keyword"></a>Episode 5 : Shortest JS Program, window &amp; this keyword</h1>
<ul class="list">
<li><p>The shortest JS program is empty file. Because even then, JS engine does a lot of things. As always, even in this case, it creates the GEC which has memory space and the execution context.</p>
</li>
<li><p>JS engine creates something known as &#39;<strong>window</strong>&#39;. It is an object, which is created in the global space. It contains lots of functions and variables. These functions and variables can be accessed from anywhere in the program. JS engine also creates a <strong>this</strong> keyword, which points to the <strong>window object</strong> at the global level. So, in summary, along with GEC, a global object (window) and a this variable are created.</p>
</li>
<li><p>In different engines, the name of global object changes. Window in browsers, but in nodeJS it is called something else. At global level, this === window</p>
</li>
<li><p>If we create any variable in the global scope, then the variables get attached to the global object.</p>
</li>
</ul>
<p>eg:</p>
<pre class="hljs"><code><span class="hljs-keyword">var</span> x = <span class="hljs-number">10</span>;
<span class="hljs-built_in">console</span>.log(x); <span class="hljs-comment">// 10</span>
<span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>.x); <span class="hljs-comment">// 10</span>
<span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">window</span>.x); <span class="hljs-comment">// 10</span></code></pre><hr>

<br>

<hr>

<br>

<h1 id="episode-6--undefined-vs-not-defined-in-js"><a class="header-link" href="#episode-6--undefined-vs-not-defined-in-js"></a>Episode 6 : undefined vs not defined in JS</h1>
<ul class="list">
<li><p>In first phase (memory allocation) JS assigns each variable a placeholder called <strong>undefined</strong>.</p>
</li>
<li><p><strong>undefined</strong> is when memory is allocated for the variable, but no value is assigned yet.</p>
</li>
<li><p>If an object/variable is not even declared/found in memory allocation phase, and tried to access it then it is <strong>Not defined</strong></p>
</li>
<li><p>Not Defined !== Undefined</p>
</li>
</ul>
<blockquote>
<p>When variable is declared but not assigned value, its current value is <strong>undefined</strong>. But when the variable itself is not declared but called in code, then it is <strong>not defined</strong>.</p>
</blockquote>
<pre class="hljs"><code><span class="hljs-built_in">console</span>.log(x); <span class="hljs-comment">// undefined</span>
<span class="hljs-keyword">var</span> x = <span class="hljs-number">25</span>;
<span class="hljs-built_in">console</span>.log(x); <span class="hljs-comment">// 25</span>
<span class="hljs-built_in">console</span>.log(a); <span class="hljs-comment">// Uncaught ReferenceError: a is not defined</span></code></pre><ul class="list">
<li>JS is a <strong>loosely typed / weakly typed</strong> language. It doesn&#39;t attach variables to any datatype. We can say <em>var a = 5</em>, and then change the value to boolean <em>a = true</em> or string <em>a = &#39;hello&#39;</em> later on.</li>
<li><strong>Never</strong> assign <em>undefined</em> to a variable manually. Let it happen on it&#39;s own accord.</li>
</ul>
<hr>

<br>

<hr>

<br>

<h1 id="episode-7--the-scope-chain-scope--lexical-environment"><a class="header-link" href="#episode-7--the-scope-chain-scope--lexical-environment"></a>Episode 7 : The Scope Chain, Scope &amp; Lexical Environment</h1>
<ul class="list">
<li><p><strong>Scope</strong> in Javascript is directly related to <strong>Lexical Environment</strong>.</p>
</li>
<li><p>Let&#39;s observe the below examples:</p>
</li>
</ul>
<pre class="hljs"><code><span class="hljs-comment">// CASE 1</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">a</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-built_in">console</span>.log(b); <span class="hljs-comment">// 10</span>
  <span class="hljs-comment">// Instead of printing undefined it prints 10, So somehow this a function could access the variable b outside the function scope.</span>
}
<span class="hljs-keyword">var</span> b = <span class="hljs-number">10</span>;
a();</code></pre><pre class="hljs"><code><span class="hljs-comment">// CASE 2</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">a</span>(<span class="hljs-params"></span>) </span>{
  c();
  <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">c</span>(<span class="hljs-params"></span>) </span>{
    <span class="hljs-built_in">console</span>.log(b); <span class="hljs-comment">// 10</span>
  }
}
<span class="hljs-keyword">var</span> b = <span class="hljs-number">10</span>;
a();</code></pre><pre class="hljs"><code><span class="hljs-comment">// CASE 3</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">a</span>(<span class="hljs-params"></span>) </span>{
  c();
  <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">c</span>(<span class="hljs-params"></span>) </span>{
    <span class="hljs-keyword">var</span> b = <span class="hljs-number">100</span>;
    <span class="hljs-built_in">console</span>.log(b); <span class="hljs-comment">// 100</span>
  }
}
<span class="hljs-keyword">var</span> b = <span class="hljs-number">10</span>;
a();</code></pre><pre class="hljs"><code><span class="hljs-comment">// CASE 4</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">a</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-keyword">var</span> b = <span class="hljs-number">10</span>;
  c();
  <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">c</span>(<span class="hljs-params"></span>) </span>{
    <span class="hljs-built_in">console</span>.log(b); <span class="hljs-comment">// 10</span>
  }
}
a();
<span class="hljs-built_in">console</span>.log(b); <span class="hljs-comment">// Error, Not Defined</span></code></pre><ul class="list">
<li>Let&#39;s try to understand the output in each of the cases above.<ul class="list">
<li>In <strong>case 1</strong>: function a is able to access variable b from Global scope.</li>
<li>In <strong>case 2</strong>: 10 is printed. It means that within nested function too, the global scope variable can be accessed.</li>
<li>In <strong>case 3</strong>: 100 is printed meaning local variable of the same name took precedence over a global variable.</li>
<li>In <strong>case 4</strong>: A function can access a global variable, but the global execution context can&#39;t access any local variable.<pre class="prettyprint">To summarize the above points in terms of execution context:
call_stack = [GEC, a(), c()]
Now lets also assign the memory sections of each execution context in call_stack.
c() = [[lexical environment pointer pointing to a()]]
a() = [b:10, c:{}, [lexical environment pointer pointing to GEC]]
GEC =  [a:{},[lexical_environment pointer pointing to null]]
</pre>
<img src="../assets/lexical.jpg" alt="Lexical Scope Explaination" title="Lexical Scope">
<img src="../assets/lexical2.jpg" alt="Lexical Scope Explaination" title="Lexical Scope"></li>
</ul>
</li>
</ul>
<br>

<ul class="list">
<li><p>So, <strong>Lexical Environment</strong> = local memory + lexical env of its parent. Hence, Lexical Environement is the local memory along with the lexical environment of its parent</p>
</li>
<li><p><strong>Lexical</strong>: In hierarchy, In order</p>
</li>
<li><p>Whenever an Execution Context is created, a Lexical environment(LE) is also created and is referenced in the local Execution Context(in memory space).</p>
</li>
<li><p>The process of going one by one to parent and checking for values is called scope chain or Lexcial environment chain.</p>
</li>
<li><pre class="prettyprint">function a() {
  function c() {
    // logic here
  }
  c(); // c is lexically inside a
} // a is lexically inside global execution
</pre>
</li>
<li><p>Lexical or Static scope refers to the accessibility of variables, functions and object based on physical location in source code.</p>
<pre class="prettyprint">Global {
    Outer {
        Inner
    }
}
// Inner is surrounded by lexical scope of Outer
</pre>
</li>
<li><p><strong>TLDR</strong>; An inner function can access variables which are in outer functions even if inner function is nested deep. In any other case, a function can&#39;t access variables not in its scope.</p>
</li>
</ul>
<hr>

<br>

<hr>

<br>

<h1 id="episode-8--let--const-in-js-temporal-dead-zone"><a class="header-link" href="#episode-8--let--const-in-js-temporal-dead-zone"></a>Episode 8 : let &amp; const in JS, Temporal Dead Zone</h1>
<ul class="list">
<li>let and const declarations are hoisted. But its different from <strong>var</strong></li>
</ul>
<pre class="hljs"><code><span class="hljs-built_in">console</span>.log(a); <span class="hljs-comment">// ReferenceError: Cannot access &#x27;a&#x27; before initialization</span>
<span class="hljs-built_in">console</span>.log(b); <span class="hljs-comment">// prints undefined as expected</span>
<span class="hljs-keyword">let</span> a = <span class="hljs-number">10</span>;
<span class="hljs-built_in">console</span>.log(a); <span class="hljs-comment">// 10</span>
<span class="hljs-keyword">var</span> b = <span class="hljs-number">15</span>;
<span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">window</span>.a); <span class="hljs-comment">// undefined</span>
<span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">window</span>.b); <span class="hljs-comment">// 15</span></code></pre><p>It looks like let isn&#39;t hoisted, <strong>but it is</strong>, let&#39;s understand</p>
<ul class="list">
<li>Both a and b are actually initialized as <em>undefined</em> in hoisting stage. But var <strong>b</strong> is inside the storage space of GLOBAL, and <strong>a</strong> is in a separate memory object called script, where it can be accessed only after assigning some value to it first ie. one can access &#39;a&#39; only if it is assigned. Thus, it throws error.</li>
</ul>
<br>

<ul class="list">
<li><p><strong>Temporal Dead Zone</strong> : Time since when the let variable was hoisted until it is initialized some value.</p>
<ul class="list">
<li>So any line till before &quot;let a = 10&quot; is the TDZ for a</li>
<li>Since a is not accessible on global, its not accessible in <em>window/this</em> also. window.b or this.b -&gt; 15; But window.a or this.a -&gt;undefined, just like window.x-&gt;undefined (x isn&#39;t declared anywhere)</li>
</ul>
</li>
<li><p><strong>Reference Error</strong> are thrown when variables are in temporal dead zone.</p>
</li>
<li><p><strong>Syntax Error</strong> doesn&#39;t even let us run single line of code.</p>
</li>
</ul>
<pre class="hljs"><code><span class="hljs-keyword">let</span> a = <span class="hljs-number">10</span>;
<span class="hljs-keyword">let</span> a = <span class="hljs-number">100</span>;  <span class="hljs-comment">//this code is rejected upfront as SyntaxError. (duplicate declaration)</span>
------------------
<span class="hljs-keyword">let</span> a = <span class="hljs-number">10</span>;
<span class="hljs-keyword">var</span> a = <span class="hljs-number">100</span>; <span class="hljs-comment">// this code also rejected upfront as SyntaxError. (can&#x27;t use same name in same scope)</span></code></pre><ul class="list">
<li><strong>Let</strong> is a stricter version of <strong>var</strong>. Now, <strong>const</strong> is even more stricter than <strong>let</strong>.</li>
</ul>
<pre class="hljs"><code><span class="hljs-keyword">let</span> a;
a = <span class="hljs-number">10</span>;
<span class="hljs-built_in">console</span>.log(a) <span class="hljs-comment">// 10. Note declaration and assigning of a is in different lines.</span>
------------------
<span class="hljs-keyword">const</span> b;
b = <span class="hljs-number">10</span>;
<span class="hljs-built_in">console</span>.log(b); <span class="hljs-comment">// SyntaxError: Missing initializer in const declaration. (This type of declaration won&#x27;t work with const. const b = 10 only will work)</span>
------------------
<span class="hljs-keyword">const</span> b = <span class="hljs-number">100</span>;
b = <span class="hljs-number">1000</span>; <span class="hljs-comment">//this gives us TypeError: Assignment to constant variable.</span></code></pre><ul class="list">
<li><p>Types of <strong>Error</strong>: Syntax, Reference, and Type.</p>
<ul class="list">
<li><p>Uncaught ReferenceError: x is not defined at ...</p>
<ul class="list">
<li>This Error signifies that x has never been in the scope of the program. This literally means that x was never defined/declared and is being tried to be accesed.</li>
</ul>
</li>
<li><p>Uncaught ReferenceError: cannot access &#39;a&#39; before initialization</p>
<ul class="list">
<li>This Error signifies that &#39;a&#39; cannot be accessed because it is declared as &#39;let&#39; and since it is not assigned a value, it is its Temporal Dead Zone. Thus, this error occurs.</li>
</ul>
</li>
<li><p>Uncaught SyntaxError: Identifier &#39;a&#39; has already been declared</p>
<ul class="list">
<li>This Error signifies that we are redeclaring a variable that is &#39;let&#39; declared. No execution will take place.</li>
</ul>
</li>
<li><p>Uncaught SyntaxError: Missing initializer in const declaration</p>
<ul class="list">
<li>This Error signifies that we haven&#39;t initialized or assigned value to a const declaration.</li>
</ul>
</li>
<li><p>Uncaught TypeError: Assignment to constant variable</p>
<ul class="list">
<li>This Error signifies that we are reassigning to a const variable.</li>
</ul>
</li>
</ul>
</li>
</ul>
<h3 id="some-good-practices"><a class="header-link" href="#some-good-practices"></a>SOME GOOD PRACTICES:</h3>
<ul class="list">
<li>Try using const wherever possible.</li>
<li>If not, use let, Avoid var.</li>
<li>Declare and initialize all variables with let to the top to avoid errors to shrink temporal dead zone window to zero.</li>
</ul>
<hr>

<br>

<hr>

<br>

<h1 id="episode-9--block-scope--shadowing-in-js"><a class="header-link" href="#episode-9--block-scope--shadowing-in-js"></a>Episode 9 : Block Scope &amp; Shadowing in JS</h1>
<p>What is a <strong>Block</strong>?</p>
<ul class="list">
<li>Block aka <em>compound statement</em> is used to group JS statements together into 1 group. We group them within {...}</li>
</ul>
<pre class="hljs"><code>{
  <span class="hljs-keyword">var</span> a = <span class="hljs-number">10</span>;
  <span class="hljs-keyword">let</span> b = <span class="hljs-number">20</span>;
  <span class="hljs-keyword">const</span> c = <span class="hljs-number">30</span>;
  <span class="hljs-comment">// Here let and const are hoisted in Block scope,</span>
  <span class="hljs-comment">// While, var is hoisted in Global scope.</span>
}</code></pre><ul class="list">
<li>Block Scope and its accessibility example</li>
</ul>
<pre class="hljs"><code>{
  <span class="hljs-keyword">var</span> a = <span class="hljs-number">10</span>;
  <span class="hljs-keyword">let</span> b = <span class="hljs-number">20</span>;
  <span class="hljs-keyword">const</span> c = <span class="hljs-number">30</span>;
}
<span class="hljs-built_in">console</span>.log(a); <span class="hljs-comment">// 10</span>
<span class="hljs-built_in">console</span>.log(b); <span class="hljs-comment">// Uncaught ReferenceError: b is not defined</span></code></pre><pre class="hljs"><code><span class="hljs-comment">* Reason?
    * In the BLOCK SCOPE;</span> we get b <span class="hljs-meta">and</span> c inside it initialized <span class="hljs-meta">as</span> <span class="hljs-comment">*undefined* as a part of hoisting (in a seperate memory space called **block**)
    * While, a is stored inside a GLOBAL scope.

    * Thus we say, *let* and *const* are BLOCK SCOPED. They are stored in a separate mem space which is reserved for this block. Also, they can&#x27;t be accessed outside this block. But var a can be accessed anywhere as it is in global scope. Thus, we can&#x27;t access them outside the Block.</span></code></pre><p>What is <strong>Shadowing</strong>?</p>
<pre class="hljs"><code><span class="hljs-keyword">var</span> a = <span class="hljs-number">100</span>;
{
  <span class="hljs-keyword">var</span> a = <span class="hljs-number">10</span>; <span class="hljs-comment">// same name as global var</span>
  <span class="hljs-keyword">let</span> b = <span class="hljs-number">20</span>;
  <span class="hljs-keyword">const</span> c = <span class="hljs-number">30</span>;
  <span class="hljs-built_in">console</span>.log(a); <span class="hljs-comment">// 10</span>
  <span class="hljs-built_in">console</span>.log(b); <span class="hljs-comment">// 20</span>
  <span class="hljs-built_in">console</span>.log(c); <span class="hljs-comment">// 30</span>
}
<span class="hljs-built_in">console</span>.log(a); <span class="hljs-comment">// 10, instead of the 100 we were expecting. So block &quot;a&quot; modified val of global &quot;a&quot; as well. In console, only b and c are in block space. a initially is in global space(a = 100), and when a = 10 line is run, a is not created in block space, but replaces 100 with 10 in global space itself.</span></code></pre><ul class="list">
<li><p>So, If one has same named variable outside the block, the variable inside the block <em>shadows</em> the outside variable. <strong>This happens only for var</strong></p>
</li>
<li><p>Let&#39;s observe the behaviour in case of let and const and understand it&#39;s reason.</p>
</li>
</ul>
<pre class="hljs"><code><span class="hljs-keyword">let</span> b = <span class="hljs-number">100</span>;
{
  <span class="hljs-keyword">var</span> a = <span class="hljs-number">10</span>;
  <span class="hljs-keyword">let</span> b = <span class="hljs-number">20</span>;
  <span class="hljs-keyword">const</span> c = <span class="hljs-number">30</span>;
  <span class="hljs-built_in">console</span>.log(b); <span class="hljs-comment">// 20</span>
}
<span class="hljs-built_in">console</span>.log(b); <span class="hljs-comment">// 100, Both b&#x27;s are in separate spaces (one in Block(20) and one in Script(another arbitrary mem space)(100)). Same is also true for *const* declarations.</span></code></pre><p class="img-container"><img src="../assets/scope.jpg" alt="Block Scope Explaination" title="Lexical Scope"></p>
<ul class="list">
<li>Same logic is true even for <strong>functions</strong></li>
</ul>
<pre class="hljs"><code><span class="hljs-keyword">const</span> c = <span class="hljs-number">100</span>;
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">x</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-keyword">const</span> c = <span class="hljs-number">10</span>;
  <span class="hljs-built_in">console</span>.log(c); <span class="hljs-comment">// 10</span>
}
x();
<span class="hljs-built_in">console</span>.log(c); <span class="hljs-comment">// 100</span></code></pre><p>What is <strong>Illegal Shadowing</strong>?</p>
<pre class="hljs"><code><span class="hljs-keyword">let</span> a = <span class="hljs-number">20</span>;
{
  <span class="hljs-keyword">var</span> a = <span class="hljs-number">20</span>;
}
<span class="hljs-comment">// Uncaught SyntaxError: Identifier &#x27;a&#x27; has already been declared</span></code></pre><ul class="list">
<li>We cannot shadow let with var. But it is <strong>valid</strong> to shadow a let using a let. However, we can shadow var with let.</li>
<li>All scope rules that work in function are same in arrow functions too.</li>
<li>Since var is function scoped, it is not a problem with the code below.</li>
</ul>
<pre class="hljs"><code><span class="hljs-keyword">let</span> a = <span class="hljs-number">20</span>;
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">x</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-keyword">var</span> a = <span class="hljs-number">20</span>;
}</code></pre><hr>

<br>

<hr>

<br>

<h1 id="episode-10--closures-in-js"><a class="header-link" href="#episode-10--closures-in-js"></a>Episode 10 : Closures in JS</h1>
<ul class="list">
<li><p>Function bundled along with it&#39;s lexical scope is <strong>closure</strong>.</p>
</li>
<li><p>JavaScript has a lexcial scope environment. If a function needs to access a variable, it first goes to its local memory. When it does not find it there, it goes to the memory of its lexical parent. See Below code, Over here function <strong>y</strong> along with its lexical scope i.e. (function x) would be called a closure.</p>
<pre class="prettyprint">function x() {
  var a = 7;
  function y() {
    console.log(a);
  }
  return y;
}
var z = x();
console.log(z); // value of z is entire code of function y.
</pre>
<ul class="list">
<li><p>In above code, When y is returned, not only is the function returned but the entire closure (fun y + its lexical scope) is returned and put inside z. So when z is used somewhere else in program, it still remembers var a inside x()</p>
</li>
<li><p>Another Example</p>
<pre class="prettyprint">function z() {
  var b = 900;
  function x() {
    var a = 7;
    function y() {
      console.log(a, b);
    }
    y();
  }
  x();
}
z(); // 7 900
</pre>
</li>
</ul>
</li>
<li><p>Thus In simple words, we can say:</p>
<ul class="list">
<li><strong>*A closure is a function</strong> that has access to its outer function scope even after the function has returned. Meaning, A closure can remember and access variables and arguments reference of its outer function even after the function has returned.*</li>
</ul>
</li>
</ul>
<br>

<ul class="list">
<li><p class="img-container"><img src="../assets/closure.jpg" alt="Closure Explaination" title="Lexical Scope"></p>
</li>
<li><p>Advantages of Closure:</p>
<p>  Certainly! Let&#39;s explore examples for each of the advantages you&#39;ve
  mentioned:</p>
<ol class="list">
<li><p><strong>Module Design Pattern</strong>:</p>
<ul class="list">
<li><p>The module design pattern allows us to encapsulate related
functionality into a single module or file. It helps organize
code, prevent global namespace pollution, and promotes
reusability.</p>
</li>
<li><p>Example: Suppose we&#39;re building a web application, and we want
to create a module for handling user authentication. We can
create a <code>auth.js</code> module that exports functions like <code>login</code>,
<code>logout</code>, and <code>getUserInfo</code>.</p>
<pre class="prettyprint">// auth.js
const authModule = (function () {
  let loggedInUser = null;

  function login(username, password) {
    // Authenticate user logic...
    loggedInUser = username;
  }

  function logout() {
    loggedInUser = null;
  }

  function getUserInfo() {
    return loggedInUser;
  }

  return {
    login,
    logout,
    getUserInfo,
  };
})();

// Usage
authModule.login(&#39;john_doe&#39;, &#39;secret&#39;);
console.log(authModule.getUserInfo()); // &#39;john_doe&#39;
</pre>
</li>
</ul>
</li>
<li><p><strong>Currying</strong>:</p>
<ul class="list">
<li><p>Currying is a technique where a function that takes multiple
arguments is transformed into a series of functions that take
one argument each. It enables partial function application and
enhances code flexibility.</p>
</li>
<li><p>Example: Let&#39;s create a curried function to calculate the total
price of items with tax.</p>
<pre class="prettyprint">const calculateTotalPrice = (taxRate) =&gt; (price) =&gt; price + price * (taxRate / 100);

const calculateSalesTax = calculateTotalPrice(8); // 8% sales tax
const totalPrice = calculateSalesTax(100); // Price with tax
console.log(totalPrice); // 108
</pre>
</li>
</ul>
</li>
<li><p><strong>Memoization</strong>:</p>
<ul class="list">
<li><p>Memoization optimizes expensive function calls by caching their
results. It&#39;s useful for recursive or repetitive computations.</p>
</li>
<li><p>Example: Implement a memoized Fibonacci function.</p>
<pre class="prettyprint">function fibonacci(n, memo = {}) {
  if (n in memo) return memo[n];
  if (n &lt;= 1) return n;

  memo[n] = fibonacci(n - 1, memo) + fibonacci(n - 2, memo);
  return memo[n];
}

console.log(fibonacci(10)); // 55
</pre>
</li>
</ul>
</li>
<li><p><strong>Data Hiding and Encapsulation</strong>:</p>
<ul class="list">
<li><p>Encapsulation hides the internal details of an object and
exposes only necessary methods and properties. It improves code
maintainability and security.</p>
</li>
<li><p>Example: Create a <code>Person</code> class with private properties.</p>
<pre class="prettyprint">class Person {
  #name; // Private field

  constructor(name) {
    this.#name = name;
  }

  getName() {
    return this.#name;
  }
}

const person = new Person(&#39;Alice&#39;);
console.log(person.getName()); // &#39;Alice&#39;
// console.log(person.#name); // Error: Private field &#39;#name&#39; must be declared in an enclosing class
</pre>
</li>
</ul>
</li>
<li><p><strong>setTimeouts</strong>:</p>
<ul class="list">
<li><p><code>setTimeout</code> allows scheduling a function to run after a
specified delay. It&#39;s commonly used for asynchronous tasks,
animations, and event handling.</p>
</li>
<li><p>Example: Delayed message display.</p>
<pre class="prettyprint">function showMessage(message, delay) {
  setTimeout(() =&gt; {
    console.log(message);
  }, delay);
}

showMessage(&#39;Hello, world!&#39;, 2000); // Display after 2 seconds
</pre>
</li>
</ul>
</li>
</ol>
<p>These examples demonstrate the power and versatility of closures in
JavaScript! 🚀</p>
</li>
<li><p>Disadvantages of Closure:</p>
<ul class="list">
<li>Over consumption of memory</li>
<li>Memory Leak</li>
<li>Freeze browser</li>
</ul>
</li>
</ul>
<hr>


<br>

<hr>

<br>

<h1 id="episode-11--settimeout--closures-interview-question"><a class="header-link" href="#episode-11--settimeout--closures-interview-question"></a>Episode 11 : setTimeout + Closures Interview Question</h1>
<blockquote>
<p><strong>Time, tide and Javascript wait for none.</strong></p>
</blockquote>
<pre class="hljs"><code><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">x</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-keyword">var</span> i = <span class="hljs-number">1</span>;
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{
    <span class="hljs-built_in">console</span>.log(i);
  }, <span class="hljs-number">3000</span>);
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;Namaste Javascript&quot;</span>);
}
x();
<span class="hljs-comment">// Output:</span>
<span class="hljs-comment">// Namaste Javascript</span>
<span class="hljs-comment">// 1 // after waiting 3 seconds</span></code></pre><ul class="list">
<li><p>We expect JS to wait 3 sec, print 1 and then go down and print the string. But JS prints string immediately, waits 3 sec and then prints 1.</p>
</li>
<li><p>The function inside setTimeout forms a closure (remembers reference to i). So wherever function goes it carries this ref along with it.</p>
</li>
<li><p>setTimeout takes this callback function &amp; attaches timer of 3000ms and stores it. Goes to next line without waiting and prints string.</p>
</li>
<li><p>After 3000ms runs out, JS takes function, puts it into call stack and runs it.</p>
</li>
<li><p>Q: Print 1 after 1 sec, 2 after 2 sec till 5 : Tricky interview question</p>
<p>We assume this has a simple approach as below</p>
<pre class="prettyprint">function x() {
  for (var i = 1; i &lt;= 5; i++) {
    setTimeout(function () {
      console.log(i);
    }, i * 1000);
  }
  console.log(&quot;Namaste Javascript&quot;);
}
x();
// Output:
// Namaste Javascript
// 6
// 6
// 6
// 6
// 6
</pre>
<ul class="list">
<li><p>Reason?</p>
<ul class="list">
<li><p>This happens because of closures. When setTimeout stores the function somewhere and attaches timer to it, the function remembers its reference to i, <strong>not value of i</strong>. All 5 copies of function point to same reference of i. JS stores these 5 functions, prints string and then comes back to the functions. By then the timer has run fully. And due to looping, the i value became 6. And when the callback fun runs the variable i = 6. So same 6 is printed in each log</p>
</li>
<li><p>To avoid this, we can use <strong>let</strong> instead of <strong>var</strong> as let has Block scope. For each iteration, the i is a new variable altogether(new copy of i). Everytime setTimeout is run, the inside function forms closure with new variable i</p>
</li>
</ul>
</li>
<li><p>But what if interviewer ask us to implement using <strong>var</strong>?</p>
<pre class="prettyprint">function x() {
  for (var i = 1; i &lt;= 5; i++) {
    function close(i) {
      setTimeout(function () {
        console.log(i);
      }, i * 1000);
      // put the setT function inside new function close()
    }
    close(i); // everytime you call close(i) it creates new copy of i. Only this time, it is with var itself!
  }
  console.log(&quot;Namaste Javascript&quot;);
}
x();
</pre>
</li>
</ul>
</li>
</ul>
<hr>

<br>

<hr>

<br>

<h1 id="episode-12--famous-interview-questions-ft-closures"><a class="header-link" href="#episode-12--famous-interview-questions-ft-closures"></a>Episode 12 : Famous Interview Questions ft. Closures</h1>
<h3 id="q1-what-is-closure-in-javascript"><a class="header-link" href="#q1-what-is-closure-in-javascript"></a>Q1: What is Closure in Javascript?</h3>
<p><strong>Ans</strong>: A function along with reference to its outer environment together forms a closure. Or in other words, A Closure is a combination of a function and its lexical scope bundled together.
eg:</p>
<pre class="hljs"><code><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">outer</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-keyword">var</span> a = <span class="hljs-number">10</span>;
  <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">inner</span>(<span class="hljs-params"></span>) </span>{
    <span class="hljs-built_in">console</span>.log(a);
  } <span class="hljs-comment">// inner forms a closure with outer</span>
  <span class="hljs-keyword">return</span> inner;
}
outer()(); <span class="hljs-comment">// 10 // over here first `()` will return inner function and then using second `()` to call inner function</span></code></pre><h3 id="q2-will-the-below-code-still-forms-a-closure"><a class="header-link" href="#q2-will-the-below-code-still-forms-a-closure"></a>Q2: Will the below code still forms a closure?</h3>
<pre class="hljs"><code><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">outer</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">inner</span>(<span class="hljs-params"></span>) </span>{
    <span class="hljs-built_in">console</span>.log(a);
  }
  <span class="hljs-keyword">var</span> a = <span class="hljs-number">10</span>;
  <span class="hljs-keyword">return</span> inner;
}
outer()(); <span class="hljs-comment">// 10</span></code></pre><p><strong>Ans</strong>: Yes, because inner function forms a closure with its outer environment so sequence doesn&#39;t matter.</p>
<h3 id="q3-changing-var-to-let-will-it-make-any-difference"><a class="header-link" href="#q3-changing-var-to-let-will-it-make-any-difference"></a>Q3: Changing var to let, will it make any difference?</h3>
<pre class="hljs"><code><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">outer</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-keyword">let</span> a = <span class="hljs-number">10</span>;
  <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">inner</span>(<span class="hljs-params"></span>) </span>{
    <span class="hljs-built_in">console</span>.log(a);
  }
  <span class="hljs-keyword">return</span> inner;
}
outer()(); <span class="hljs-comment">// 10</span></code></pre><p><strong>Ans</strong>: It will still behave the same way.</p>
<h3 id="q4-will-inner-function-have-the-access-to-outer-function-argument"><a class="header-link" href="#q4-will-inner-function-have-the-access-to-outer-function-argument"></a>Q4: Will inner function have the access to outer function argument?</h3>
<pre class="hljs"><code><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">outer</span>(<span class="hljs-params">str</span>) </span>{
  <span class="hljs-keyword">let</span> a = <span class="hljs-number">10</span>;
  <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">inner</span>(<span class="hljs-params"></span>) </span>{
    <span class="hljs-built_in">console</span>.log(a, str);
  }
  <span class="hljs-keyword">return</span> inner;
}
outer(<span class="hljs-string">&quot;Hello There&quot;</span>)(); <span class="hljs-comment">// 10 &quot;Hello There&quot;</span></code></pre><p><strong>Ans</strong>: Inner function will now form closure and will have access to both a and str.</p>
<h3 id="q5-in-below-code-will-inner-form-closure-with-outest"><a class="header-link" href="#q5-in-below-code-will-inner-form-closure-with-outest"></a>Q5: In below code, will inner form closure with <strong>outest</strong>?</h3>
<pre class="hljs"><code><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">outest</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-keyword">var</span> c = <span class="hljs-number">20</span>;
  <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">outer</span>(<span class="hljs-params">str</span>) </span>{
    <span class="hljs-keyword">let</span> a = <span class="hljs-number">10</span>;
    <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">inner</span>(<span class="hljs-params"></span>) </span>{
      <span class="hljs-built_in">console</span>.log(a, c, str);
    }
    <span class="hljs-keyword">return</span> inner;
  }
  <span class="hljs-keyword">return</span> outer;
}
outest()(<span class="hljs-string">&quot;Hello There&quot;</span>)(); <span class="hljs-comment">// 10 20 &quot;Hello There&quot;</span></code></pre><p><strong>Ans</strong>: Yes, inner will have access to all its outer environment.</p>
<h3 id="q6-output-of-below-code-and-explaination"><a class="header-link" href="#q6-output-of-below-code-and-explaination"></a>Q6: Output of below code and explaination?</h3>
<pre class="hljs"><code><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">outest</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-keyword">var</span> c = <span class="hljs-number">20</span>;
  <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">outer</span>(<span class="hljs-params">str</span>) </span>{
    <span class="hljs-keyword">let</span> a = <span class="hljs-number">10</span>;
    <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">inner</span>(<span class="hljs-params"></span>) </span>{
      <span class="hljs-built_in">console</span>.log(a, c, str);
    }
    <span class="hljs-keyword">return</span> inner;
  }
  <span class="hljs-keyword">return</span> outer;
}
<span class="hljs-keyword">let</span> a = <span class="hljs-number">100</span>;
outest()(<span class="hljs-string">&quot;Hello There&quot;</span>)(); <span class="hljs-comment">// 10 20 &quot;Hello There&quot;</span></code></pre><p><strong>Ans</strong>: Still the same output, the inner function will have reference to inner a, so conflicting name won&#39;t matter here. If it wouldn&#39;t have find a inside outer function then it would have went more outer to find a and thus have printed 100. So, it try to resolve variable in scope chain and if a wouldn&#39;t have been found it would have given reference error.</p>
<h3 id="q7-advantage-of-closure"><a class="header-link" href="#q7-advantage-of-closure"></a>Q7: Advantage of Closure?</h3>
<ul class="list">
<li>Module Design Pattern</li>
<li>Currying</li>
<li>Memoize</li>
<li>Data hiding and encapsulation</li>
<li>setTimeouts etc.</li>
</ul>
<h3 id="q8-discuss-more-on-data-hiding-and-encapsulation"><a class="header-link" href="#q8-discuss-more-on-data-hiding-and-encapsulation"></a>Q8: Discuss more on Data hiding and encapsulation?</h3>
<pre class="hljs"><code><span class="hljs-comment">// without closures</span>
<span class="hljs-keyword">var</span> count = <span class="hljs-number">0</span>;
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">increment</span>(<span class="hljs-params"></span>)</span>{
  count++;
}
<span class="hljs-comment">// in the above code, anyone can access count and change it.</span>

------------------------------------------------------------------

<span class="hljs-comment">// (with closures) -&gt; put everything into a function</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">counter</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-keyword">var</span> count = <span class="hljs-number">0</span>;
  <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">increment</span>(<span class="hljs-params"></span>)</span>{
    count++;
  }
}
<span class="hljs-built_in">console</span>.log(count); <span class="hljs-comment">// this will give referenceError as count can&#x27;t be accessed. So now we are able to achieve hiding of data</span>

------------------------------------------------------------------

<span class="hljs-comment">//(increment with function using closure) true function</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">counter</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-keyword">var</span> count = <span class="hljs-number">0</span>;
  <span class="hljs-keyword">return</span> <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">increment</span>(<span class="hljs-params"></span>)</span>{
    count++;
    <span class="hljs-built_in">console</span>.log(count);
  }
}
<span class="hljs-keyword">var</span> counter1 = counter(); <span class="hljs-comment">//counter function has closure with count var.</span>
counter1(); <span class="hljs-comment">// increments counter</span>

<span class="hljs-keyword">var</span> counter2 = counter();
counter2(); <span class="hljs-comment">// here counter2 is whole new copy of counter function and it wont impack the output of counter1</span>

*************************

<span class="hljs-comment">// Above code is not good and scalable for say, when you plan to implement decrement counter at a later stage.</span>
<span class="hljs-comment">// To address this issue, we use *constructors*</span>

<span class="hljs-comment">// Adding decrement counter and refactoring code:</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">Counter</span>(<span class="hljs-params"></span>) </span>{
<span class="hljs-comment">//constructor function. Good coding would be to capitalize first letter of constructor function.</span>
  <span class="hljs-keyword">var</span> count = <span class="hljs-number">0</span>;
  <span class="hljs-built_in">this</span>.incrementCounter = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>{ <span class="hljs-comment">//anonymous function</span>
    count++;
    <span class="hljs-built_in">console</span>.log(count);
  }
   <span class="hljs-built_in">this</span>.decrementCounter = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>{
    count--;
    <span class="hljs-built_in">console</span>.log(count);
  }
}

<span class="hljs-keyword">var</span> counter1 = <span class="hljs-keyword">new</span> Counter();  <span class="hljs-comment">// new keyword for constructor fun</span>
counter1.incrementCounter();
counter1.incrementCounter();
counter1.decrementCounter();
<span class="hljs-comment">// returns 1 2 1</span></code></pre><h3 id="q9-disadvantage-of-closure"><a class="header-link" href="#q9-disadvantage-of-closure"></a>Q9: Disadvantage of closure?</h3>
<p><strong>Ans</strong>: Overconsumption of memory when using closure as everytime as those closed over variables are not garbage collected till program expires.
So when creating many closures, more memory is accumulated and this can create memory leaks if not handled.</p>
<p><strong>Garbage collector</strong> : Program in JS engine or browser that frees up unused memory. In highlevel languages like C++ or JAVA, garbage collection is left to the programmer, but in JS engine its done implicitly.</p>
<pre class="hljs"><code><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">a</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-keyword">var</span> x = <span class="hljs-number">0</span>;
  <span class="hljs-keyword">return</span> <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">b</span>(<span class="hljs-params"></span>) </span>{
    <span class="hljs-built_in">console</span>.log(x);
  };
}

<span class="hljs-keyword">var</span> y = a(); <span class="hljs-comment">// y is a copy of b()</span>
y();

<span class="hljs-comment">// Once a() is called, its element x should be garbage collected ideally. But fun b has closure over var x. So mem of x cannot be freed. Like this if more closures formed, it becomes an issue. To tacke this, JS engines like v8 and Chrome have smart garbage collection mechanisms. Say we have var x = 0, z = 10 in above code. When console log happens, x is printed as 0 but z is removed automatically.</span></code></pre><hr>

<br>

<hr>

<br>

<h1 id="episode-13--first-class-functions-ft-anonymous-functions"><a class="header-link" href="#episode-13--first-class-functions-ft-anonymous-functions"></a>Episode 13 : First Class Functions ft. Anonymous Functions</h1>
<blockquote>
<p>Functions are heart ♥ of Javascript.</p>
</blockquote>
<h3 id="q-what-is-function-statement"><a class="header-link" href="#q-what-is-function-statement"></a>Q: What is Function statement?</h3>
<p>Below way of creating function are function statement.</p>
<pre class="hljs"><code><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">a</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;Hello&quot;</span>);
}
a(); <span class="hljs-comment">// Hello</span></code></pre><h3 id="q-what-is-function-expression"><a class="header-link" href="#q-what-is-function-expression"></a>Q: What is Function Expression?</h3>
<p>Assigning a function to a variable. Function acts like a value.</p>
<pre class="hljs"><code><span class="hljs-keyword">var</span> b = <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;Hello&quot;</span>);
};
b();</code></pre><h3 id="q-difference-between-function-statement-and-expression"><a class="header-link" href="#q-difference-between-function-statement-and-expression"></a>Q: Difference between function statement and expression</h3>
<p>The major difference between these two lies in <strong>Hoisting</strong>.</p>
<pre class="hljs"><code>a(); <span class="hljs-comment">// &quot;Hello A&quot;</span>
b(); <span class="hljs-comment">// TypeError</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">a</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;Hello A&quot;</span>);
}
<span class="hljs-keyword">var</span> b = <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;Hello B&quot;</span>);
};
<span class="hljs-comment">// Why? During mem creation phase a is created in memory and function assigned to a. But b is created like a variable (b:undefined) and until code reaches the function()  part, it is still undefined. So it cannot be called.</span></code></pre><h3 id="q-what-is-function-declaration"><a class="header-link" href="#q-what-is-function-declaration"></a>Q: What is Function Declaration?</h3>
<p>Other name for <strong>function statement</strong>.</p>
<h3 id="q-what-is-anonymous-function"><a class="header-link" href="#q-what-is-anonymous-function"></a>Q: What is Anonymous Function?</h3>
<p>A function without a name.</p>
<pre class="hljs"><code><span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{

}<span class="hljs-comment">// this is going to throw Syntax Error - Function Statement requires function name.</span></code></pre><ul class="list">
<li>They don&#39;t have their own identity. So an anonymous function without code inside it results in an error.</li>
<li>Anonymous functions are used when functions are used as values eg. the code sample for <strong>function expression</strong> above.</li>
</ul>
<h3 id="q-what-is-named-function-expression"><a class="header-link" href="#q-what-is-named-function-expression"></a>Q: What is Named Function Expression?</h3>
<p>Same as Function Expression but function has a name instead of being anonymous.</p>
<pre class="hljs"><code><span class="hljs-keyword">var</span> b = <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">xyz</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;b called&quot;</span>);
};
b(); <span class="hljs-comment">// &quot;b called&quot;</span>
xyz(); <span class="hljs-comment">// Throws ReferenceError:xyz is not defined.</span>
<span class="hljs-comment">// xyz function is not created in global scope. So it can&#x27;t be called.</span></code></pre><h3 id="q-parameters-vs-arguments"><a class="header-link" href="#q-parameters-vs-arguments"></a>Q: Parameters vs Arguments?</h3>
<pre class="hljs"><code><span class="hljs-keyword">var</span> b = <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">param1, param2</span>) </span>{
  <span class="hljs-comment">// labels/identifiers are parameters</span>
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;b called&quot;</span>);
};
b(arg1, arg2); <span class="hljs-comment">// arguments - values passed inside function call</span></code></pre><h3 id="q-what-is-first-class-function-aka-first-class-citizens"><a class="header-link" href="#q-what-is-first-class-function-aka-first-class-citizens"></a>Q: What is First Class Function aka First Class Citizens?</h3>
<p>We can pass functions inside a function as arguments and
/or return a function(HOF). These ability are altogether known as First class function. It is programming concept available in some other languages too.</p>
<pre class="hljs"><code><span class="hljs-keyword">var</span> b = <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">param1</span>) </span>{
  <span class="hljs-built_in">console</span>.log(param1); <span class="hljs-comment">// prints &quot; f() {} &quot;</span>
};
b(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{});

<span class="hljs-comment">// Other way of doing the same thing:</span>
<span class="hljs-keyword">var</span> b = <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">param1</span>) </span>{
  <span class="hljs-built_in">console</span>.log(param1);
};
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">xyz</span>(<span class="hljs-params"></span>) </span>{}
b(xyz); <span class="hljs-comment">// same thing as prev code</span>

<span class="hljs-comment">// we can return a function from a function:</span>
<span class="hljs-keyword">var</span> b = <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">param1</span>) </span>{
  <span class="hljs-keyword">return</span> <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{};
};
<span class="hljs-built_in">console</span>.log(b()); <span class="hljs-comment">//we log the entire fun within b.</span></code></pre><hr>

<br>

<hr>

<br>

<h1 id="episode-14--callback-functions-in-js-ft-event-listeners"><a class="header-link" href="#episode-14--callback-functions-in-js-ft-event-listeners"></a>Episode 14 : Callback Functions in JS ft. Event Listeners</h1>
<h3 id="callback-functions"><a class="header-link" href="#callback-functions"></a>Callback Functions</h3>
<ul class="list">
<li>Functions are first class citizens ie. take a function A and pass it to another function B. Here, A is a callback function. So basically I am giving access to function B to call function A. This callback function gives us the access to whole <strong>Asynchronous</strong> world in <strong>Synchronous</strong> world.</li>
</ul>
<pre class="hljs"><code><span class="hljs-built_in">setTimeout</span>(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;Timer&quot;</span>);
}, <span class="hljs-number">1000</span>); <span class="hljs-comment">// first argument is callback function and second is timer.</span></code></pre><ul class="list">
<li>JS is a synchronous and single threaded language. But due to callbacks, we can do async things in JS.</li>
</ul>
<pre class="hljs"><code><span class="hljs-built_in">setTimeout</span>(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;timer&quot;</span>);
}, <span class="hljs-number">5000</span>);
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">x</span>(<span class="hljs-params">y</span>) </span>{
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;x&quot;</span>);
  y();
}
x(<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">y</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;y&quot;</span>);
});
<span class="hljs-comment">// x y timer</span></code></pre><ul class="list">
<li>In the call stack, first x and y are present. After code execution, they go away and stack is empty. Then after 5 seconds (from beginning) anonymous suddenly appear up in stack ie. setTimeout</li>
<li>All 3 functions are executed through call stack. If any operation blocks the call stack, its called blocking the main thread.</li>
<li>Say if x() takes 30 sec to run, then JS has to wait for it to finish as it has only 1 call stack/1 main thread. Never block main thread.</li>
<li>Always use <strong>async</strong> for functions that take time eg. setTimeout</li>
</ul>
<pre class="hljs"><code><span class="hljs-comment">// Another Example of callback</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">printStr</span>(<span class="hljs-params">str, cb</span>) </span>{
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    <span class="hljs-built_in">console</span>.log(str);
    cb();
  }, <span class="hljs-built_in">Math</span>.floor(<span class="hljs-built_in">Math</span>.random() * <span class="hljs-number">100</span>) + <span class="hljs-number">1</span>);
}
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">printAll</span>(<span class="hljs-params"></span>) </span>{
  printStr(<span class="hljs-string">&quot;A&quot;</span>, <span class="hljs-function">() =&gt;</span> {
    printStr(<span class="hljs-string">&quot;B&quot;</span>, <span class="hljs-function">() =&gt;</span> {
      printStr(<span class="hljs-string">&quot;C&quot;</span>, <span class="hljs-function">() =&gt;</span> {});
    });
  });
}
printAll(); <span class="hljs-comment">// A B C // in order</span></code></pre><h3 id="event-listener"><a class="header-link" href="#event-listener"></a>Event Listener</h3>
<ul class="list">
<li>We will create a button in html and attach event to it.</li>
</ul>
<pre class="hljs"><code><span class="hljs-comment">// index.html</span>
&lt;button id=<span class="hljs-string">&quot;clickMe&quot;</span>&gt;Click Me!&lt;/button&gt;;

<span class="hljs-comment">// in index.js</span>
<span class="hljs-built_in">document</span>.getElementById(<span class="hljs-string">&quot;clickMe&quot;</span>).addEventListener(<span class="hljs-string">&quot;click&quot;</span>, <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">xyz</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-comment">//when event click occurs, this callback function (xyz) is called into callstack</span>
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;Button clicked&quot;</span>);
});</code></pre><ul class="list">
<li>Lets implement a increment counter button.<ul class="list">
<li>Using global variable (not good as anyone can change it)<pre class="prettyprint">let count = 0;
document
  .getElementById(&quot;clickMe&quot;)
  .addEventListener(&quot;click&quot;, function xyz() {
    console.log(&quot;Button clicked&quot;, ++count);
  });
</pre>
</li>
<li>Use closures for data abstraction<pre class="prettyprint">function attachEventList() {
  //creating new function for closure
  let count = 0;
  document
    .getElementById(&quot;clickMe&quot;)
    .addEventListener(&quot;click&quot;, function xyz() {
      console.log(&quot;Button clicked&quot;, ++count); //now callback function forms closure with outer scope(count)
    });
}
attachEventList();
</pre>
<img src="../assets/event.jpg" alt="Event Listerner Demo"></li>
</ul>
</li>
</ul>
<h3 id="garbage-collection-and-removeeventlisteners"><a class="header-link" href="#garbage-collection-and-removeeventlisteners"></a>Garbage Collection and removeEventListeners</h3>
<ul class="list">
<li>Event listeners are heavy as they form closures. So even when call stack is empty, EventListener won&#39;t free up memory allocated to count as it doesn&#39;t know when it may need count again. So we remove event listeners when we don&#39;t need them (garbage collected) onClick, onHover, onScroll all in a page can slow it down heavily.</li>
</ul>
<hr>

<br>

<hr>

<br>

<h1 id="episode-15--asynchronous-javascript--event-loop-from-scratch"><a class="header-link" href="#episode-15--asynchronous-javascript--event-loop-from-scratch"></a>Episode 15 : Asynchronous JavaScript &amp; EVENT LOOP from scratch</h1>
<blockquote>
<p>Note: Call stack will execeute any execeution context which enters it. Time, tide and JS waits for none. TLDR; Call stack has no timer.</p>
</blockquote>
<ul class="list">
<li>Browser has JS Engine which has Call Stack which has Global execution context, local execution context etc.<ul class="list">
<li>But browser has many other superpowers - Local storage space, Timer, place to enter URL, Bluetooth access, Geolocation access and so on.</li>
<li>Now JS needs some way to connect the callstack with all these superpowers. This is done using Web APIs.
<img src="../assets/eventloop1.jpg" alt="Event Loop 1 Demo"></li>
</ul>
</li>
</ul>
<h3 id="webapis"><a class="header-link" href="#webapis"></a>WebAPIs</h3>
<p>None of the below are part of Javascript! These are extra superpowers that browser has. Browser gives access to JS callstack to use these powers.
<img src="../assets/eventloop2.jpg" alt="Event Loop 2 Demo"></p>
<ul class="list">
<li><p>setTimeout(), DOM APIs, fetch(), localstorage, console (yes, even console.log is not JS!!), location and so many more.</p>
<ul class="list">
<li>setTimeout() : Timer function</li>
<li>DOM APIs : eg.Document.xxxx ; Used to access HTML DOM tree. (Document Object Manipulation)</li>
<li>fetch() : Used to make connection with external servers eg. Netflix servers etc.</li>
</ul>
</li>
<li><p>We get all these inside call stack through global object ie. window</p>
<ul class="list">
<li>Use window keyword like : window.setTimeout(), window.localstorage, window.console.log() to log something inside console.</li>
<li>As window is global obj, and all the above functions are present in global object, we don&#39;t explicity write window but it is implied.</li>
</ul>
</li>
<li><p>Let&#39;s undertand the below code image and its explaination:
<img src="../assets/eventloop3.jpg" alt="Event Loop 3 Demo"></p>
<ul class="list">
<li><pre class="prettyprint">console.log(&quot;start&quot;);
setTimeout(function cb() {
  console.log(&quot;timer&quot;);
}, 5000);
console.log(&quot;end&quot;);
// start end timer
</pre>
</li>
<li>First a GEC is created and put inside call stack.</li>
<li>console.log(&quot;Start&quot;); // this calls the console web api (through window) which in turn actually modifies values in console.</li>
<li>setTimeout(function cb() { //this calls the setTimeout web api which gives access to timer feature. It stores the callback cb() and starts timer. console.log(&quot;Callback&quot;);}, 5000);</li>
<li>console.log(&quot;End&quot;); // calls console api and logs in console window. After this GEC pops from call stack.</li>
<li>While all this is happening, the timer is constantly ticking. After it becomes 0, the callback cb() has to run.</li>
<li>Now we need this cb to go into call stack. Only then will it be executed. For this we need <strong>event loop</strong> and <strong>Callback queue</strong></li>
</ul>
</li>
</ul>
<h3 id="event-loops-and-callback-queue"><a class="header-link" href="#event-loops-and-callback-queue"></a>Event Loops and Callback Queue</h3>
<p>Q: How after 5 secs timer is console?</p>
<ul class="list">
<li>cb() cannot simply directly go to callstack to be execeuted. It goes through the callback queue when timer expires.</li>
<li>Event loop keep checking the callback queue, and see if it has any element to puts it into call stack. It is like a gate keeper.</li>
<li>Once cb() is in callback queue, eventloop pushes it to callstack to run. Console API is used and log printed</li>
<li><img src="../assets/eventloop4.jpg" alt="Event Loop 4 Demo"></li>
</ul>
<p>Q: Another example to understand Eventloop &amp; Callback Queue.</p>
<p>See the below Image and code and try to understand the reason:
<img src="../assets/eventloop5.jpg" alt="Event Loop 5 Demo">
Explaination?</p>
<ul class="list">
<li><pre class="prettyprint">console.log(&quot;Start&quot;);
document.getElementById(&quot;btn&quot;).addEventListener(&quot;click&quot;, function cb() {
  // cb() registered inside webapi environment and event(click) attached to it. i.e. REGISTERING CALLBACK AND ATTACHING EVENT TO IT.
  console.log(&quot;Callback&quot;);
});
console.log(&quot;End&quot;); // calls console api and logs in console window. After this GEC get removed from call stack.
// In above code, even after console prints &quot;Start&quot; and &quot;End&quot; and pops GEC out, the eventListener stays in webapi env(with hope that user may click it some day) until explicitly removed, or the browser is closed.
</pre>
</li>
<li><p>Eventloop has just one job to keep checking callback queue and if found something push it to call stack and delete from callback queue.</p>
</li>
</ul>
<p>Q: Need of callback queue?</p>
<p><strong>Ans</strong>: Suppose user clciks button x6 times. So 6 cb() are put inside callback queue. Event loop sees if call stack is empty/has space and whether callback queue is not empty(6 elements here). Elements of callback queue popped off, put in callstack, executed and then popped off from call stack.</p>
<br>

<h3 id="behaviour-of-fetch-microtask-queue"><a class="header-link" href="#behaviour-of-fetch-microtask-queue"></a>Behaviour of fetch (<strong>Microtask Queue?</strong>)</h3>
<p>Let&#39;s observe the code below and try to understand</p>
<pre class="hljs"><code><span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;Start&quot;</span>); <span class="hljs-comment">// this calls the console web api (through window) which in turn actually modifies values in console.</span>
<span class="hljs-built_in">setTimeout</span>(<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">cbT</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;CB Timeout&quot;</span>);
}, <span class="hljs-number">5000</span>);
fetch(<span class="hljs-string">&quot;https://api.netflix.com&quot;</span>).then(<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">cbF</span>(<span class="hljs-params"></span>) </span>{
    <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;CB Netflix&quot;</span>);
}); <span class="hljs-comment">// take 2 seconds to bring response</span>
<span class="hljs-comment">// millions lines of code</span>
<span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;End&quot;</span>);

Code Explaination:
* Same steps <span class="hljs-keyword">for</span> everything before fetch() <span class="hljs-keyword">in</span> above code.
* fetch registers cbF into webapi environment along <span class="hljs-keyword">with</span> existing cbT.
* cbT is waiting <span class="hljs-keyword">for</span> 5000ms to end so that it can be put inside callback queue. cbF is waiting <span class="hljs-keyword">for</span> data to be returned <span class="hljs-keyword">from</span> Netflix servers gonna take <span class="hljs-number">2</span> seconds.
* After <span class="hljs-built_in">this</span> millions <span class="hljs-keyword">of</span> lines <span class="hljs-keyword">of</span> code is running, by the time millions line <span class="hljs-keyword">of</span> code will execute, <span class="hljs-number">5</span> seconds has finished and now the timer has expired and response <span class="hljs-keyword">from</span> Netflix server is ready.
* Data back <span class="hljs-keyword">from</span> cbF ready to be executed gets stored into something called a Microtask Queue.
* Also after expiration <span class="hljs-keyword">of</span> timer, cbT is ready to execute <span class="hljs-keyword">in</span> Callback Queue.
* Microtask Queue is exactly same <span class="hljs-keyword">as</span> Callback Queue, but it has higher priority. Functions <span class="hljs-keyword">in</span> Microtask Queue are executed earlier than Callback Queue.
* In <span class="hljs-built_in">console</span>, first Start and End are printed <span class="hljs-keyword">in</span> <span class="hljs-built_in">console</span>. First cbF goes <span class="hljs-keyword">in</span> callstack and <span class="hljs-string">&quot;CB Netflix&quot;</span> is printed. cbF popped <span class="hljs-keyword">from</span> callstack. Next cbT is removed <span class="hljs-keyword">from</span> callback Queue, put <span class="hljs-keyword">in</span> Call Stack, <span class="hljs-string">&quot;CB Timeout&quot;</span> is printed, and cbT removed <span class="hljs-keyword">from</span> callstack.
* See below Image <span class="hljs-keyword">for</span> more understanding</code></pre><p><img src="../assets/eventloop6.jpg" alt="Event Loop 6 Demo">
Microtask Priority Visualization
<img src="../assets/microtask.gif" alt="Event Loop 7 Demo"></p>
<h4 id="what-enters-the-microtask-queue-"><a class="header-link" href="#what-enters-the-microtask-queue-"></a>What enters the Microtask Queue ?</h4>
<ul class="list">
<li>All the callback functions that come through promises go in microtask Queue.</li>
<li><strong>Mutation Observer</strong> : Keeps on checking whether there is mutation in DOM tree or not, and if there, then it execeutes some callback function.</li>
<li>Callback functions that come through promises and mutation observer go inside <strong>Microtask Queue</strong>.</li>
<li>All the rest goes inside <strong>Callback Queue aka. Task Queue</strong>.</li>
<li>If the task in microtask Queue keeps creating new tasks in the queue, element in callback queue never gets chance to be run. This is called <strong>starvation</strong></li>
</ul>
<h3 id="some-important-questions"><a class="header-link" href="#some-important-questions"></a>Some Important Questions</h3>
<ol class="list">
<li><p><strong>When does the event loop actually start ? -</strong> Event loop, as the name suggests, is a single-thread, loop that is <em>almost infinite</em>. It&#39;s always running and doing its job.</p>
</li>
<li><p><strong>Are only asynchronous web api callbacks are registered in web api environment? -</strong> YES, the synchronous callback functions like what we pass inside map, filter and reduce aren&#39;t registered in the Web API environment. It&#39;s just those async callback functions which go through all this.</p>
</li>
<li><p><strong>Does the web API environment stores only the callback function and pushes the same callback to queue/microtask queue? -</strong> Yes, the callback functions are stored, and a reference is scheduled in the queues. Moreover, in the case of event listeners(for example click handlers), the original callbacks stay in the web API environment forever, that&#39;s why it&#39;s adviced to explicitly remove the listeners when not in use so that the garbage collector does its job.</p>
</li>
<li><p><strong>How does it matter if we delay for setTimeout would be 0ms. Then callback will move to queue without any wait ? -</strong> No, there are trust issues with setTimeout() 😅. The callback function needs to wait until the Call Stack is empty. So the 0 ms callback might have to wait for 100ms also if the stack is busy.</p>
</li>
</ol>
<br>

<h3 id="observation-of-eventloop-callback-queue--microtask-queue-gif"><a class="header-link" href="#observation-of-eventloop-callback-queue--microtask-queue-gif"></a>Observation of Eventloop, Callback Queue &amp; Microtask Queue [<strong>GiF</strong>]</h3>
<p><img src="../assets/microtask1.gif" alt="microtask 1 Demo">
<img src="../assets/microtask2.gif" alt="microtask 2 Demo">
<img src="../assets/microtask3.gif" alt="microtask 3 Demo">
<img src="../assets/microtask4.gif" alt="microtask 4 Demo">
<img src="../assets/microtask5.gif" alt="microtask 5 Demo">
<img src="../assets/microtask6.gif" alt="microtask 6 Demo"></p>
<hr>

<br>

<hr>

<br>

<h1 id="episode-16--js-engine-exposed-googles-v8-architecture"><a class="header-link" href="#episode-16--js-engine-exposed-googles-v8-architecture"></a>Episode 16 : JS Engine Exposed, Google&#39;s V8 Architecture</h1>
<ul class="list">
<li><p>JS runs literally everywhere from smart watch to robots to browsers because of Javascript Runtime Environment (JRE).</p>
</li>
<li><p>JRE is like a big container which has everything which are required to run Javascript code.</p>
</li>
<li><p>JRE consists of a JS Engine (❤️ of JRE), set of APIs to connect with outside environment, event loop, Callback queue, Microtask queue etc.</p>
</li>
<li><p>Browser can execute javascript code because it has the Javascript Runtime Environment.</p>
</li>
<li><p>ECMAScript is a governing body of JS. It has set of rules which are followed by all JS engines like Chakra(Edge), Spidermonkey(Firefox)(first javascript engine created by JS creator himself), v8(Chrome)</p>
</li>
<li><p>Javascript Engine is not a machine. Its software written in low level languages (eg. C++) that takes in hi-level code in JS and spits out low level machine code.</p>
</li>
<li><p>Code inside Javascript Engine passes through 3 steps : <strong>Parsing</strong>, <strong>Compilation</strong> and <strong>Execution</strong></p>
<ol class="list">
<li><strong>Parsing</strong> - Code is broken down into tokens. In &quot;let a = 7&quot; -&gt; let, a, =, 7 are all tokens. Also we have a syntax parser that takes code and converts it into an AST (Abstract Syntax Tree) which is a JSON with all key values like type, start, end, body etc (looks like package.json but for a line of code in JS. Kinda unimportant)(Check out astexplorer.net -&gt; converts line of code into AST).</li>
<li><strong>Compilation</strong> - JS has something called Just-in-time(JIT) Compilation - uses both interpreter &amp; compiler. Also compilation and execution both go hand in hand. The AST from previous step goes to interpreter which converts hi-level code to byte code and moves to execeution. While interpreting, compiler also works hand in hand to compile and form optimized code during runtime. <strong>Does JavaScript really Compiles?</strong> The answer is a loud <strong>YES</strong>. More info at: <a href="https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/get-started/ch1.md#whats-in-an-interpretation">Link 1</a>, <a href="https://web.stanford.edu/class/cs98si/slides/overview.html">Link 2</a>, <a href="https://blog.greenroots.info/javascript-interpreted-or-compiled-the-debate-is-over-ckb092cv302mtl6s17t14hq1j">Link 3</a>. JS used to be only interpreter in old times, but now has both to compile and interpreter code and this make JS a JIT compiled language, its like best of both world.</li>
<li><strong>Execution</strong> - Needs 2 components ie. Memory heap(place where all memory is stored) and Call Stack(same call stack from prev episodes). There is also a garbage collector. It uses an algo called <strong>Mark and Sweep</strong>.
<img src="../assets/jsengine.jpg" alt="JS Engine Demo">
GiF Demo
<img src="../assets/jsenginegif.gif" alt="JS Engine Demo"></li>
</ol>
</li>
<li><p>Companies use different JS engines and each try to make theirs the best.</p>
<ul class="list">
<li>v8 of Google has Interpreter called Ignition, a compiler called Turbo Fan and garbage collector called Orinoco</li>
<li>v8 architecture:
<img src="../assets/jsengine.png" alt="JS Engine Demo"></li>
</ul>
</li>
</ul>
<hr>

<br>

<hr>

<br>

<h1 id="episode-17--trust-issues-with-settimeout"><a class="header-link" href="#episode-17--trust-issues-with-settimeout"></a>Episode 17 : Trust issues with setTimeout()</h1>
<ul class="list">
<li><p>setTimeout with timer of 5 secs sometimes does not exactly guarantees that the callback function will execute exactly after 5s.</p>
</li>
<li><p>Let&#39;s observe the below code and it&#39;s explaination</p>
<pre class="prettyprint">console.log(&quot;Start&quot;);
setTimeout(function cb() {
  console.log(&quot;Callback&quot;);
}, 5000);
console.log(&quot;End&quot;);
// Millions of lines of code to execute

// o/p: Over here setTimeout exactly doesn&#39;t guarantee that the callback function will be called exactly after 5s. Maybe 6,7 or even 10! It all depends on callstack. Why?
</pre>
<p>Reason?</p>
<ul class="list">
<li>First GEC is created and pushed in callstack.</li>
<li>Start is printed in console</li>
<li>When setTimeout is seen, callback function is registered into webapi&#39;s env. And timer is attached to it and started. callback waits for its turn to be execeuted once timer expires. But JS waits for none. Goes to next line.</li>
<li>End is printed in console.</li>
<li>After &quot;End&quot;, we have 1 million lines of code that takes 10 sec(say) to finish execution. So GEC won&#39;t pop out of stack. It runs all the code for 10 sec.</li>
<li>But in the background, the timer runs for 5s. While callstack runs the 1M line of code, this timer has already expired and callback fun has been pushed to Callback queue and waiting to pushed to callstack to get executed.</li>
<li>Event loop keeps checking if callstack is empty or not. But here GEC is still in stack so cb can&#39;t be popped from callback Queue and pushed to CallStack. <strong>Though setTimeout is only for 5s, it waits for 10s until callstack is empty before it can execute</strong> (When GEC popped after 10sec, callstack() is pushed into call stack and immediately executed (Whatever is pushed to callstack is executed instantly).</li>
<li>This is called as the <strong><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop">Concurrency model</a></strong> of JS. This is the logic behind setTimeout&#39;s trust issues.</li>
</ul>
</li>
<li><p>The First rule of JavaScript: Do not <strong>block the main thread</strong> (as JS is a single threaded(only 1 callstack) language).</p>
</li>
<li><p>In below example, we are blocking the main thread. Observe Questiona and Output.
<img src="../assets/settimeout1.jpg" alt="setTimeout Demo"></p>
</li>
<li><p>setTimeout guarantees that it will take at least the given timer to execute the code.</p>
</li>
<li><p>JS is a synchronous single threaded language. With just 1 thread it runs all pieces of code. It becomes kind of an interpreter language, and runs code very fast inside browser (no need to wait for code to be compiled) (JIT - Just in time compilation). And there are still ways to do async operations as well.</p>
</li>
<li><p>What if <strong>timeout = 0sec</strong>?</p>
<pre class="prettyprint">console.log(&quot;Start&quot;);
setTimeout(function cb() {
  console.log(&quot;Callback&quot;);
}, 0);
console.log(&quot;End&quot;);
// Even though timer = 0s, the cb() has to go through the queue. Registers calback in webapi&#39;s env , moves to callback queue, and execute once callstack is empty.
// O/p - Start End Callback
// This method of putting timer = 0, can be used to defer a less imp function by a little so the more important function(here printing &quot;End&quot;) can take place
</pre>
</li>
</ul>
<hr>

<br>

<hr>

<br>

<h1 id="episode-18--higher-order-functions-ft-functional-programming"><a class="header-link" href="#episode-18--higher-order-functions-ft-functional-programming"></a>Episode 18 : Higher-Order Functions ft. Functional Programming</h1>
<h3 id="q-what-is-higher-order-function"><a class="header-link" href="#q-what-is-higher-order-function"></a>Q: What is Higher Order Function?</h3>
<p><strong>Ans</strong>: A Higher-order functions are regular functions that take other functions as arguments or return functions as their results. Eg:</p>
<pre class="hljs"><code><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">x</span>(<span class="hljs-params"></span>) </span>{
    <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;Hi)&quot;</span>;
};
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">y</span>(<span class="hljs-params">x</span>) </span>{
    x();
};
y(); <span class="hljs-comment">// Hi</span>
<span class="hljs-comment">// y is a higher order function</span>
<span class="hljs-comment">// x is a callback function</span></code></pre><p>Let&#39;s try to understand how we should approach solution in interview.
I have an array of radius and I have to calculate area using these radius and store in an array.</p>
<p>First Approach:</p>
<pre class="hljs"><code><span class="hljs-keyword">const</span> radius = [<span class="hljs-number">1</span>, <span class="hljs-number">2</span>, <span class="hljs-number">3</span>, <span class="hljs-number">4</span>];
<span class="hljs-keyword">const</span> calculateArea = <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">radius</span>) </span>{
  <span class="hljs-keyword">const</span> output = [];
  <span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> i = <span class="hljs-number">0</span>; i &lt; radius.length; i++) {
    output.push(<span class="hljs-built_in">Math</span>.PI * radius[i] * radius[i]);
  }
  <span class="hljs-keyword">return</span> output;
};
<span class="hljs-built_in">console</span>.log(calculateArea(radius));</code></pre><p>The above solution works perfectly fine but what if we have now requirement to calculate array of circumference. Code now be like</p>
<pre class="hljs"><code><span class="hljs-keyword">const</span> radius = [<span class="hljs-number">1</span>, <span class="hljs-number">2</span>, <span class="hljs-number">3</span>, <span class="hljs-number">4</span>];
<span class="hljs-keyword">const</span> calculateCircumference = <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">radius</span>) </span>{
  <span class="hljs-keyword">const</span> output = [];
  <span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> i = <span class="hljs-number">0</span>; i &lt; radius.length; i++) {
    output.push(<span class="hljs-number">2</span> * <span class="hljs-built_in">Math</span>.PI * radius[i]);
  }
  <span class="hljs-keyword">return</span> output;
};
<span class="hljs-built_in">console</span>.log(calculateCircumference(radius));</code></pre><p>But over here we are violating some principle like DRY Principle, now lets observe the better approach.</p>
<pre class="hljs"><code><span class="hljs-keyword">const</span> radiusArr = [<span class="hljs-number">1</span>, <span class="hljs-number">2</span>, <span class="hljs-number">3</span>, <span class="hljs-number">4</span>];

<span class="hljs-comment">// logic to calculate area</span>
<span class="hljs-keyword">const</span> area = <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">radius</span>) </span>{
    <span class="hljs-keyword">return</span> <span class="hljs-built_in">Math</span>.PI * radius * radius;
}

<span class="hljs-comment">// logic to calculate circumference</span>
<span class="hljs-keyword">const</span> circumference = <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">radius</span>) </span>{
    <span class="hljs-keyword">return</span> <span class="hljs-number">2</span> * <span class="hljs-built_in">Math</span>.PI * radius;
}

<span class="hljs-keyword">const</span> calculate = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">radiusArr, operation</span>) </span>{
    <span class="hljs-keyword">const</span> output = [];
    <span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> i = <span class="hljs-number">0</span>; i &lt; radiusArr.length; i++) {
        output.push(operation(radiusArr[i]));
    }
    <span class="hljs-keyword">return</span> output;
}
<span class="hljs-built_in">console</span>.log(calculate(radiusArr, area));
<span class="hljs-built_in">console</span>.log(calculate(radiusArr, circumference));
<span class="hljs-comment">// Over here calculate is HOF</span>
<span class="hljs-comment">// Over here we have extracted logic into separate functions. This is the beauty of functional programming.</span>

Polyfill <span class="hljs-keyword">of</span> map
<span class="hljs-comment">// Over here calculate is nothing but polyfill of map function</span>
<span class="hljs-comment">// console.log(radiusArr.map(area)) == console.log(calculate(radiusArr, area));</span>

***************************************************
Lets convert above calculate <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">as</span> <span class="hljs-title">map</span> <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">and</span> <span class="hljs-title">try</span> <span class="hljs-title">to</span> <span class="hljs-title">use</span>. <span class="hljs-title">So</span>,

<span class="hljs-title">Array</span>.<span class="hljs-title">prototype</span>.<span class="hljs-title">calculate</span> = <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">operation</span>) </span>{
    <span class="hljs-title">const</span> <span class="hljs-title">output</span> = []</span>;
    <span class="hljs-title">for</span> (<span class="hljs-params"><span class="hljs-keyword">let</span> i = <span class="hljs-number">0</span>; i &lt; <span class="hljs-built_in">this</span>.length; i++</span>) </span>{
        output.push(operation(<span class="hljs-built_in">this</span>[i]));
    }
    <span class="hljs-keyword">return</span> output;
}
<span class="hljs-built_in">console</span>.log(radiusArr.calculate(area))</code></pre><hr>

<br>

<hr>

<br>

<h1 id="episode-19--map-filter--reduce"><a class="header-link" href="#episode-19--map-filter--reduce"></a>Episode 19 : map, filter &amp; reduce</h1>
<blockquote>
<p>map, filter &amp; reducer are Higher Order Functions.</p>
</blockquote>
<h2 id="map-function"><a class="header-link" href="#map-function"></a>Map function</h2>
<p>It is basically used to transform a array. The map() method creates a new array with the results of calling a function for every array element.</p>
<p>const output = arr.map(<em>function</em>) // this <em>function</em> tells map that what transformation I want on each element of array</p>
<pre class="hljs"><code><span class="hljs-keyword">const</span> arr = [<span class="hljs-number">5</span>, <span class="hljs-number">1</span>, <span class="hljs-number">3</span>, <span class="hljs-number">2</span>, <span class="hljs-number">6</span>];
<span class="hljs-comment">// Task 1: Double the array element: [10, 2, 6, 4, 12]</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">double</span>(<span class="hljs-params">x</span>) </span>{
  <span class="hljs-keyword">return</span> x * <span class="hljs-number">2</span>;
}
<span class="hljs-keyword">const</span> doubleArr = arr.map(double); <span class="hljs-comment">// Internally map will run double function for each element of array and create a new array and returns it.</span>
<span class="hljs-built_in">console</span>.log(doubleArr); <span class="hljs-comment">// [10, 2, 6, 4, 12]</span></code></pre><pre class="hljs"><code><span class="hljs-comment">// Task 2: Triple the array element</span>
<span class="hljs-keyword">const</span> arr = [<span class="hljs-number">5</span>, <span class="hljs-number">1</span>, <span class="hljs-number">3</span>, <span class="hljs-number">2</span>, <span class="hljs-number">6</span>];
<span class="hljs-comment">// Transformation logic</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">triple</span>(<span class="hljs-params">x</span>) </span>{
  <span class="hljs-keyword">return</span> x * <span class="hljs-number">3</span>;
}
<span class="hljs-keyword">const</span> tripleArr = arr.map(triple);
<span class="hljs-built_in">console</span>.log(tripleArr); <span class="hljs-comment">// [15, 3, 9, 6, 18]</span></code></pre><pre class="hljs"><code><span class="hljs-comment">// Task 3: Convert array elements to binary</span>
<span class="hljs-keyword">const</span> arr = [<span class="hljs-number">5</span>, <span class="hljs-number">1</span>, <span class="hljs-number">3</span>, <span class="hljs-number">2</span>, <span class="hljs-number">6</span>];
<span class="hljs-comment">// Transformation logic:</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">binary</span>(<span class="hljs-params">x</span>) </span>{
    <span class="hljs-keyword">return</span> x.toString(<span class="hljs-number">2</span>);
}
<span class="hljs-keyword">const</span> binaryArr = arr.map(binary);

<span class="hljs-comment">// The above code can be rewritten as :</span>
<span class="hljs-keyword">const</span> binaryArr = arr.map(<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">binary</span>(<span class="hljs-params">x</span>) </span>{
    <span class="hljs-keyword">return</span> x.toString(<span class="hljs-number">2</span>);
}

<span class="hljs-comment">// OR -&gt; Arrow function</span>
<span class="hljs-keyword">const</span> binaryArr = arr.map(<span class="hljs-function">(<span class="hljs-params">x</span>) =&gt;</span> x.toString(<span class="hljs-number">2</span>));</code></pre><p>So basically map function is mapping each and every value and transforming it based on given condition.</p>
<h2 id="filter-function"><a class="header-link" href="#filter-function"></a>Filter function</h2>
<p>Filter function is basically used to filter the value inside an array. The arr.filter() method is used to create a new array from a given array consisting of only those elements from the given array which satisfy a condition set by the argument method.</p>
<pre class="hljs"><code><span class="hljs-keyword">const</span> array = [<span class="hljs-number">5</span>, <span class="hljs-number">1</span>, <span class="hljs-number">3</span>, <span class="hljs-number">2</span>, <span class="hljs-number">6</span>];
<span class="hljs-comment">// filter odd values</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">isOdd</span>(<span class="hljs-params">x</span>) </span>{
  <span class="hljs-keyword">return</span> x % <span class="hljs-number">2</span>;
}
<span class="hljs-keyword">const</span> oddArr = array.filter(isOdd); <span class="hljs-comment">// [5,1,3]</span>

<span class="hljs-comment">// Other way of writing the above:</span>
<span class="hljs-keyword">const</span> oddArr = arr.filter(<span class="hljs-function">(<span class="hljs-params">x</span>) =&gt;</span> x % <span class="hljs-number">2</span>);</code></pre><p>Filter function creates an array and store only those values which evaluates to true.</p>
<h2 id="reduce-function"><a class="header-link" href="#reduce-function"></a>Reduce function</h2>
<p>It is a function which take all the values of array and gives a single output of it. It reduces the array to give a single output.</p>
<pre class="hljs"><code><span class="hljs-keyword">const</span> array = [<span class="hljs-number">5</span>, <span class="hljs-number">1</span>, <span class="hljs-number">3</span>, <span class="hljs-number">2</span>, <span class="hljs-number">6</span>];
<span class="hljs-comment">// Calculate sum of elements of array - Non functional programming way</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">findSum</span>(<span class="hljs-params">arr</span>) </span>{
  <span class="hljs-keyword">let</span> sum = <span class="hljs-number">0</span>;
  <span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> i = <span class="hljs-number">0</span>; i &lt; arr.length; i++) {
    sum = sum + arr[i];
  }
  <span class="hljs-keyword">return</span> sum;
}
<span class="hljs-built_in">console</span>.log(findSum(array)); <span class="hljs-comment">// 17</span>

<span class="hljs-comment">// reduce function way</span>
<span class="hljs-keyword">const</span> sumOfElem = arr.reduce(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">accumulator, current</span>) </span>{
  <span class="hljs-comment">// current represent the value of array</span>
  <span class="hljs-comment">// accumulator is used the result from element of array.</span>
  <span class="hljs-comment">// In comparison to previous code snippet, *sum* variable is *accumulator* and *arr[i]* is *current*</span>
  accumulator = accumulator + current;
  <span class="hljs-keyword">return</span> accumulator;
}, <span class="hljs-number">0</span>); <span class="hljs-comment">//In above example sum was initialized with 0, so over here accumulator also needs to be initialized, so the second argument to reduce function represent the initialization value.</span>
<span class="hljs-built_in">console</span>.log(sumOfElem); <span class="hljs-comment">// 17</span></code></pre><pre class="hljs"><code><span class="hljs-comment">// find max inside array: Non functional programming way:</span>
<span class="hljs-keyword">const</span> array = [<span class="hljs-number">5</span>, <span class="hljs-number">1</span>, <span class="hljs-number">3</span>, <span class="hljs-number">2</span>, <span class="hljs-number">6</span>];
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">findMax</span>(<span class="hljs-params">arr</span>) </span>{
    <span class="hljs-keyword">let</span> max = <span class="hljs-number">0</span>;
    <span class="hljs-keyword">for</span>(<span class="hljs-keyword">let</span> i = <span class="hljs-number">0</span>; i &lt; arr.length; i++ {
        <span class="hljs-keyword">if</span> (arr[i] &gt; max) {
            max = arr[i]
        }
    }
    <span class="hljs-keyword">return</span> max;
}
<span class="hljs-built_in">console</span>.log(findMax(array)); <span class="hljs-comment">// 6</span>

<span class="hljs-comment">// using reduce</span>
<span class="hljs-keyword">const</span> output = arr.reduce(<span class="hljs-function">(<span class="hljs-params">acc, current</span>) =&gt;</span> {
    <span class="hljs-keyword">if</span> (current &gt; acc ) {
        acc = current;
    }
    <span class="hljs-keyword">return</span> acc;
}, <span class="hljs-number">0</span>);
<span class="hljs-built_in">console</span>.log(output); <span class="hljs-comment">// 6</span>

<span class="hljs-comment">// acc is just a label which represent the accumulated value till now,</span>
<span class="hljs-comment">// so we can also label it as max in this case</span>
<span class="hljs-keyword">const</span> output = arr.reduce(<span class="hljs-function">(<span class="hljs-params">max, current</span>) =&gt;</span> {
    <span class="hljs-keyword">if</span> (current &gt; max) {
        max= current;
    }
    <span class="hljs-keyword">return</span> max;
}, <span class="hljs-number">0</span>);
<span class="hljs-built_in">console</span>.log(output); <span class="hljs-comment">// 6</span></code></pre><h2 id="tricky-map"><a class="header-link" href="#tricky-map"></a>Tricky MAP</h2>
<pre class="hljs"><code><span class="hljs-keyword">const</span> users = [
    { <span class="hljs-attr">firstName</span>: <span class="hljs-string">&quot;Alok&quot;</span>, <span class="hljs-attr">lastName</span>: <span class="hljs-string">&quot;Raj&quot;</span>, <span class="hljs-attr">age</span>: <span class="hljs-number">23</span> },
    { <span class="hljs-attr">firstName</span>: <span class="hljs-string">&quot;Ashish&quot;</span>, <span class="hljs-attr">lastName</span>: <span class="hljs-string">&quot;Kumar&quot;</span>, <span class="hljs-attr">age</span>: <span class="hljs-number">29</span> },
    { <span class="hljs-attr">firstName</span>: <span class="hljs-string">&quot;Ankit&quot;</span>, <span class="hljs-attr">lastName</span>: <span class="hljs-string">&quot;Roy&quot;</span>, <span class="hljs-attr">age</span>: <span class="hljs-number">29</span> },
    { <span class="hljs-attr">firstName</span>: <span class="hljs-string">&quot;Pranav&quot;</span>, <span class="hljs-attr">lastName</span>: <span class="hljs-string">&quot;Mukherjee&quot;</span>, <span class="hljs-attr">age</span>: <span class="hljs-number">50</span> },
];
<span class="hljs-comment">// Get array of full name : [&quot;Alok Raj&quot;, &quot;Ashish Kumar&quot;, ...]</span>
<span class="hljs-keyword">const</span> fullNameArr = users.map(<span class="hljs-function">(<span class="hljs-params">user</span>) =&gt;</span> user.firstName + <span class="hljs-string">&quot; &quot;</span> + user.lastName);
<span class="hljs-built_in">console</span>.log(fullNameArr); <span class="hljs-comment">// [&quot;Alok Raj&quot;, &quot;Ashish Kumar&quot;, ...]</span>

----------------------------------------------------------

<span class="hljs-comment">// Get the count/report of how many unique people with unique age are there</span>
<span class="hljs-comment">// like: {29 : 2, 75 : 1, 50 : 1}</span>
<span class="hljs-comment">// We should use reduce, why? we want to deduce some information from the array. Basically we want to get a single object as output</span>
<span class="hljs-keyword">const</span> report = users.reduce(<span class="hljs-function">(<span class="hljs-params">acc, curr</span>) =&gt;</span> {
    <span class="hljs-keyword">if</span>(acc[curr.age]) {
        acc[curr.age] = ++ acc[curr.age] ;
    } <span class="hljs-keyword">else</span> {
        acc[curr.age] = <span class="hljs-number">1</span>;
    }
    <span class="hljs-keyword">return</span> acc;  <span class="hljs-comment">//to every time return update object</span>
}, {})
<span class="hljs-built_in">console</span>.log(report) <span class="hljs-comment">// {29 : 2, 75 : 1, 50 : 1}</span></code></pre><h2 id="function-chaining"><a class="header-link" href="#function-chaining"></a>Function Chaining</h2>
<pre class="hljs"><code><span class="hljs-comment">// First name of all people whose age is less than 30</span>
<span class="hljs-keyword">const</span> users = [
  { <span class="hljs-attr">firstName</span>: <span class="hljs-string">&quot;Alok&quot;</span>, <span class="hljs-attr">lastName</span>: <span class="hljs-string">&quot;Raj&quot;</span>, <span class="hljs-attr">age</span>: <span class="hljs-number">23</span> },
  { <span class="hljs-attr">firstName</span>: <span class="hljs-string">&quot;Ashish&quot;</span>, <span class="hljs-attr">lastName</span>: <span class="hljs-string">&quot;Kumar&quot;</span>, <span class="hljs-attr">age</span>: <span class="hljs-number">29</span> },
  { <span class="hljs-attr">firstName</span>: <span class="hljs-string">&quot;Ankit&quot;</span>, <span class="hljs-attr">lastName</span>: <span class="hljs-string">&quot;Roy&quot;</span>, <span class="hljs-attr">age</span>: <span class="hljs-number">29</span> },
  { <span class="hljs-attr">firstName</span>: <span class="hljs-string">&quot;Pranav&quot;</span>, <span class="hljs-attr">lastName</span>: <span class="hljs-string">&quot;Mukherjee&quot;</span>, <span class="hljs-attr">age</span>: <span class="hljs-number">50</span> },
];

<span class="hljs-comment">// function chaining</span>
<span class="hljs-keyword">const</span> output = users
  .filter(<span class="hljs-function">(<span class="hljs-params">user</span>) =&gt;</span> user.age &lt; <span class="hljs-number">30</span>)
  .map(<span class="hljs-function">(<span class="hljs-params">user</span>) =&gt;</span> user.firstName);
<span class="hljs-built_in">console</span>.log(output); <span class="hljs-comment">// [&quot;Alok&quot;, &quot;Ashish&quot;, &quot;Ankit&quot;]</span>

<span class="hljs-comment">// Homework challenge: Implement the same logic using reduce</span>
<span class="hljs-keyword">const</span> output = users.reduce(<span class="hljs-function">(<span class="hljs-params">acc, curr</span>) =&gt;</span> {
  <span class="hljs-keyword">if</span> (curr.age &lt; <span class="hljs-number">30</span>) {
    acc.push(curr.firstName);
  }
  <span class="hljs-keyword">return</span> acc;
}, []);
<span class="hljs-built_in">console</span>.log(output); <span class="hljs-comment">// [&quot;Alok&quot;, &quot;Ashish&quot;, &quot;Ankit&quot;]</span></code></pre><hr>

<br>

<hr>

<br>

<h1 id="episode-20--callback"><a class="header-link" href="#episode-20--callback"></a>Episode 20 : Callback</h1>
<ul class="list">
<li><p>There are 2 Parts of Callback:</p>
<ol class="list">
<li>Good Part of callback - Callback are super important while writing asynchronous code in JS</li>
<li>Bad Part of Callback - Using callback we can face issue:<ul class="list">
<li>Callback Hell</li>
<li>Inversion of control</li>
</ul>
</li>
</ol>
</li>
<li><p>Understanding of Bad part of callback is super important to learn Promise in next lecture.</p>
</li>
</ul>
<blockquote>
<p>💡 JavaScript is synchronous, single threaded language. It can Just do one thing at a time, it has just one call-stack and it can execute one thing at a time. Whatever code we give to Javascript will be quickly executed by Javascript engine, it does not wait.</p>
</blockquote>
<pre class="hljs"><code><span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;Namaste&quot;</span>);
<span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;JavaScript&quot;</span>);
<span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;Season 2&quot;</span>);
<span class="hljs-comment">// Namaste</span>
<span class="hljs-comment">// JavaScript</span>
<span class="hljs-comment">// Season 2</span>

<span class="hljs-comment">// 💡 It is quickly printing because `Time, tide &amp; Javascript waits for none.`</span></code></pre><p><em>But what if we have to delay execution of any line, we could utilize callback, How?</em></p>
<pre class="hljs"><code><span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;Namaste&quot;</span>);
<span class="hljs-built_in">setTimeout</span>(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;JavaScript&quot;</span>);
}, <span class="hljs-number">5000</span>);
<span class="hljs-built_in">console</span>.log(<span class="hljs-string">&quot;Season 2&quot;</span>);
<span class="hljs-comment">// Namaste</span>
<span class="hljs-comment">// Season 2</span>
<span class="hljs-comment">// JavaScript</span>

<span class="hljs-comment">// 💡 Here we are delaying the execution using callback approach of setTimeout.</span></code></pre><h3 id="🛒-e-commerce-web-app-situation"><a class="header-link" href="#🛒-e-commerce-web-app-situation"></a>🛒 e-Commerce web app situation</h3>
<p>Assume a scenario of e-Commerce web, where one user is placing order, he has added items like, shoes, pants and kurta in cart and now he is placing order. So in backend the situation could look something like this.</p>
<pre class="hljs"><code><span class="hljs-keyword">const</span> cart = [<span class="hljs-string">&quot;shoes&quot;</span>, <span class="hljs-string">&quot;pants&quot;</span>, <span class="hljs-string">&quot;kurta&quot;</span>];
<span class="hljs-comment">// Two steps to place a order</span>
<span class="hljs-comment">// 1. Create a Order</span>
<span class="hljs-comment">// 2. Proceed to Payment</span>

<span class="hljs-comment">// It could look something like this:</span>
api.createOrder();
api.proceedToPayment();</code></pre><p>Assumption, once order is created then only we can proceed to payment, so there is a dependency. So How to manage this dependency.
Callback can come as rescue, How?</p>
<pre class="hljs"><code>api.createOrder(cart, <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{
  api.proceedToPayment();
});
<span class="hljs-comment">// 💡 Over here `createOrder` api is first creating a order then it is responsible to call `api.proceedToPayment()` as part of callback approach.</span></code></pre><p>To make it a bit complicated, what if after payment is done, you have to show Order summary by calling <code>api.showOrderSummary()</code> and now it has dependency on <code>api.proceedToPayment()</code>
Now my code should look something like this:</p>
<pre class="hljs"><code>api.createOrder(cart, <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{
  api.proceedToPayment(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{
    api.showOrderSummary();
  });
});</code></pre><p>Now what if we have to update the wallet, now this will have a dependency over <code>showOrderSummary</code></p>
<pre class="hljs"><code>api.createOrder(cart, <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{
  api.proceedToPayment(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{
    api.showOrderSummary(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{
      api.updateWallet();
    });
  });
});
<span class="hljs-comment">// 💡 Callback Hell</span></code></pre><p>When we have a large codebase and multiple apis and have dependency on each other, then we fall into callback hell.
These codes are tough to maintain.
These callback hell structure is also known as <strong>Pyramid of Doom</strong>.</p>
<p>Till this point we are comfortable with concept of callback hell but now lets discuss about <code>Inversion of Control</code>. It is very important to understand in order to get comfortable around the concept of promise.</p>
<blockquote>
<p>💡 Inversion of control is like that you lose the control of code when we are using callback.</p>
</blockquote>
<p>Let&#39;s understand with the help of example code and comments:</p>
<pre class="hljs"><code>api.createOrder(cart, <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{
  api.proceedToPayment();
});

<span class="hljs-comment">// 💡 So over here, we are creating a order and then we are blindly trusting `createOrder` to call `proceedToPayment`.</span>

<span class="hljs-comment">// 💡 It is risky, as `proceedToPayment` is important part of code and we are blindly trusting `createOrder` to call it and handle it.</span>

<span class="hljs-comment">// 💡 When we pass a function as a callback, basically we are dependant on our parent function that it is his responsibility to run that function. This is called `inversion of control` because we are dependant on that function. What if parent function stopped working, what if it was developed by another programmer or callback runs two times or never run at all.</span>

<span class="hljs-comment">// 💡 In next session, we will see how we can fix such problems.</span></code></pre><blockquote>
<p>💡 Async programming in JavaScript exists because callback exits.</p>
</blockquote>
<p>more at <code>http://callbackhell.com/</code></p>

<br>

<hr>

<h1 id="episode-21--promises"><a class="header-link" href="#episode-21--promises"></a>Episode 21 : Promises</h1>
<blockquote>
<p>Promises are used to handle async operations in JavaScript.</p>
</blockquote>
<p>We will discuss with code example that how things used to work before <code>Promises</code> and then how it works after <code>Promises</code></p>
<p>Suppose, taking an example of E-Commerce</p>
<pre class="hljs"><code><span class="hljs-keyword">const</span> cart = [<span class="hljs-string">&quot;shoes&quot;</span>, <span class="hljs-string">&quot;pants&quot;</span>, <span class="hljs-string">&quot;kurta&quot;</span>];

<span class="hljs-comment">// Below two functions are asynchronous and dependent on each other</span>
<span class="hljs-keyword">const</span> orderId = createOrder(cart);
proceedToPayment(orderId);

<span class="hljs-comment">// with Callback (Before Promise)</span>
<span class="hljs-comment">// Below here, it is the responsibility of createOrder function to first create the order then call the callback function</span>
createOrder(cart, <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{
  proceedToPayment(orderId);
});
<span class="hljs-comment">// Above there is the issue of `Inversion of Control`</span></code></pre><p>Q: How to fix the above issue?<br><em>A: Using Promise.</em></p>
<p>Now, we will make <code>createOrder</code> function return a promise and we will capture that <code>promise</code> into a <code>variable</code></p>
<p>Promise is nothing but we can assume it to be empty object with some data value in it, and this data value will hold whatever this <code>createOrder</code> function will return.</p>
<p>Since <code>createOrder</code> function is an async function and we don&#39;t know how much time will it take to finish execution.</p>
<p>So the moment <code>createOrder</code> will get executed, it will return you a <code>undefined</code> value. Let&#39;s say after 5 secs execution finished so now <code>orderId</code> is ready so, it will fill the <code>undefined</code> value with the <code>orderId</code>.</p>
<p>In short, When <code>createOrder</code> get executed, it immediately returns a <code>promise object</code> with <code>undefined</code> value. then javascript will continue to execute with other lines of code. After sometime when <code>createOrder</code> has finished execution and <code>orderId</code> is ready then that will <code>automatically</code> be assigned to our returned <code>promise</code> which was earlier <code>undefined</code>.</p>
<p>Q: Question is how we will get to know <code>response</code> is ready?<br><em>A: So, we will attach a <code>callback</code> function to the <code>promise object</code> using <code>then</code> to get triggered automatically when <code>result</code> is ready.</em></p>
<pre class="hljs"><code><span class="hljs-keyword">const</span> cart = [<span class="hljs-string">&quot;shoes&quot;</span>, <span class="hljs-string">&quot;pants&quot;</span>, <span class="hljs-string">&quot;kurta&quot;</span>];

<span class="hljs-keyword">const</span> promiseRef = createOrder(cart);
<span class="hljs-comment">// this promiseRef has access to `then`</span>

<span class="hljs-comment">// {data: undefined}</span>
<span class="hljs-comment">// Initially it will be undefined so below code won&#x27;t trigger</span>
<span class="hljs-comment">// After some time, when execution has finished and promiseRef has the data then automatically the below line will get triggered.</span>

promiseRef.then(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{
  proceedToPayment(orderId);
});</code></pre><p>Q: How it is better than callback approach?</p>
<p>In Earlier solution we used to pass the function and then used to trust the function to execute the callback.</p>
<p>But with promise, we are attaching a callback function to a promiseObject.</p>
<p>There is difference between these words, passing a function and attaching a function.</p>
<p>Promise guarantee, it will callback the attached function once it has the fulfilled data. And it will call it only once. Just once.</p>
<p>Earlier we talked about promise are object with empty data but that&#39;s not entirely true, <code>Promise</code> are much more than that.</p>
<p>Now let&#39;s understand and see a real promise object.</p>
<p>fetch is a web-api which is utilized to make api call and it returns a promise.</p>
<p>We will be calling public github api to fetch data
<a href="https://api.github.com/users/alok722">https://api.github.com/users/alok722</a></p>
<pre class="hljs"><code><span class="hljs-comment">// We will be calling public github api to fetch data</span>
<span class="hljs-keyword">const</span> URL = <span class="hljs-string">&quot;https://api.github.com/users/alok722&quot;</span>;
<span class="hljs-keyword">const</span> user = fetch(URL);
<span class="hljs-comment">// User above will be a promise.</span>
<span class="hljs-built_in">console</span>.log(user); <span class="hljs-comment">// Promise {&lt;Pending&gt;}</span>

<span class="hljs-comment">/** OBSERVATIONS:
 * If we will deep dive and see, this `promise` object has 3 things
 * `prototype`, `promiseState` &amp; `promiseResult`
 * &amp; this `promiseResult` is the same data which we talked earlier as data
 * &amp; initially `promiseResult` is `undefined`
 *
 * `promiseResult` will store data returned from API call
 * `promiseState` will tell in which state the promise is currently, initially it will be in `pending` state and later it will become `fulfilled`
 */</span>

<span class="hljs-comment">/**
 * When above line is executed, `fetch` makes API call and return a `promise` instantly which is in `Pending` state and Javascript doesn&#x27;t wait to get it `fulfilled`
 * And in next line it console out the `pending promise`.
 * <span class="hljs-doctag">NOTE:</span> chrome browser has some in-consistency, the moment console happens it shows in pending state but if you will expand that it will show fulfilled because chrome updated the log when promise get fulfilled.
 * Once fulfilled data is there in promiseResult and it is inside body in ReadableStream format and there is a way to extract data.
 */</span></code></pre><p>Now we can attach callback to above response?</p>
<p>Using <code>.then</code></p>
<pre class="hljs"><code><span class="hljs-keyword">const</span> URL = <span class="hljs-string">&quot;https://api.github.com/users/alok722&quot;</span>;
<span class="hljs-keyword">const</span> user = fetch(URL);

user.then(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">data</span>) </span>{
  <span class="hljs-built_in">console</span>.log(data);
});
<span class="hljs-comment">// And this is how Promise is used.</span>
<span class="hljs-comment">// It guarantees that it could be resolved only once, either it could be `success` or `failure`</span>
<span class="hljs-comment">/**
    A Promise is in one of these states:

    pending: initial state, neither fulfilled nor rejected.
    fulfilled: meaning that the operation was completed successfully.
    rejected: meaning that the operation failed.
 */</span></code></pre><p>💡Promise Object are immutable.<br>-&gt; Once promise is fulfilled and we have data we can pass here and there and we don&#39;t have to worry that someone can mutate that data. So over above we can&#39;t directly mutate <code>user</code> promise object, we will have to use <code>.then</code></p>
<h3 id="interview-guide"><a class="header-link" href="#interview-guide"></a>Interview Guide</h3>
<p>💡What is Promise?<br>-&gt; Promise object is a placeholder for certain period of time until we receive value from asynchronous operation.</p>
<p>-&gt; A container for a future value.</p>
<p>-&gt; <strong>A Promise is an object representing the eventual completion or failure of an asynchronous operation.</strong></p>
<p>We are now done solving one issue of callback i.e. Inversion of Control</p>
<p>But there is one more issue, callback hell...</p>
<pre class="hljs"><code><span class="hljs-comment">// Callback Hell Example</span>
createOrder(cart, <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">orderId</span>) </span>{
  proceedToPayment(orderId, <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">paymentInf</span>) </span>{
    showOrderSummary(paymentInf, <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">balance</span>) </span>{
      updateWalletBalance(balance);
    });
  });
});
<span class="hljs-comment">// And now above code is expanding horizontally and this is called pyramid of doom.</span>
<span class="hljs-comment">// Callback hell is ugly and hard to maintain.</span>

<span class="hljs-comment">// 💡 Promise fixes this issue too using `Promise Chaining`</span>
<span class="hljs-comment">// Example Below is a Promise Chaining</span>
createOrder(cart)
  .then(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">orderId</span>) </span>{
    proceedToPayment(orderId);
  })
  .then(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">paymentInf</span>) </span>{
    showOrderSummary(paymentInf);
  })
  .then(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">balance</span>) </span>{
    updateWalletBalance(balance);
  });

<span class="hljs-comment">// ⚠️ Common PitFall</span>
<span class="hljs-comment">// We forget to return promise in Promise Chaining</span>
<span class="hljs-comment">// The idea is promise/data returned from one .then become data for next .then</span>
<span class="hljs-comment">// So,</span>
createOrder(cart)
  .then(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">orderId</span>) </span>{
    <span class="hljs-keyword">return</span> proceedToPayment(orderId);
  })
  .then(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">paymentInf</span>) </span>{
    <span class="hljs-keyword">return</span> showOrderSummary(paymentInf);
  })
  .then(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">balance</span>) </span>{
    <span class="hljs-keyword">return</span> updateWalletBalance(balance);
  });

<span class="hljs-comment">// To improve readability you can use arrow function instead of regular function</span></code></pre><hr>


<br>

<hr>

<h1 id="episode-22--creating-a-promise-chaining--error-handling"><a class="header-link" href="#episode-22--creating-a-promise-chaining--error-handling"></a>Episode 22 : Creating a Promise, Chaining &amp; Error Handling</h1>
<h3 id=""><a class="header-link" href="#"></a></h3>
<pre class="hljs"><code><span class="hljs-keyword">const</span> cart = [<span class="hljs-string">&quot;shoes&quot;</span>, <span class="hljs-string">&quot;pants&quot;</span>, <span class="hljs-string">&quot;kurta&quot;</span>];

<span class="hljs-comment">// Consumer part of promise</span>
<span class="hljs-keyword">const</span> promise = createOrder(cart); <span class="hljs-comment">// orderId</span>
<span class="hljs-comment">// Our expectation is above function is going to return me a promise.</span>

promise.then(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">orderId</span>) </span>{
  proceedToPayment(orderId);
});

<span class="hljs-comment">// Above snippet we have observed in our previous lecture itself.</span>
<span class="hljs-comment">// Now we will see, how createOrder is implemented so that it is returning a promise</span>
<span class="hljs-comment">// In short we will see, &quot;How we can create Promise&quot; and then return it.</span>

<span class="hljs-comment">// Producer part of Promise</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">createOrder</span>(<span class="hljs-params">cart</span>) </span>{
  <span class="hljs-comment">// JS provides a Promise constructor through which we can create promise</span>
  <span class="hljs-comment">// It accepts a callback function with two parameter `resolve` &amp; `reject`</span>
  <span class="hljs-keyword">const</span> promise = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">resolve, reject</span>) </span>{
    <span class="hljs-comment">// What is this `resolve` and `reject`?</span>
    <span class="hljs-comment">// These are function which are passed by javascript to us in order to handle success and failure of function call.</span>
    <span class="hljs-comment">// Now we will write logic to `createOrder`</span>
    <span class="hljs-comment">/** Mock logic steps
     * 1. validateCart
     * 2. Insert in DB and get an orderId
     */</span>
    <span class="hljs-comment">// We are assuming in real world scenario, validateCart would be defined</span>
    <span class="hljs-keyword">if</span> (!validateCart(cart)) {
      <span class="hljs-comment">// If cart not valid, reject the promise</span>
      <span class="hljs-keyword">const</span> err = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Error</span>(<span class="hljs-string">&quot;Cart is not Valid&quot;</span>);
      reject(err);
    }
    <span class="hljs-keyword">const</span> orderId = <span class="hljs-string">&quot;12345&quot;</span>; <span class="hljs-comment">// We got this id by calling to db (Assumption)</span>
    <span class="hljs-keyword">if</span> (orderId) {
      <span class="hljs-comment">// Success scenario</span>
      resolve(orderId);
    }
  });
  <span class="hljs-keyword">return</span> promise;
}</code></pre><p>Over above, if your validateCart is returning true, so the above promise will be resolved (success),</p>
<pre class="hljs"><code><span class="hljs-keyword">const</span> cart = [<span class="hljs-string">&quot;shoes&quot;</span>, <span class="hljs-string">&quot;pants&quot;</span>, <span class="hljs-string">&quot;kurta&quot;</span>];

<span class="hljs-keyword">const</span> promise = createOrder(cart); <span class="hljs-comment">// orderId</span>
<span class="hljs-comment">// ❓ What will be printed in below line?</span>
<span class="hljs-comment">// It prints Promise {&lt;pending&gt;}, but why?</span>
<span class="hljs-comment">// Because above createOrder is going to take sometime to get resolved, so pending state. But once the promise is resolved, `.then` would be executed for callback.</span>
<span class="hljs-built_in">console</span>.log(promise);

promise.then(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">orderId</span>) </span>{
  proceedToPayment(orderId);
});

<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">createOrder</span>(<span class="hljs-params">cart</span>) </span>{
  <span class="hljs-keyword">const</span> promise = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">resolve, reject</span>) </span>{
    <span class="hljs-keyword">if</span> (!validateCart(cart)) {
      <span class="hljs-keyword">const</span> err = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Error</span>(<span class="hljs-string">&quot;Cart is not Valid&quot;</span>);
      reject(err);
    }
    <span class="hljs-keyword">const</span> orderId = <span class="hljs-string">&quot;12345&quot;</span>;
    <span class="hljs-keyword">if</span> (orderId) {
      resolve(orderId);
    }
  });
  <span class="hljs-keyword">return</span> promise;
}</code></pre><p>Now let&#39;s see if there was some error and we are rejecting the promise, how we could catch that?<br>-&gt; Using <code>.catch</code></p>
<pre class="hljs"><code><span class="hljs-keyword">const</span> cart = [<span class="hljs-string">&quot;shoes&quot;</span>, <span class="hljs-string">&quot;pants&quot;</span>, <span class="hljs-string">&quot;kurta&quot;</span>];

<span class="hljs-keyword">const</span> promise = createOrder(cart); <span class="hljs-comment">// orderId</span>

<span class="hljs-comment">// Here we are consuming Promise and will try to catch promise error</span>
promise
  .then(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">orderId</span>) </span>{
    <span class="hljs-comment">// ✅ success aka resolved promise handling</span>
    proceedToPayment(orderId);
  })
  .catch(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">err</span>) </span>{
    <span class="hljs-comment">// ⚠️ failure aka reject handling</span>
    <span class="hljs-built_in">console</span>.log(err);
  });

<span class="hljs-comment">// Here we are creating Promise</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">createOrder</span>(<span class="hljs-params">cart</span>) </span>{
  <span class="hljs-keyword">const</span> promise = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">resolve, reject</span>) </span>{
    <span class="hljs-comment">// Assume below `validateCart` return false then the promise will be rejected</span>
    <span class="hljs-comment">// And then our browser is going to throw the error.</span>
    <span class="hljs-keyword">if</span> (!validateCart(cart)) {
      <span class="hljs-keyword">const</span> err = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Error</span>(<span class="hljs-string">&quot;Cart is not Valid&quot;</span>);
      reject(err);
    }
    <span class="hljs-keyword">const</span> orderId = <span class="hljs-string">&quot;12345&quot;</span>;
    <span class="hljs-keyword">if</span> (orderId) {
      resolve(orderId);
    }
  });
  <span class="hljs-keyword">return</span> promise;
}</code></pre><p>Now, Let&#39;s understand the concept of Promise Chaining<br>-&gt; for this we will assume after <code>createOrder</code> we have to invoke <code>proceedToPayment</code><br>-&gt; In promise chaining, whatever is returned from first <code>.then</code> become data for next <code>.then</code> and so on...<br>-&gt; At any point of promise chaining, if promise is rejected, the execution will fallback to <code>.catch</code> and others promise won&#39;t run.</p>
<pre class="hljs"><code><span class="hljs-keyword">const</span> cart = [<span class="hljs-string">&quot;shoes&quot;</span>, <span class="hljs-string">&quot;pants&quot;</span>, <span class="hljs-string">&quot;kurta&quot;</span>];

createOrder(cart)
  .then(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">orderId</span>) </span>{
    <span class="hljs-comment">// ✅ success aka resolved promise handling</span>
    <span class="hljs-comment">// 💡 we have return data or promise so that we can keep chaining the promises, here we are returning data</span>
    <span class="hljs-built_in">console</span>.log(orderId);
    <span class="hljs-keyword">return</span> orderId;
  })
  .then(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">orderId</span>) </span>{
    <span class="hljs-comment">// Promise chaining</span>
    <span class="hljs-comment">// 💡 we will make sure that `proceedToPayment` returns a promise too</span>
    <span class="hljs-keyword">return</span> proceedToPayment(orderId);
  })
  .then(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">paymentInfo</span>) </span>{
    <span class="hljs-comment">// from above, `proceedToPayment` is returning a promise so we can consume using `.then`</span>
    <span class="hljs-built_in">console</span>.log(paymentInfo);
  })
  .catch(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">err</span>) </span>{
    <span class="hljs-comment">// ⚠️ failure aka reject handling</span>
    <span class="hljs-built_in">console</span>.log(err);
  });

<span class="hljs-comment">// Here we are creating Promise</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">createOrder</span>(<span class="hljs-params">cart</span>) </span>{
  <span class="hljs-keyword">const</span> promise = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">resolve, reject</span>) </span>{
    <span class="hljs-comment">// Assume below `validateCart` return false then the promise will be rejected</span>
    <span class="hljs-comment">// And then our browser is going to throw the error.</span>
    <span class="hljs-keyword">if</span> (!validateCart(cart)) {
      <span class="hljs-keyword">const</span> err = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Error</span>(<span class="hljs-string">&quot;Cart is not Valid&quot;</span>);
      reject(err);
    }
    <span class="hljs-keyword">const</span> orderId = <span class="hljs-string">&quot;12345&quot;</span>;
    <span class="hljs-keyword">if</span> (orderId) {
      resolve(orderId);
    }
  });
  <span class="hljs-keyword">return</span> promise;
}

<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">proceedToPayment</span>(<span class="hljs-params">cart</span>) </span>{
  <span class="hljs-keyword">return</span> <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">resolve, reject</span>) </span>{
    <span class="hljs-comment">// For time being, we are simply `resolving` promise</span>
    resolve(<span class="hljs-string">&quot;Payment Successful&quot;</span>);
  });
}</code></pre><p>Q: What if we want to continue execution even if any of my promise is failing, how to achieve this?<br>-&gt; By placing the <code>.catch</code> block at some level after which we are not concerned with failure.<br>-&gt; There could be multiple <code>.catch</code> too.
Eg:</p>
<pre class="hljs"><code>createOrder(cart)
  .then(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">orderId</span>) </span>{
    <span class="hljs-comment">// ✅ success aka resolved promise handling</span>
    <span class="hljs-comment">// 💡 we have return data or promise so that we can keep chaining the promises, here we are returning data</span>
    <span class="hljs-built_in">console</span>.log(orderId);
    <span class="hljs-keyword">return</span> orderId;
  })
    .catch(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">err</span>) </span>{
    <span class="hljs-comment">// ⚠️ Whatever fails below it, catch wont care</span>
    <span class="hljs-comment">// this block is responsible for code block above it.</span>
    <span class="hljs-built_in">console</span>.log(err);
  });
  .then(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">orderId</span>) </span>{
    <span class="hljs-comment">// Promise chaining</span>
    <span class="hljs-comment">// 💡 we will make sure that `proceedToPayment` returns a promise too</span>
    <span class="hljs-keyword">return</span> proceedToPayment(orderId);
  })
  .then(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params">paymentInfo</span>) </span>{
    <span class="hljs-comment">// from above, `proceedToPayment` is returning a promise so we can consume using `.then`</span>
    <span class="hljs-built_in">console</span>.log(paymentInfo);
  })</code></pre><hr>

<br>

<hr>

<h1 id="episode-23--async-await"><a class="header-link" href="#episode-23--async-await"></a>Episode 23 : async await</h1>
<h3 id="-1"><a class="header-link" href="#-1"></a></h3>
<p>Topics Covered</p>
<ul class="list">
<li>What is async?</li>
<li>What is await?</li>
<li>How async await works behind the scenes?</li>
<li>Example of using async/await</li>
<li>Error Handling</li>
<li>Interviews</li>
<li>Async await vs Promise.then/.catch</li>
</ul>
<p>Q: What is async?<br>A: Async is a keyword that is used before a function to create a async function.</p>
<p>Q: What is async function and how it is different from normal function?  </p>
<pre class="hljs"><code><span class="hljs-comment">// 💡 async function always returns a promise, even if I return a simple string from below function, async keyword will wrap it under Promise and then return.</span>
<span class="hljs-keyword">async</span> <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">getData</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-keyword">return</span> <span class="hljs-string">&quot;Namaste JavaScript&quot;</span>;
}
<span class="hljs-keyword">const</span> dataPromise = getData();
<span class="hljs-built_in">console</span>.log(dataPromise); <span class="hljs-comment">// Promise {&lt;fulfilled&gt;: &#x27;Namaste JavaScript&#x27;}</span>

<span class="hljs-comment">//❓How to extract data from above promise? One way is using promise .then</span>
dataPromise.then(<span class="hljs-function"><span class="hljs-params">res</span> =&gt;</span> <span class="hljs-built_in">console</span>.log(res)); <span class="hljs-comment">// Namaste JavaScript</span></code></pre><p>Another example where <code>async</code> function is returning a Promise</p>
<pre class="hljs"><code><span class="hljs-keyword">const</span> p = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  resolve(<span class="hljs-string">&#x27;Promise resolved value!!&#x27;</span>);
})

<span class="hljs-keyword">async</span> <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">getData</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-keyword">return</span> p;
}
<span class="hljs-comment">// In above case, since we are already returning a promise async function would simply return that instead of wrapping with a new Promise.</span>
<span class="hljs-keyword">const</span> dataPromise = getData();
<span class="hljs-built_in">console</span>.log(dataPromise); <span class="hljs-comment">// Promise {&lt;fulfilled&gt;: &#x27;Promise resolved value!!&#x27;}</span>
dataPromise.then(<span class="hljs-function"><span class="hljs-params">res</span> =&gt;</span> <span class="hljs-built_in">console</span>.log(res)); <span class="hljs-comment">// Promise resolved value!!</span></code></pre><p>Q: How we can use <code>await</code> along with async function?<br>A: <code>async</code> and <code>await</code> combo is used to handle promises.</p>
<p>But Question is how we used to handle promises earlier and why we even need async/await?</p>
<pre class="hljs"><code><span class="hljs-keyword">const</span> p = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  resolve(<span class="hljs-string">&#x27;Promise resolved value!!&#x27;</span>);
})

<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">getData</span>(<span class="hljs-params"></span>) </span>{
  p.then(<span class="hljs-function"><span class="hljs-params">res</span> =&gt;</span> <span class="hljs-built_in">console</span>.log(res));
}

getData(); <span class="hljs-comment">// Promise resolved value!!</span>

<span class="hljs-comment">//📌 Till now we have been using Promise.then/.catch to handle promise.</span>
<span class="hljs-comment">// Now let&#x27;s see how async await can help us and how it is different</span>

<span class="hljs-comment">// The rule is we have to use keyword await in front of promise.</span>
<span class="hljs-keyword">async</span> <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">handlePromise</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-keyword">const</span> val = <span class="hljs-keyword">await</span> p;
  <span class="hljs-built_in">console</span>.log(val);
}
handlePromise(); <span class="hljs-comment">// Promise resolved value!!</span></code></pre><p>📌 <code>await</code> is a keyword that can only be used inside a <code>async</code> function.</p>
<pre class="hljs"><code><span class="hljs-keyword">await</span> <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>{} <span class="hljs-comment">// Syntax error: await is only valid under async function.</span></code></pre><p>Q: What makes <code>async</code>-<code>await</code> special?<br>A: Let&#39;s understand with one example where we will compare async-await way of resolving promise with older .then/.catch fashion. For that we will modify our promise <code>p</code>.</p>
<pre class="hljs"><code><span class="hljs-keyword">const</span> p = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    resolve(<span class="hljs-string">&#x27;Promise resolved value!!&#x27;</span>);
  }, <span class="hljs-number">3000</span>);
})

<span class="hljs-comment">// Let&#x27;s now compare with some modification:</span>

<span class="hljs-comment">// 📌 Promise.then/.catch way</span>
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">getData</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-comment">// JS engine will not wait for promise to be resolved</span>
  p.then(<span class="hljs-function"><span class="hljs-params">res</span> =&gt;</span> <span class="hljs-built_in">console</span>.log(res));
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&#x27;Hello There!&#x27;</span>);
}

getData(); <span class="hljs-comment">// First `Hello There!` would be printed and then after 3 secs &#x27;Promise resolved value!!&#x27; will be printed.</span>
<span class="hljs-comment">// Above happened as Javascript wait for none, so it will register this promise and take this callback function and register separately then js will move on and execute the following console and later once promise is resolved, following console will be printed.</span>

<span class="hljs-comment">//❓ Problem: Normally one used to get confused that JS will wait for promise to be resolved before executing following lines.</span>

<span class="hljs-comment">// 📌 async-wait way:</span>
<span class="hljs-keyword">async</span> <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">handlePromise</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-comment">// JS Engine will waiting for promise to resolve.</span>
  <span class="hljs-keyword">const</span> val = <span class="hljs-keyword">await</span> p;
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&#x27;Hello There!&#x27;</span>);
  <span class="hljs-built_in">console</span>.log(val);
}
handlePromise(); <span class="hljs-comment">// This time `Hello There!` won&#x27;t be printed immediately instead after 3 secs `Hello There!` will be printed followed by &#x27;Promise resolved value!!&#x27;</span>
<span class="hljs-comment">// 💡 So basically code was waiting at `await` line to get the promise resolve before moving on to next line.</span>

<span class="hljs-comment">// Above is the major difference between Promise.then/.catch vs async-await</span>

<span class="hljs-comment">//🤓 Let&#x27;s brainstorm more around async-await</span>
<span class="hljs-keyword">async</span> <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">handlePromise</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&#x27;Hi&#x27;</span>);
  <span class="hljs-keyword">const</span> val = <span class="hljs-keyword">await</span> p;
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&#x27;Hello There!&#x27;</span>);
  <span class="hljs-built_in">console</span>.log(val);

  <span class="hljs-keyword">const</span> val2 = <span class="hljs-keyword">await</span> p;
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&#x27;Hello There! 2&#x27;</span>);
  <span class="hljs-built_in">console</span>.log(val2);
}
handlePromise(); 
<span class="hljs-comment">// In above code example, will our program wait for 2 time or will it execute parallely.</span>
<span class="hljs-comment">//📌 `Hi` printed instantly -&gt; now code will wait for 3 secs -&gt; After 3 secs both promises will be resolved so (&#x27;Hello There!&#x27; &#x27;Promise resolved value!!&#x27; &#x27;Hello There! 2&#x27; &#x27;Promise resolved value!!&#x27;) will get printed immediately.</span>

<span class="hljs-comment">// Let&#x27;s create one promise and then resolve two different promise.</span>
<span class="hljs-keyword">const</span> p2 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    resolve(<span class="hljs-string">&#x27;Promise resolved value by p2!!&#x27;</span>);
  }, <span class="hljs-number">2000</span>);
})

<span class="hljs-keyword">async</span> <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">handlePromise</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&#x27;Hi&#x27;</span>);
  <span class="hljs-keyword">const</span> val = <span class="hljs-keyword">await</span> p;
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&#x27;Hello There!&#x27;</span>);
  <span class="hljs-built_in">console</span>.log(val);

  <span class="hljs-keyword">const</span> val2 = <span class="hljs-keyword">await</span> p2;
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&#x27;Hello There! 2&#x27;</span>);
  <span class="hljs-built_in">console</span>.log(val2);
}
handlePromise(); 
<span class="hljs-comment">// 📌 `Hi` printed instantly -&gt; now code will wait for 3 secs -&gt; After 3 secs both promises will be resolved so (&#x27;Hello There!&#x27; &#x27;Promise resolved value!!&#x27; &#x27;Hello There! 2&#x27; &#x27;Promise resolved value by p2!!&#x27;) will get printed immediately. So even though `p2` was resolved after 2 secs it had to wait for `p` to get resolved</span>


<span class="hljs-comment">// Now let&#x27;s reverse the order execution of promise and observe response.</span>
<span class="hljs-keyword">async</span> <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">handlePromise</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&#x27;Hi&#x27;</span>);
  <span class="hljs-keyword">const</span> val = <span class="hljs-keyword">await</span> p2;
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&#x27;Hello There!&#x27;</span>);
  <span class="hljs-built_in">console</span>.log(val);

  <span class="hljs-keyword">const</span> val2 = <span class="hljs-keyword">await</span> p;
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&#x27;Hello There! 2&#x27;</span>);
  <span class="hljs-built_in">console</span>.log(val2);
}
handlePromise(); 
<span class="hljs-comment">// 📌 `Hi` printed instantly -&gt; now code will wait for 2 secs -&gt; After 2 secs (&#x27;Hello There!&#x27; &#x27;Promise resolved value by p2!!&#x27;) will get printed and in the subsequent second i.e. after 3 secs (&#x27;Hello There! 2&#x27; &#x27;Promise resolved value!!&#x27;) will get printed</span></code></pre><p>Q: Question is Is program actually waiting or what is happening behind the scene?<br>A: As we know, Time, Tide and JS wait for none. And it&#39;s true. Over here it appears that JS engine is waiting but JS engine is not waiting over here. It has not occupied the call stack if that would have been the case our page may have got frozen. So JS engine is not waiting. So if it is not waiting then what it is doing behind the scene? Let&#39;s understand with below code snippet.</p>
<pre class="hljs"><code><span class="hljs-keyword">const</span> p1 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    resolve(<span class="hljs-string">&#x27;Promise resolved value by p1!!&#x27;</span>);
  }, <span class="hljs-number">5000</span>);
})

<span class="hljs-keyword">const</span> p2 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    resolve(<span class="hljs-string">&#x27;Promise resolved value by p2!!&#x27;</span>);
  }, <span class="hljs-number">10000</span>);
})

<span class="hljs-keyword">async</span> <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">handlePromise</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&#x27;Hi&#x27;</span>);
  <span class="hljs-keyword">debugger</span>;
  <span class="hljs-keyword">const</span> val = <span class="hljs-keyword">await</span> p;
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&#x27;Hello There!&#x27;</span>);
  <span class="hljs-keyword">debugger</span>;
  <span class="hljs-built_in">console</span>.log(val);

  <span class="hljs-keyword">const</span> val2 = <span class="hljs-keyword">await</span> p2;
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">&#x27;Hello There! 2&#x27;</span>);
  <span class="hljs-keyword">debugger</span>;
  <span class="hljs-built_in">console</span>.log(val2);
}
handlePromise(); 
<span class="hljs-comment">// When this function is executed, it will go line by line as JS is synchronous single threaded language. Lets observe what is happening under call-stack. Above you can see we have set the break-points.</span>

<span class="hljs-comment">// call stack flow -&gt; handlePromise() is pushed -&gt; It will log `Hi` to console -&gt; Next it sees we have await where promise is suppose to be resolved -&gt; So will it wait for promise to resolve and block call stack? No -&gt; thus handlePromise() execution get suspended and moved out of call stack -&gt; So when JS sees await keyword it suspend the execution of function till promise is resolved -&gt; So `p` will get resolved after 5 secs so handlePromise() will be pushed to call-stack again after 5 secs. -&gt; But this time it will start executing from where it had left. -&gt; Now it will log &#x27;Hello There!&#x27; and &#x27;Promise resolved value!!&#x27; -&gt; then it will check whether `p2` is resolved or not -&gt; It will find since `p2` will take 10 secs to resolve so the same above process will repeat -&gt; execution will be suspended until promise is resolved.</span>

<span class="hljs-comment">// 📌 Thus JS is not waiting, call stack is not getting blocked.</span>

<span class="hljs-comment">// Moreover in above scenario what if p1 would be taking 10 secs and p2 5 secs -&gt; even though p2 got resolved earlier but JS is synchronous single threaded language so it will first wait for p1 to be resolved and then will immediately execute all.</span></code></pre><h3 id="real-world-example-of-asyncawait"><a class="header-link" href="#real-world-example-of-asyncawait"></a>Real World example of async/await</h3>
<pre class="hljs"><code><span class="hljs-keyword">async</span> <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">handlePromise</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-comment">// fetch() =&gt; Response Object which as body as Readable stream =&gt; Response.json() is also a promise which when resolved =&gt; value</span>
  <span class="hljs-keyword">const</span> data = <span class="hljs-keyword">await</span> fetch(<span class="hljs-string">&#x27;https://api.github.com/users/alok722&#x27;</span>);
  <span class="hljs-keyword">const</span> res = <span class="hljs-keyword">await</span> data.json();
  <span class="hljs-built_in">console</span>.log(res);
};
handlePromise()</code></pre><h3 id="error-handling"><a class="header-link" href="#error-handling"></a>Error Handling</h3>
<p>While we were using normal Promise we were using .catch to handle error, now in <code>async-await</code> we would be using <code>try-catch</code> block to handle error.</p>
<pre class="hljs"><code><span class="hljs-keyword">async</span> <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">handlePromise</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-keyword">try</span> {
    <span class="hljs-keyword">const</span> data = <span class="hljs-keyword">await</span> fetch(<span class="hljs-string">&#x27;https://api.github.com/users/alok722&#x27;</span>);
    <span class="hljs-keyword">const</span> res = <span class="hljs-keyword">await</span> data.json();
    <span class="hljs-built_in">console</span>.log(res);
  } <span class="hljs-keyword">catch</span> (err) {
    <span class="hljs-built_in">console</span>.log(err)
  }
};
handlePromise()

<span class="hljs-comment">// In above whenever any error will occur the execution will move to catch block. One could try above with bad url which will result in error.</span>

<span class="hljs-comment">// Other way of handling error:</span>
handlePromise().catch(<span class="hljs-function"><span class="hljs-params">err</span> =&gt;</span> <span class="hljs-built_in">console</span>.log(err)); <span class="hljs-comment">// this will work as handlePromise will return error promise in case of failure.</span></code></pre><h3 id="async-await-vs-promisethencatch"><a class="header-link" href="#async-await-vs-promisethencatch"></a>Async await vs Promise.then/.catch</h3>
<p>What one should use? <code>async-await</code> is just a syntactic sugar around promise. Behind the scene <code>async-await</code> is just promise. So both are same, it&#39;s just <code>async-await</code> is new way of writing code. <code>async-await</code> solves few of the short-coming of Promise like <code>Promise Chaining</code>. <code>async-await</code> also increases the readability. So sort of it is always advisable to use <code>async-await.</code></p>
<hr>

<br>

<hr>

<h1 id="episode-24--promise-apis-all-allsettled-race-any--interview-questions-🔥"><a class="header-link" href="#episode-24--promise-apis-all-allsettled-race-any--interview-questions-🔥"></a>Episode 24 : Promise APIs (all, allSettled, race, any) + Interview Questions 🔥</h1>
<h3 id="-2"><a class="header-link" href="#-2"></a></h3>
<p>4 Promise APIs which are majorly used:</p>
<ul class="list">
<li>Promise.all()</li>
<li>Promise.allSettled()</li>
<li>Promise.race()</li>
<li>Promise.any()</li>
</ul>
<p>💡 One simply doesn&#39;t use async/await without knowing promises!</p>
<h3 id="promiseall"><a class="header-link" href="#promiseall"></a>Promise.all()</h3>
<blockquote>
<p>A promise is a placeholder for a value that&#39;s going to be available sometime later. The promise helps handle asynchronous operations. JavaScript provides a helper function Promise.all(promisesArrayOrIterable) to handle multiple promises at once, in parallel, and get the results in a single aggregate array.</p>
</blockquote>
<p>Q: In what situation one could use above api?<br>A: Suppose, you have to make parallel API call and get the result, how one can do? This is where Promise.all can be utilized. It is used to handle multiple promises together.</p>
<p>Promise.all([p1, p2, p3]) -&gt; Lets assume we are making 3 API call to fetch data. Also assume <strong>p1</strong> takes <strong>3 seconds</strong>, <strong>p2</strong> takes <strong>1 second</strong>, <strong>p3</strong> takes <strong>2 seconds</strong>.  </p>
<p>In first scenario let&#39;s assume all 3 promises are successful. So Promise.all will take <strong>3secs</strong> and will give promise value of result like [val1, val2, val3]. It will wait for all of them to finish then it will collect the results and give array as output.  </p>
<p>What if any of the promise gets rejected, for eg: Promise.all([p1, p2, p3]). But this time, p2 get rejected after 1 sec. Thus Promise.all will throw same error as p2 immediately as soon as error happened. It will not wait for other promise to either become success or failure. Moreover, p1 and p2 wont get cancelled as they are already triggered so it may result in success or failure depending upon their fate but Promise.all wont care. So its a situation of or/null.</p>
<p>💡 To conclude, the Promise.all() waits for all the input promises to resolve and returns a new promise that resolves to an array containing the results of the input promises. If one of the input promises is rejected, the Promise.all() method immediately returns a promise that is rejected with an error of the first rejected promise.</p>
<h3 id="promiseallsettled"><a class="header-link" href="#promiseallsettled"></a>Promise.allSettled()</h3>
<blockquote>
<p>Promise.allSettled() method that accepts a list of Promises and returns a new promise that resolves after all the input promises have settled, either resolved or rejected.</p>
</blockquote>
<p>Promise.allSettled([p1, p2, p3]) -&gt; Lets assume we are making 3 API call to fetch data. Also assume <strong>p1</strong> takes <strong>3 seconds</strong>, <strong>p2</strong> takes <strong>1 second</strong>, <strong>p3</strong> takes <strong>2 seconds</strong>.  </p>
<p>In first scenario let&#39;s assume all 3 promises are successful. So Promise.allSettled will take <strong>3secs</strong> and will give promise value of result like [val1, val2, val3]. It will wait for all of them to finish then it will collect the results and give array as output.  </p>
<p>What if any of the promise gets rejected, for eg: Promise.all([p1, p2, p3]). But this time, p2 get rejected after 1 sec. Thus Promise.allSettled will still wait for all promises to get settled. So After 3 secs, it will be [val1, err, val3]</p>
<p>💡 Promise.all() -&gt; Fail Fast<br>💡 Promise.allSettled() -&gt; Will wait and provide accumulative result</p>
<h3 id="promiserace"><a class="header-link" href="#promiserace"></a>Promise.race()</h3>
<blockquote>
<p>The Promise.race() static method accepts a list of promises as an iterable object and returns a new promise that fulfills or rejects as soon as there is one promise that fulfills or rejects, with the value or reason from that promise. The name of Promise.race() implies that all the promises race against each other with a single winner, either resolved or rejected.</p>
</blockquote>
<p>Promise.race([p1, p2, p3]) -&gt; Lets assume we are making 3 API call to fetch data. Also assume <strong>p1</strong> takes <strong>3 seconds</strong>, <strong>p2</strong> takes <strong>1 second</strong>, <strong>p3</strong> takes <strong>2 seconds</strong>.  So as soon as first promise will resolve or reject, it will give the output.  </p>
<p>So in Happy scenario, Promise.race will give (val2) as output after 1sec as p2 got resolved at the earliest. Whereas if it would have been failed Promise.race would have still given output after 1 sec but this time with error.</p>
<h3 id="promiseany"><a class="header-link" href="#promiseany"></a>Promise.any()</h3>
<blockquote>
<p>The Promise.any() method accepts a list of Promise objects as an iterable object. If one of the promises in the iterable object is fulfilled, the Promise.any() returns a single promise that resolves to a value which is the result of the fulfilled promise.</p>
</blockquote>
<p>Promise.any([p1, p2, p3]) -&gt; Lets assume we are making 3 API call to fetch data. Also assume <strong>p1</strong> takes <strong>3 seconds</strong>, <strong>p2</strong> takes <strong>1 second</strong>, <strong>p3</strong> takes <strong>2 seconds</strong>.  So as soon as first promise will be successful, it will give the output.</p>
<p>If in above situation what if p2 got rejected, nothing will happen as Promise.any seek for success, so the moment first success will happen that will become the result.</p>
<p>❓ But what if all promises got failed, so the returned result will be aggregated error i.e. [err1, err2, err3].</p>
<h2 id="code-examples"><a class="header-link" href="#code-examples"></a>Code Examples:</h2>
<h3 id="promiseall-1"><a class="header-link" href="#promiseall-1"></a>Promise.all()</h3>
<pre class="hljs"><code><span class="hljs-comment">// 📌 First Scenario</span>

<span class="hljs-keyword">const</span> p1 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    resolve(<span class="hljs-string">&#x27;P1 Success&#x27;</span>);
  }, <span class="hljs-number">3000</span>);
});
<span class="hljs-keyword">const</span> p2 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    resolve(<span class="hljs-string">&#x27;P2 Success&#x27;</span>);
  }, <span class="hljs-number">1000</span>);
});
<span class="hljs-keyword">const</span> p3 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    resolve(<span class="hljs-string">&#x27;P3 Success&#x27;</span>);
  }, <span class="hljs-number">2000</span>);
});

<span class="hljs-built_in">Promise</span>.all([p1, p2, p3]).then(<span class="hljs-function">(<span class="hljs-params">results</span>) =&gt;</span> {
  <span class="hljs-built_in">console</span>.log(results); <span class="hljs-comment">// [&#x27;P1 Success&#x27;, &#x27;P2 Success&#x27;, &#x27;P3 Success&#x27;] -&gt; took 3 secs</span>
});</code></pre><pre class="hljs"><code><span class="hljs-comment">// 📌 Second Scenario</span>


<span class="hljs-keyword">const</span> p1 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    resolve(<span class="hljs-string">&#x27;P1 Success&#x27;</span>);
  }, <span class="hljs-number">3000</span>);
});
<span class="hljs-keyword">const</span> p2 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    reject(<span class="hljs-string">&#x27;P2 Fail&#x27;</span>);
  }, <span class="hljs-number">1000</span>);
});
<span class="hljs-keyword">const</span> p3 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    resolve(<span class="hljs-string">&#x27;P3 Success&#x27;</span>);
  }, <span class="hljs-number">2000</span>);
});

<span class="hljs-built_in">Promise</span>.all([p1, p2, p3])
  .then(<span class="hljs-function"><span class="hljs-params">results</span> =&gt;</span> <span class="hljs-built_in">console</span>.log(results))
  .catch(<span class="hljs-function"><span class="hljs-params">err</span> =&gt;</span> <span class="hljs-built_in">console</span>.error(err)); <span class="hljs-comment">// throws error after 1 sec i.e. &#x27;P2 Fails&#x27;</span></code></pre><h3 id="promiseallsettled-1"><a class="header-link" href="#promiseallsettled-1"></a>Promise.allSettled()</h3>
<p>💡This is safest among all Promises API.</p>
<pre class="hljs"><code><span class="hljs-keyword">const</span> p1 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    resolve(<span class="hljs-string">&#x27;P1 Success&#x27;</span>);
  }, <span class="hljs-number">3000</span>);
});
<span class="hljs-keyword">const</span> p2 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    resolve(<span class="hljs-string">&#x27;P2 Success&#x27;</span>);
  }, <span class="hljs-number">1000</span>);
});
<span class="hljs-keyword">const</span> p3 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    reject(<span class="hljs-string">&#x27;P3 Fail&#x27;</span>);
  }, <span class="hljs-number">2000</span>);
});

<span class="hljs-built_in">Promise</span>.allSettled([p1, p2, p3])
  .then(<span class="hljs-function">(<span class="hljs-params">results</span>) =&gt;</span> <span class="hljs-built_in">console</span>.log(results))
  .catch(<span class="hljs-function"><span class="hljs-params">err</span> =&gt;</span> <span class="hljs-built_in">console</span>.error(err));

<span class="hljs-comment">// Over here, it will wait for all promises to be either settled or rejected and then return,</span>
  <span class="hljs-comment">/*
    [
      {status: &#x27;fulfilled&#x27;, value: &#x27;P1 Success&#x27;},
      {status: &#x27;fulfilled&#x27;, value: &#x27;P2 Success&#x27;},
      {status: &#x27;rejected&#x27;, reason: &#x27;P3 Fail&#x27;}
    ]
  */</span></code></pre><h3 id="promiserace-1"><a class="header-link" href="#promiserace-1"></a>Promise.race()</h3>
<pre class="hljs"><code><span class="hljs-comment">// 📌 First Scenario</span>

<span class="hljs-keyword">const</span> p1 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    resolve(<span class="hljs-string">&#x27;P1 Success&#x27;</span>);
  }, <span class="hljs-number">3000</span>);
});
<span class="hljs-keyword">const</span> p2 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    resolve(<span class="hljs-string">&#x27;P2 Success&#x27;</span>);
  }, <span class="hljs-number">1000</span>);
});
<span class="hljs-keyword">const</span> p3 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    reject(<span class="hljs-string">&#x27;P3 Fail&#x27;</span>);
  }, <span class="hljs-number">2000</span>);
});

<span class="hljs-built_in">Promise</span>.race([p1, p2, p3])
  .then(<span class="hljs-function">(<span class="hljs-params">results</span>) =&gt;</span> <span class="hljs-built_in">console</span>.log(results))
  .catch(<span class="hljs-function"><span class="hljs-params">err</span> =&gt;</span> <span class="hljs-built_in">console</span>.error(err));

 <span class="hljs-comment">// It will return as soon as first promise is resolved or rejected.</span>
 <span class="hljs-comment">// In above example O/P: &quot;P2 Success&quot;</span></code></pre><pre class="hljs"><code><span class="hljs-comment">// 📌 Second Scenario</span>

<span class="hljs-keyword">const</span> p1 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    resolve(<span class="hljs-string">&#x27;P1 Success&#x27;</span>);
  }, <span class="hljs-number">3000</span>);
});
<span class="hljs-keyword">const</span> p2 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    resolve(<span class="hljs-string">&#x27;P2 Success&#x27;</span>);
  }, <span class="hljs-number">5000</span>);
});
<span class="hljs-keyword">const</span> p3 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    reject(<span class="hljs-string">&#x27;P3 Fail&#x27;</span>);
  }, <span class="hljs-number">2000</span>);
});

<span class="hljs-built_in">Promise</span>.race([p1, p2, p3])
  .then(<span class="hljs-function">(<span class="hljs-params">results</span>) =&gt;</span> <span class="hljs-built_in">console</span>.log(results))
  .catch(<span class="hljs-function"><span class="hljs-params">err</span> =&gt;</span> <span class="hljs-built_in">console</span>.error(err));

 <span class="hljs-comment">//After 2 secs O/P: &quot;P3 Fail&quot;</span></code></pre><p>Notes:  </p>
<ul class="list">
<li>Once promise is settled, it means -&gt; got the result. Moreover, settled is broadly divided into two categories:</li>
</ul>
<ol class="list">
<li>resolve, success, fulfilled</li>
<li>reject, failure, rejected</li>
</ol>
<h3 id="promiseany-1"><a class="header-link" href="#promiseany-1"></a>Promise.any()</h3>
<pre class="hljs"><code><span class="hljs-comment">// 📌 First Scenario</span>

<span class="hljs-keyword">const</span> p1 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    resolve(<span class="hljs-string">&#x27;P1 Success&#x27;</span>);
  }, <span class="hljs-number">3000</span>);
});
<span class="hljs-keyword">const</span> p2 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    resolve(<span class="hljs-string">&#x27;P2 Success&#x27;</span>);
  }, <span class="hljs-number">5000</span>);
});
<span class="hljs-keyword">const</span> p3 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    reject(<span class="hljs-string">&#x27;P3 Fail&#x27;</span>);
  }, <span class="hljs-number">2000</span>);
});

<span class="hljs-built_in">Promise</span>.any([p1, p2, p3])
  .then(<span class="hljs-function">(<span class="hljs-params">results</span>) =&gt;</span> <span class="hljs-built_in">console</span>.log(results))
  .catch(<span class="hljs-function"><span class="hljs-params">err</span> =&gt;</span> <span class="hljs-built_in">console</span>.error(err));

<span class="hljs-comment">// It will wait for first settled **success**</span>
<span class="hljs-comment">// In above, p3 will settled first, but since it is rejected, so it will wait further so at 3rd second it will print &quot;P1 Success&quot;</span></code></pre><pre class="hljs"><code><span class="hljs-comment">// 📌 Second Scenario</span>

<span class="hljs-keyword">const</span> p1 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    reject(<span class="hljs-string">&#x27;P1 Fail&#x27;</span>);
  }, <span class="hljs-number">3000</span>);
});
<span class="hljs-keyword">const</span> p2 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    resolve(<span class="hljs-string">&#x27;P2 Success&#x27;</span>);
  }, <span class="hljs-number">5000</span>);
});
<span class="hljs-keyword">const</span> p3 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    reject(<span class="hljs-string">&#x27;P3 Fail&#x27;</span>);
  }, <span class="hljs-number">2000</span>);
});

<span class="hljs-built_in">Promise</span>.any([p1, p2, p3])
  .then(<span class="hljs-function">(<span class="hljs-params">results</span>) =&gt;</span> <span class="hljs-built_in">console</span>.log(results))
  .catch(<span class="hljs-function"><span class="hljs-params">err</span> =&gt;</span> <span class="hljs-built_in">console</span>.error(err));

<span class="hljs-comment">// After 5 secs: &#x27;P2 Success&#x27;</span></code></pre><pre class="hljs"><code><span class="hljs-comment">// 📌 Third Scenario</span>

<span class="hljs-keyword">const</span> p1 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    reject(<span class="hljs-string">&#x27;P1 Fail&#x27;</span>);
  }, <span class="hljs-number">3000</span>);
});
<span class="hljs-keyword">const</span> p2 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    reject(<span class="hljs-string">&#x27;P2 Fail&#x27;</span>);
  }, <span class="hljs-number">5000</span>);
});
<span class="hljs-keyword">const</span> p3 = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
  <span class="hljs-built_in">setTimeout</span>(<span class="hljs-function">() =&gt;</span> {
    reject(<span class="hljs-string">&#x27;P3 Fail&#x27;</span>);
  }, <span class="hljs-number">2000</span>);
});

<span class="hljs-built_in">Promise</span>.any([p1, p2, p3])
  .then(<span class="hljs-function">(<span class="hljs-params">results</span>) =&gt;</span> <span class="hljs-built_in">console</span>.log(results))
  .catch(<span class="hljs-function"><span class="hljs-params">err</span> =&gt;</span> {
    <span class="hljs-built_in">console</span>.error(err);
    <span class="hljs-built_in">console</span>.error(err.errors); <span class="hljs-comment">// [&#x27;P1 Fail&#x27;, &#x27;P2 Fail&#x27;, &#x27;P3 Fail&#x27;]</span>
  });

<span class="hljs-comment">// Since all are rejected, so it will give &quot;aggregate error&quot; as output</span>
<span class="hljs-comment">// AggregateError: All promises were rejected</span>
<span class="hljs-comment">// To get AggregateError array you need to write &quot;err.errors&quot;</span></code></pre><h3 id="summary"><a class="header-link" href="#summary"></a>Summary</h3>
<p>There are 6 static methods of Promise class:</p>
<blockquote>
<p>Promise.all(promises) – waits for all promises to resolve and returns an array of their results. If any of the given promises rejects, it becomes the error of Promise.all, and all other results are ignored.</p>
</blockquote>
<blockquote>
<p>Promise.allSettled(promises) (recently added method) – waits for all promises to settle and returns their results as an array of objects with:
status: &quot;fulfilled&quot; or &quot;rejected&quot;
value (if fulfilled) or reason (if rejected).</p>
</blockquote>
<blockquote>
<p>Promise.race(promises) – waits for the first promise to settle, and its result/error becomes the outcome.</p>
</blockquote>
<blockquote>
<p>Promise.any(promises) (recently added method) – waits for the first promise to fulfill, and its result becomes the outcome. If all of the given promises are rejected, AggregateError becomes the error of Promise.any.</p>
</blockquote>
<blockquote>
<p>Promise.resolve(value) – makes a resolved promise with the given value.</p>
</blockquote>
<blockquote>
<p>Promise.reject(error) – makes a rejected promise with the given error.
Of all these, Promise.all is probably the most common in practice.</p>
</blockquote>
<hr>

<br>

<hr>

<h1 id="episode-25--this-keyword-in-javascript"><a class="header-link" href="#episode-25--this-keyword-in-javascript"></a>Episode 25 : <code>this</code> keyword in JavaScript</h1>
<h3 id="-3"><a class="header-link" href="#-3"></a></h3>
<blockquote>
<p>In JavaScript, the this keyword refers to an object, which object depends on how this is being invoked (used or called).</p>
</blockquote>
<h2 id="this-in-global-space"><a class="header-link" href="#this-in-global-space"></a><code>this</code> in global space</h2>
<p>Anything defined globally is said to be in a global space.</p>
<pre class="hljs"><code><span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>); <span class="hljs-comment">// refers to global object i.e. window in case of browser</span>
<span class="hljs-comment">// 💡 global object differs based on runtime environment,</span></code></pre><h2 id="this-inside-a-function"><a class="header-link" href="#this-inside-a-function"></a><code>this</code> inside a function</h2>
<pre class="hljs"><code><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">x</span>(<span class="hljs-params"></span>) </span>{
    <span class="hljs-comment">// the below value depends on strict/non-strict mode</span>
    <span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>);
    <span class="hljs-comment">// in strict mode - undefined</span>
    <span class="hljs-comment">// in non-strict mode - refers to global window object</span>
}
x();
<span class="hljs-comment">// 💡 Notes:</span>

<span class="hljs-comment">// On the first go feels like `this` keyword in global space and inside function behaves same but in reality it&#x27;s different.</span>

<span class="hljs-comment">// The moment you make JS run in strict mode by using: &quot;use strict&quot; at the top, `this` keyword inside function returns `undefined` whereas global space will still refers to global window object</span></code></pre><p><code>this substitution</code> -&gt; According to <code>this</code> substitution, if the value of <code>this</code> keyword is <code>null/undefined</code>, it will be replaced by globalObject only in non-strict mode. This is the reason why <code>this</code> refers to global window object inside function in non-strict mode.</p>
<p>💡 So to summarize, the value of <code>this</code> keyword inside function is <code>undefined</code>, but because of <code>this substitution</code> in non-strict mode <code>this</code> keyword refers to <code>globalWindowObject</code> and in strict mode it will still be <code>undefined</code></p>
<p><code>this</code> keyword value depends on how the <code>function</code> is called. For eg:<br>In strict mode:  </p>
<pre class="hljs"><code>x(); <span class="hljs-comment">// undefined  </span>
<span class="hljs-built_in">window</span>.x(); <span class="hljs-comment">// global window object</span></code></pre><h2 id="this-inside-a-objects-method"><a class="header-link" href="#this-inside-a-objects-method"></a><code>this</code> inside a object&#39;s method</h2>
<pre class="hljs"><code><span class="hljs-comment">// `x` key below is a method as per terminology</span>
<span class="hljs-keyword">const</span> obj = {
    <span class="hljs-attr">a</span>: <span class="hljs-number">10</span>,
    <span class="hljs-attr">x</span>: <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{
        <span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>); <span class="hljs-comment">// {a: 10, x: f()}</span>
        <span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>.a); <span class="hljs-comment">// 10</span>
    }
}
obj.x(); <span class="hljs-comment">// value of `this` is referring to current object i.e. `obj`</span></code></pre><h2 id="call-apply--bind-methods"><a class="header-link" href="#call-apply--bind-methods"></a><code>call</code>, <code>apply</code> &amp; <code>bind</code> methods</h2>
<blockquote>
<p>For detail around call, apply and bind method. Refer <a href="https://www.youtube.com/watch?v=75W8UPQ5l7k&ab_channel=AkshaySaini">here</a>.</p>
</blockquote>
<pre class="hljs"><code><span class="hljs-keyword">const</span> student = {
    <span class="hljs-attr">name</span>: <span class="hljs-string">&#x27;Alok&#x27;</span>,
    <span class="hljs-attr">printName</span>: <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{
        <span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>.name);
    }
}
student.printName(); <span class="hljs-comment">// Alok</span>

<span class="hljs-keyword">const</span> student2 = {
    <span class="hljs-attr">name</span>: <span class="hljs-string">&#x27;Kajal&#x27;</span>,
}
student2.printName(); <span class="hljs-comment">// throw error</span>

<span class="hljs-comment">// ❓ how to re-use printName method from `student` object</span>
student.printName.call(student2); <span class="hljs-comment">// Kajal</span>
<span class="hljs-comment">// Above `call` method is taking the value of `this` keyword</span>
<span class="hljs-comment">// So, Inside `printName` method value of `this` is now `student2` object</span>

<span class="hljs-comment">// So, call, bind and apply is used to set the value of this keyword.</span></code></pre><h2 id="this-inside-arrow-function"><a class="header-link" href="#this-inside-arrow-function"></a><code>this</code> inside arrow function</h2>
<p>Arrow function doesn&#39;t have their own <code>this</code> value, they take the value from enclosing lexical context.</p>
<pre class="hljs"><code><span class="hljs-keyword">const</span> obj = {
    <span class="hljs-attr">a</span>: <span class="hljs-number">10</span>,
    <span class="hljs-attr">x</span>: <span class="hljs-function">() =&gt;</span> {
        <span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>); <span class="hljs-comment">// window object</span>
        <span class="hljs-comment">// Above the value of `this` won&#x27;t be obj anymore instead it will be enclosing lexical context i.e. window object in current scenario.</span>
    }
}
obj.x();

<span class="hljs-keyword">const</span> obj2 = {
    <span class="hljs-attr">a</span>: <span class="hljs-number">10</span>,
    <span class="hljs-attr">x</span>: <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{
        <span class="hljs-keyword">const</span> y = <span class="hljs-function">() =&gt;</span> {
            <span class="hljs-built_in">console</span>.log(<span class="hljs-built_in">this</span>);
            <span class="hljs-comment">// Above the value of `this` will be obj2 as function y&#x27;s enclosing lexical context is function `x`.</span>
        };
        y();
    }
}
obj2.x();</code></pre><h2 id="this-inside-dom"><a class="header-link" href="#this-inside-dom"></a><code>this</code> inside DOM</h2>
<blockquote>
<p>It refers to HTML element.</p>
</blockquote>
<pre class="hljs"><code><span class="hljs-tag">&lt;<span class="hljs-name">button</span> <span class="hljs-attr">onclick</span>=<span class="hljs-string">&quot;alert(this)&quot;</span>&gt;</span>Click Me<span class="hljs-tag">&lt;/<span class="hljs-name">button</span>&gt;</span>
<span class="hljs-comment">&lt;!-- [object HTMLButtonElement] Button element --&gt;</span></code></pre><hr>

<p>To Be Continued...</p>
</body>
</html>