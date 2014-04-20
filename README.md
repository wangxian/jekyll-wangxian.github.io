声明
=============

这是木頭的个人博客，_post文件夹中所有文章版权归我所有，未经允许不得转载！

有任何问题请联系我: wo#wangxian.me(#->@)

----------------------------------------------------------------

rake Tips
=========================================

rake server [default]
rake post
rake reset

Sample Markdown Cheat Sheet
=========================================

## highlight code
### code 1
    {% highlight javascript linenos %}
    {
      events: { },
      handle: function(e){ }
    }
    {% endhighlight %}



### code 2
    var now = new Date();
    console.log( now.toString() )


### code 3
`code block`


## Indentation
> Here is some indented text
>> even more indented
>> xx bb

## Text basics
this is *italic* and this is **bold** .
another _italic_ and another __bold__


## Example lists

### Unordered list
+ bullet list
  - sub1
  * sub2
  + sub3
- bullet list
* bullet list

### Ordered list
1. 1111
2. 2222
3. 3333
4. 4444
  1. 2222
  2. 3333
  3. 4444


## link
[link](http://url.com/)
<http://url.com>

[url.com][ref]
[ref]: http://url.com

<http://url.com>

## img
![logo](http://backbonejs.org/docs/images/backbone.png "image alt")


## h1 ~ h6 examples
# Big title (h1)
## Middle title (h2)
### Smaller title (h3)
#### and so on (h4)
##### and so on (h5)
###### and so on (h6)
