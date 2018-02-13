层叠就是浏览器对多个样式来源进行叠加，最终确定结果的过程.css之所以有“层叠”的概念，是因为有多个样式来源。其中css样式来源有5个，分别是内联样式（<a style="">）,内部样式(<style></style>),外部样式（写在css文件中的样式），浏览器用户自定义样式，浏览器默认样式；按照其来源优先级为内联样式>内部样式>外部样式>浏览器用户自定义样式>浏览器默认样式按照选择器优先级为id >class>元素选择器如果有important,important优先级最高。

Precedence of Style Settings

Loose compliance (minimum requirement):   <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN” "http://www.w3.org/TR/html4/loose.dtd">
Strict compliance:   <!DOCTYPE html PUBLIC “@-//W3C//DTD XHTML 1.0 Strict//EN”   	“http://www.w3.org/TR/html4/strict.dtd”>
XHTML Transitional compliance (less strict):  <!DOCTYPE html PUBLIC “@-//W3C//DTD XHTML 1.0 Transitional//EN”   “http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional-dtd”>
HTML5:
   <!DOCTYPE html>
Some browsers interpret the !DOCTYPE differently
The first example (loose) turns on standard mode in most browsers, but renders in quirks mode on Safari (Mac OS X)
Compound doctype declarations also exist for MathML and SVG


all - Suitable for all devices (CSS3)
braille - Intended for braille tactile feedback devices.
embossed - Intended for paged braille printers.
handheld - Intended for handheld devices (typically small screen, monochrome, limited bandwidth).
print - Intended for paged, opaque material and for documents viewed on screen in print preview mode. (CSS3)
projection - Intended for projected presentations (
screen - Intended primarily for color computer screens. (CSS3)
speech - intended for speech synthesizers (CSS3)
tty - Intended for media using a fixed-pitch character grid, such as teletypes, terminals, or portable devices with limited display capabilities.
tv - Intended for television-type devices (low resolution, color, limited-scrollability screens, sound available).
3d-glasses - Intended for 3D Glasses like Oculus VR and Google Cardboard.


Pseudo Elements and classes： 是因为他们只负责部分元素的style
一个 CSS  伪类（pseudo-class） 是一个以冒号(:)作为前缀的关键字，当你希望样式在特定状态下才被呈现到指定的元素时，你可以往元素的选择器后面加上对应的伪类（pseudo-class）。


pseudo classes
:first-child, Selects every <p> elements that is the first child of its parent
:hover, Selects links on mouse over
:active, selects the active link
:focus, selects the input element which has the focus
:lang, selects every <p> element with a lang attribute
:link – a normal, un-visited link
:visited – a link the user has visited
:hover - a link when the user mouses over it
:active - a link the moment it is clicked

pseudo elements
:first-line, add a special style to the first line of a text
:first-letter, add a special style to the first letter of a text
:before, to insert some content before the content of an element
:after, to insert some content after the content of an element


CSS Vendor Prefixes
Android: -webkit-
Chrome: -webkit-
Firefox: -moz-
Internet Explorer: -ms-
iOS: -webkit-
Opera: -o-
Safari: -webkit-
