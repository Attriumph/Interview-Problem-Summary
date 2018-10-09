# HTML
## HTML Semantic
Semantic HTML is HTML that introduces meaning to the web page rather than just presentation. For example, a <p> tag indicates that the enclosed text is a paragraph. This is both semantic and presentational, because people know what paragraphs are and browsers know how to display them. In HTML4, tags like < b > and < i > are not semantic, because they define only how the text should look (bold or italic) and do not provide any additional meaning.
Examples of semantic HTML tags include the header tags '< h1 > through < h6 >, < blockquote >, < code > and < em >'. There are many more semantic HTML tags.

### Why Semantic HTML is Important
1. semantic code aids accessibility. Specially, many people whose eyes are not good rely on speech browsers to read pages to them. These programs cannot interpret pages very well unless they are clearly explained.
2. Help Search engines to better understand pages.  Search engine need to understand what your content is about when rank you properly on search engines. Semantic code tends to improve your placement on search engines, as it is easier for the "search engine spiders" to understand.
3. It’s easier to read and edit, which saves time and money during maintenance.

## What is Iframe?
* An IFrame (Inline Frame) is an HTML document embedded inside another HTML document on a website.
* The IFrame HTML element is often used to insert content from another source, such as an advertisement, into a Web page.
<iframe src="http://www.w3schools.com">不支持 iframe 的浏览器</iframe>


## Meta tag
* The tag provides metadata about the HTML document. Metadata will not be displayed on the page, but will be machine parsable.
* Meta elements are typically used to specify page description, keywords, author of the document, last modified, and other metadata.
* The metadata can be used by browsers (how to display content or reload page), search engines (keywords), or other web services.

# CSS
## CSS preprocessor
CSS preprocessors take code written in the preprocessed language and then convert that code into the same old css. 3 of the more popular css preprocessors are Sass(用过), LESS, and Stylus
### CSS preprocessor Pros and cons:
* Pros:
  1.	Nested syntax
  2.	Ability to define variables
  3.	Ability to define mixins
  4.	Mathematical functions
  5.	Operational functions (such as “lighten” and “darken”)
  6.	Joining of multiple files
* Cons:
  1.	Debugging is harder
    - Due to having a compilation step, the browser is not interpreting the source files, meaning the CSS line numbers are now irrelevant when trying to debug. This makes debugging a lot harder.

  2.	Maintainance

  3.	Compilation time slows down development
    - Compilation times can be painfully slow, even when using the fastest techniques on a cutting edge machine.
  4.	Performance is compromised
    - Source files may be small, but the generated CSS could be huge. And it’s the generated CSS that counts.

## pt, px, em, rem
* pt are absolute length, 1 pt = 1/72 inch
* px are relative length, different resolution is different length
* em is also relative length, which depends its parents length
* rem is also relative length, which depends root length of HTML

### CSS3 to make shape
* use transform(traslate, rotate)
* use border
```css

  #triangle-up {
    width: 0;
    height: 0;
    border-left: 50px solid transparent;
    border-right: 50px solid transparent;
    border-bottom: 100px solid red;
}
```
 [See more details here](http://www.jqhtml.com/8045.html)

## SASS basic concepts
1. Variables: Variables in SASS start with $ sign
2. Nesting: CSS lacks visual hierarchy while working with child selectors. You have to write selectors and their combinations in separate lines. Nesting provides a visual hierarchy as in the HTML and increases the readability.
3. mixins: mixins are used to include a bunch of properties or group declarations together. It allows for the easy reuse of blocks of code. Use include  to
4. Inheritance: extends are useful for sharing a generic definition with selectors rather than copying it in.
5. If/Else Statements and loops
6. import: separating your codes in small pieces is helpful for expressing your declarations and increasing maintainability and control over the codebase.
7. Math operations: can be used for standard arithmetic or unit conversions.

## Box model
* block: by default, the width is 100%
* inline: width is decided by Content
## Position property
* relative: not change the display property of elements
* absolute: if parents of the elements do not set relative or absolute, the element will locate by the body
  - width of block elements becomes auto
  - inline elements' display will become blocks
* using relative and absolute, the elements will cover other elements; but we can set z-index as -1
## float
* The float CSS property specifies that an element should be placed along the left or right side of its container, allowing text and inline elements to wrap around it. The element is removed from the normal flow of the web page, but the element will not cover the content of next elements(only cover the border).
* after setting a float property, the element will become a block

## Clear float
If children set float, the parent will lose height from children. In order to let the parent looks like contain children, we have several method:
1. add new tag in the parent element: < br style="clear:both" />
2. Float (Nearly) Everything
3. use psedou class after
```html
<div class="l-form-row">
            <div class="l-form-label"></div>
            ....
        </div>
        <style>
            .l-form-row:after {
                clear: both;
                content: "\0020";
                display: block;
                height: 0;
                overflow: hidden
            }
        </style>
```
4. set the parent container overflow: hidden,  or overflow: auto;
5. use clearfix:
```
        .clearfix:after {
          content: " ";
          display: block;
          clear: both;
          height: 0;
        }
        .clearfix {
          zoom: 1;
        }
        <div class="clearfix">
        <div class="floated"></div>
        </div>
```
