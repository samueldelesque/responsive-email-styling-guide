Most annoying responsive email rendering issues
===============================================




A little list of annoying bugs that might save you time if you are heading to create a responsive email:


[I have excluded the most obvious like having to use Tables, obscure oldschool html/css patterns etc]


* Outlook 2007 and 2010 render HTML through Word Html engine, and therefore all *tables longer than 1790px will cause a line break*. The solution is to add a 'style="page-break-before: always"' on the containing tr element. [source: http://mikethecoder.tumblr.com/post/861597102/outlook-2007-screws-up-spacing-where-page-breaks-would] [read also: http://www.emailonacid.com/blog/details/C13/horizontal_spacing_issues_in_outlook_2007_and_2010]
* Yahoo will render inline ALL your styles EVEN THOUGH it is a media query. So if you plan on increasing text for Iphone, remember it will be a *compromise between the Iphone's too small size and Yahoo's too big* size.
* To *hide elements* in Gmail you need to add height=0 and width=0 on your element (display:none is not enough). The oposite is true for other readers (you might need to add "mso-hide:all" on your elements for Outlook 2007-2013 [source: http://www.copernica.com/en/blog/quick-tip-how-to-hide-mobile-content-in-desktop-email-clients]).
* To *hide an image* in Outlook 2010/2007 you cannot simply add the styles on the image. You have to wrap the image in a span or other element and hide that span.
* The Gmail app will NOT render any media queries (or anything inside a style element), so *forget about "responsive" emails in Gmail*.








Why, oh why do email clients need to differ that badly?
=======================================================

The Internet Consortium shut down in 2001 - maybe that could explain something.
[source: http://www.imc.org/]
