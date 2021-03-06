
1. xss攻击的基本概念

* XSS是跨站脚本攻击（Cross-Site Scripting）的简称，它是个老油条了，在OWASP Web Application Top 10排行榜中长期霸榜，从未掉出过前三名。XSS这类安全问题发生的本质原因在于，浏览器错误的将攻击者提供的用户输入数据当做JavaScript脚本给执行了。

* XSS有几种不同的分类办法，例如按照恶意输入的脚本是否在应用中存储，XSS被划分为“存储型XSS”和“反射型XSS”，如果按照是否和服务器有交互，又可以划分为“Server Side XSS”和“DOM based XSS”。

* 无论怎么分类，XSS漏洞始终是威胁用户的一个安全隐患。攻击者可以利用XSS漏洞来窃取包括用户身份信息在内的各种敏感信息、修改Web页面以欺骗用户，甚至控制受害者浏览器，或者和其他漏洞结合起来形成蠕虫攻击，等等。总之，关于XSS漏洞的利用，只有想不到没有做不到。


2. 如何防御

* 防御XSS最佳的做法就是对数据进行严格的输出编码，使得攻击者提供的数据不再被浏览器认为是脚本而被误执行。例如<script>在进行HTML编码后变成了&lt;script&gt;，而这段数据就会被浏览器认为只是一段普通的字符串，而不会被当做脚本执行了。

* 编码也不是件容易的事情，需要根据输出数据所在的上下文来进行相应的编码。例如刚才的例子，由于数据将被放置于HTML元素中，因此进行的是HTML编码，而如果数据将被放置于URL中，则需要进行URL编码，将其变为%3Cscript%3E。此外，还有JavaScript编码、CSS编码、HTML属性编码、JSON编码等等。好在现如今的前端开发框架基本上都默认提供了前端输出编码，这大大减轻了前端开发小伙伴们的工作负担。

* 其他的防御措施，例如设置CSP HTTP Header、输入验证、开启浏览器XSS防御等等都是可选项，原因在于这些措施都存在被绕过的可能，并不能完全保证能防御XSS攻击。不过它们和输出编码却可以共同协作实施纵深防御策略。