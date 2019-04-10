<h1 id="highlight.js">Highlight.js</h1>

<p>Highlight.js нужен для подсветки синтаксиса в примерах кода в блогах,
форумах и вообще на любых веб-страницах. Пользоваться им очень просто,
потому что работает он автоматически: сам находит блоки кода, сам
определяет язык, сам подсвечивает.</p>

<p>Автоопределением языка можно управлять, когда оно не справляется само (см.
дальше "Эвристика").</p>

<h2 id="%F0%9F%F1%80%F0%BE%F1%81%F1%82%F0%BE%F0%B5-%F0%B8%F1%81%F0%BF%F0%BE%F0%BB%F1%8C%F0%B7%F0%BE%F0%B2%F0%B0%F0%BD%F0%B8%F0%B5">Простое использование</h2>

<p>Подключите библиотеку и стиль на страницу и повесть вызов подсветки на
загрузку страницы:</p>

<pre><code class="html">&lt;link rel="stylesheet" href="styles/default.css"&gt;
&lt;script src="highlight.pack.js"&gt;&lt;/script&gt;
&lt;script&gt;hljs.initHighlightingOnLoad();&lt;/script&gt;
</code></pre>

<p>Весь код на странице, обрамлённый в теги <code>&lt;pre&gt;&lt;code&gt; .. &lt;/code&gt;&lt;/pre&gt;</code>
будет автоматически подсвечен. Если вы используете другие теги или хотите
подсвечивать блоки кода динамически, читайте "Инициализацию вручную" ниже.</p>

<ul>
<li><p>Вы можете скачать собственную версию "highlight.pack.js" или сослаться
на захостенный файл, как описано на странице загрузки:
<a href="http://softwaremaniacs.org/soft/highlight/download/">http://softwaremaniacs.org/soft/highlight/download/</a></p></li>
<li><p>Стилевые темы можно найти в загруженном архиве или также использовать
захостенные. Чтобы сделать собственный стиль для своего сайта, вам
будет полезен справочник классов в файле <a href="http://github.com/isagalaev/highlight.js/blob/master/classref.txt">classref.txt</a>, который тоже
есть в архиве.</p></li>
</ul>

<h2 id="node.js">node.js</h2>

<p>Highlight.js можно использовать в node.js. Библиотеку со всеми возможными языками можно
установить с NPM:</p>

<pre><code>npm install highlight.js
</code></pre>

<p>Также её можно собрать из исходников с только теми языками, которые нужны:</p>

<pre><code>python tools/build.py -tnode lang1 lang2 ..
</code></pre>

<p>Использование библиотеки:</p>

<pre><code class="javascript">var hljs = require('highlight.js');

// Если вы знаете язык
hljs.highlight(lang, code).value;

// Автоопределение языка
hljs.highlightAuto(code).value;
</code></pre>

<h2 id="%F0%97%F0%B0%F0%BC%F0%B5%F0%BD%F0%B0-tab%F0%BE%F0%B2">Замена TABов</h2>

<p>Также вы можете заменить символы TAB ('\x09'), используемые для отступов, на
фиксированное количество пробелов или на отдельный <code>&lt;span&gt;</code>, чтобы задать ему
какой-нибудь специальный стиль:</p>

<pre><code class="html">&lt;script type="text/javascript"&gt;
  hljs.tabReplace = '    '; // 4 spaces
  // ... or
  hljs.tabReplace = '&lt;span class="indent"&gt;\t&lt;/span&gt;';

  hljs.initHighlightingOnLoad();
&lt;/script&gt;
</code></pre>

<h2 id="%F0%98%F0%BD%F0%B8%F1%86%F0%B8%F0%B0%F0%BB%F0%B8%F0%B7%F0%B0%F1%86%F0%B8%F1%8F-%F0%B2%F1%80%F1%83%F1%87%F0%BD%F1%83%F1%8E">Инициализация вручную</h2>

<p>Если вы используете другие теги для блоков кода, вы можете инициализировать их
явно с помощью функции <code>highlightBlock(code, tabReplace, useBR)</code>. Она принимает
DOM-элемент с текстом расцвечиваемого кода и опционально - строчку для замены
символов TAB.</p>

<p>Например с использованием jQuery код инициализации может выглядеть так:</p>

<pre><code class="javascript">$(document).ready(function() {
  $('pre code').each(function(i, e) {hljs.highlightBlock(e)});
});
</code></pre>

<p><code>highlightBlock</code> можно также использовать, чтобы подсветить блоки кода,
добавленные на страницу динамически. Только убедитесь, что вы не делаете этого
повторно для уже раскрашенных блоков.</p>

<p>Если ваш блок кода использует <code>&lt;br&gt;</code> вместо переводов строки (т.е. если это не
<code>&lt;pre&gt;</code>), передайте <code>true</code> третьим параметром в <code>highlightBlock</code>:</p>

<pre><code class="javascript">$('div.code').each(function(i, e) {hljs.highlightBlock(e, null, true)});
</code></pre>

<h2 id="%F0%AD%F0%B2%F1%80%F0%B8%F1%81%F1%82%F0%B8%F0%BA%F0%B0">Эвристика</h2>

<p>Определение языка, на котором написан фрагмент, делается с помощью
довольно простой эвристики: программа пытается расцветить фрагмент всеми
языками подряд, и для каждого языка считает количество подошедших
синтаксически конструкций и ключевых слов. Для какого языка нашлось больше,
тот и выбирается.</p>

<p>Это означает, что в коротких фрагментах высока вероятность ошибки, что
периодически и случается. Чтобы указать язык фрагмента явно, надо написать
его название в виде класса к элементу <code>&lt;code&gt;</code>:</p>

<pre><code class="html">&lt;pre&gt;&lt;code class="html"&gt;...&lt;/code&gt;&lt;/pre&gt;
</code></pre>

<p>Можно использовать рекомендованные в HTML5 названия классов:
"language-html", "language-php". Также можно назначать классы на элемент
<code>&lt;pre&gt;</code>.</p>

<p>Чтобы запретить расцветку фрагмента вообще, используется класс "no-highlight":</p>

<pre><code class="html">&lt;pre&gt;&lt;code class="no-highlight"&gt;...&lt;/code&gt;&lt;/pre&gt;
</code></pre>

<h2 id="%F0%AD%F0%BA%F1%81%F0%BF%F0%BE%F1%80%F1%82">Экспорт</h2>

<p>В файле export.html находится небольшая программка, которая показывает и дает
скопировать непосредственно HTML-код подсветки для любого заданного фрагмента кода.
Это может понадобится например на сайте, на котором нельзя подключить сам скрипт
highlight.js.</p>

<h2 id="%F0%9A%F0%BE%F0%BE%F1%80%F0%B4%F0%B8%F0%BD%F0%B0%F1%82%F1%8B">Координаты</h2>

<ul>
<li>Версия: 7.3</li>
<li>URL:    http://softwaremaniacs.org/soft/highlight/</li>
<li>Автор:  Иван Сагалаев (<a href="&#109;&#x61;&#105;&#x6c;&#116;&#x6f;:&#109;&#x61;&#110;&#x69;&#97;&#x63;&#64;&#x73;o&#102;&#x74;&#119;&#x61;&#114;&#x65;&#109;&#x61;&#x6e;&#105;&#x61;&#99;&#x73;&#46;&#x6f;r&#103;">&#109;&#x61;&#110;&#x69;&#97;&#x63;&#64;&#x73;o&#102;&#x74;&#119;&#x61;&#114;&#x65;&#109;&#x61;&#x6e;&#105;&#x61;&#99;&#x73;&#46;&#x6f;r&#103;</a>)</li>
</ul>

<p>Лицензионное соглашение читайте в файле LICENSE.
Список соавторов читайте в файле AUTHORS.ru.txt</p>
