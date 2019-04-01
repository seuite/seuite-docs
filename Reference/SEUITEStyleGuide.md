# SEUITE 文档写作规范

本规范适用于所有SEUITE文档，若文档内有特殊要求，以文档内为准

## RFC2119
关键字 "必须"，"禁止"，"被要求"，"应当"，"不应"，"推荐"，"可以"，"可选" 均遵循[RFC 2119](http://tools.ietf.org/html/rfc2119)要求，对原文的翻译和本地化，你可以在[RFC2119中文译本](/Reference/RFC2119)中找到相关内容

### SEUITE对RFC2119使用的解释

原目录中关键字 "SHALL" 与 "SHALL NOT" 无中文对应译名，在SEUITE文档中舍弃不用

## 写作风格

**推荐**使用微软写作格式写作，参见[Microsoft Style Guide](https://docs.microsoft.com/en-us/style-guide/welcome/)

对部分原文档的摘要和翻译，参见[微软写作风格指南摘要及中文译本（部分）](/arch/MicrosoftStyleGuide)

此外，推荐阅读如下：

1. [Microsoft's brand voice: Above all, simple and human](https://docs.microsoft.com/en-us/style-guide/brand-voice-above-all-simple-human)
2. [Scannable content](https://docs.microsoft.com/en-us/style-guide/scannable-content/index)
3. [Punctuation](https://docs.microsoft.com/en-us/style-guide/punctuation/index)
4. [Capitalization](https://docs.microsoft.com/en-us/style-guide/capitalization)
5. [Word choice](https://docs.microsoft.com/en-us/style-guide/word-choice/index)


## 标点符号

**可以**参考国家标准GB/T 15834-2011《标点符号用法》

### SEUITE对标点符号使用的要求
- 以下标点符号**必须**使用半角符号   
    - 单引号 ' 和双引号 "   
    - 中括号 [ ]      
    - 空格
- 标点符号之间不应加上空格      
- 同一内容块中的同一标点符号应格式一致     
- 代码块中**禁止**使用全角符号

## 代码规范

https://google.github.io/styleguide/

http://checkstyle.sourceforge.net/config.html

什么大括号怎么摆啊、缩进怎么缩啊，全是浮云，闲的蛋疼才去关心这些。

真正体现好代码的地方应该是定义清晰明确、边界清楚、复用性高。当你需要修改一个功能的时候最好只需要改这个功能本身，而不用连带着考虑一串其他相关模块。而且最好是在类型和接口的定义中就把逻辑交代清楚，要么就不能编译或者不能用，要么一定正确，不要给误用留下空间然后处处小心用代码逻辑去填这个坑。

## 版本管理

遵照[SemVer2.0](http://semver.org/)要求进行，对原文的翻译和本地化，见[语义化版本控制2.0](/Reference/SemVerReference)

### SEUITE 对附加版本号的相关解释

- Alpha版(内部测试版)：一般只在软件开发组织内部运行，不对外公开。主要是开发者自己对产品进行测试，检查产品是否存在缺陷、错误，验证产品功能与说明书、用户手册是否一致。　　
- Beta版(外部测试版)：非正式版本，免费发送给具有典型性的用户，让用户测试该软件的不足之处及存在问题，以便在正式发行前进一步改进和完善。该版本一般可通过Internet免费下载。　　 
- Demo版(演示版)：演示正式软件的部分功能的非正式版本，用户可以从中得知软件的基本操作，该版本一般可通过Internet免费下载。　　 　　 　　 
