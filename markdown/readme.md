---
title: "Markdown"
permalink: "/markdown"
layout: default
---



#### hello there!

This page will be used as a documentation on markdown (lightweight markup language).
This is my personal "guide" that I made while exploring the syntaxe, and if you need help you should check the [Markdown Guide](https://www.markdownguide.org/) or a [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet).

-------

| Elements                              |       How to                                                  |      Notes      
| :------:                              |       :------:                                                |      ------     
| [Italic](#italic)                     |      \_Text\_                                                 |                 
| [Bold](#bold)                         |     \*\*Text\*\*                                              |                 
| [Headers](#headers)                   |     \# Header 1                                               |   not recommended to use big headers             
|                                       |     \## Header 2                                              |   better to just use \#\# like a content table              
|                                       |     \###### Header 6                                          |   and then \# where you want to point to              
| [Inline Link](#inline-link)           |     \[Text](link)                                             |                 |
| [Reference Link](#reference-link)     |     \[Text][reference]   \[reference]:link                    |   this seems useful for lots of the same link            
| [Inline Image Link](#inline-image)    |     \!\[Alt Text](link)                                       |   to display an image which is in the repository, use relative links instead of absolute links.   
| [Reference Image](#reference-image):  |     \[Alt Text][reference]                                    |    \[reference]:link  ([same as without image](#reference-link))        
| [Quote Block](#quote-block)           |     \> Text                                                   |   usefull to highlight a snippet of text from the rest              
| [Unordered List](#unordered-list)     |     \* Item                                                   |                 
| [Ordered List](#ordered-list)         |     1. Item                                                   |                 
| [Line Break](#line-break)             |     2 spaces end of line                                      |   it can be good for lists but doesn't work well on tables             
| [Code Block](#code-block)             |     2 TABS or 4 spaces                                        |   it's a good idea to indent the code!              
| [Horizontal Bar](#horizontal-bar)     |     \----------                                               |   a thinner is created on "headers" so it's not that useful             

## italic  
_Emphasis, aka italics, with *asterisks* or _underscores_._
## bold  
**Strong emphasis, aka bold, with **asterisks** or __underscores__.**
## headers  
# H1
## H2
###### H6
## inline-link 
[My Github Page](https://github.com/NinjaSpottedCoding/Main-Page)
## reference-link
[My Website][website]
## inline-image
Same result as reference
## reference-image
![My Avatar](/markdown/105322822.png "Original Avatar")
<!--- ![My Avatar][avatar] -->
## quote-block
> This is a quote  
## unordered-list
* Milk
* Eggs
* Cookies  
## ordered-list
1. Gold
2. Silver
3. Bronze  
Bronze is underatted  
# line-break
How are you here?  
That's pretty awesome!  
## code-block
    fn main() {
      println!("Hello, world!");
    }  
## horizontal-bar
---------  
[avatar]:/markdown/105322822.png
[website]:https://ninjaspottedcoding.github.io/Main-Page/

Thank you for finding this page, and remember to check out the resources used on this document, or others more directed to help learn how to use Markdown!  
This page was written in 12/5/2022 and last updated in 06/06/2022.
