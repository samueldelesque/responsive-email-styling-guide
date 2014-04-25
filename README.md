responsive email rendering issues
=================================

<img src="http://162.243.0.54/most-annoying-email/assets/img/useless-markup.png" style="margin:0 auto"/>


A little list of annoying bugs that might save you time if you are heading to create a responsive email:


[I have excluded the most obvious like having to use Tables, obscure oldschool html/css patterns etc]


todo list
=========
* don't re-use CSS classes generally (like you would in html). Its better to have a distinct class on each element so that you can style them separately (especially when then render differently in responsive mode)


bug list
========

* Outlook 2007 and 2010 render HTML through Word Html engine, and therefore all **tables longer than 1790px will cause a line break**. The solution is to add a 'style="page-break-before: always"' on the containing tr element. [source: http://mikethecoder.tumblr.com/post/861597102/outlook-2007-screws-up-spacing-where-page-breaks-would] [read also: http://www.emailonacid.com/blog/details/C13/horizontal_spacing_issues_in_outlook_2007_and_2010]
* Your {br/} tags now won't work as expected. You will need to **add tables and trs everywhere** you want line breaks.
* Yahoo will render inline ALL your styles EVEN THOUGH it is a media query. So if you plan on increasing text for Iphone, remember it will be a **compromise between the Iphone's too small size and Yahoo's too big** size.
* To **hide elements** in Gmail you need to add height=0 and width=0 on your element (display:none is not enough). The oposite is true for other readers (you might need to add "mso-hide:all" on your elements for Outlook 2007-2013 [source: http://www.copernica.com/en/blog/quick-tip-how-to-hide-mobile-content-in-desktop-email-clients]).
* To **hide text** in Gmail, you will have to set the color to "transparent". Also add "overflow:hidden;float:left;" and clear in css.
* To **hide an image** in Outlook 2010/2007 you cannot simply add the styles on the image. You have to wrap the image in a span or other element and hide that span.
* The Gmail app will NOT render any media queries (or anything inside a style element), so **forget about "responsive" emails in Gmail**.
* Don't use half percentage (use plain numbers) on images or HTC android **might** not display them.
* In IOS 6 and Android 4: when you have media queries around an image, the engine might not display the image if you are hiding the image originally (inline styles) - possibly because the two processes of rendering the css are running simultaniously, and only the last one to finish (the slowest) wins. Anyway, add a minimum width in pixels to fix that.
* Gmail app for Android will fuck up your display if your email is wider than [320?]px.
