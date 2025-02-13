# kupietests-ai-coding-assistants-1
## Buggy php code to test the debugging and code refactoring abilities of AI coding assistants. 

*This is the first in an eventual series of tests of online services, documenting my long history of finding ways to break things.*

I wrote one-file wordpress plugin that contains javascript in a HEREDOC format. When the plugin is first activated, the javascript is exported to a .js file which the plugin then enqueues in normal use. 

The Javascript code contains `${varname}` template literals. On activation, the PHP interpreter misinterprets these as PHP variables, not as JS literals to be included as part of the HEREDOC, causing a fatal error.

So, my test (which I've subjected several AIs to) is to supply the AI with the plugin code, plus the line of the PHP error log giving the fatal error and the line it occurs on. 

Ideally, the AI would recognize and fix the entire problem, including all template literals, by refactoring them to use ordinary strings and concatenation in the javascript code.

Some results:

**Zencoder** did successfully fix the sole instance of the error that triggered the first fatal error, but nothing else. So I told it to fix the rest. It said that it did, but left some unfixed. I told it it had left some unfixed, and went through again and said it fixed everything, but some were still unfixed. At that point, I had spent longer than it would have taken me to correct the template literals by hand, so, I called it a fail.

**Claude 3.5 Sonnet** spotted and fixed the problem immediately, and silently removed a bunch of the javascript code needed for all the plugin features to work correctly. 

**ChatGPT 4o**, after repeated cajoling, eventually figued out that the problem was the template literals, and repeatedly eviscerated the entire plugin, mangling and deleting the majority of the code while insisting it was preserving all code and functionality and just fixing the errors. 
