How to style a responsive HTML email 
====================================

This is a draft of a guide on how to avoid common gotchas while developing your responsive html emails. It will not account for every trickery that's out there - but just the basics to get you started and avoid the most time consuming bugs.


<img src="http://162.243.0.54/most-annoying-email/assets/img/useless-markup.png" style="margin:0 auto"/>


## What to say when the designer asks

* Can we have a [negative top margin style] element above a template image? -`Nay`
* Can we use this non-standard webfont? -`Nay`
* Can we add a gif? -`Sure - but make sure its ok if it falls back to just the first frame`
* How many articles can I display? -`As many as can fit in 1790px height`
* How wide should the email be? -`Less than 600px. (definitely no more than 800px)`
* Can we add transparent PNGs on top of content? -`Nope`


## How to code the email

* tables, tables, tables
* inline styles, default table/td attributes

```<table valign="top" border="0" cellpadding="0" cellspacing="0" width="600" class="full">```

* Assets must be cut by line
* Assets that are replaçable by client (in Mailchimp) should not be on over/under-laying other elements
* INK: allows for rapid 12col>1col responsive email layouts


## Making it responsive

* hiding elements
```
		.show-mobile{
			display:block !important;
			visibility:visible !important;
			mso-hide:none !important;
			height:auto !important;
			float:none !important;
			max-height:none !important;
			width:auto !important;
		}
		...
		<table class="show-mobile" 
			cellpadding="0" 
			align="center" 
			cellspacing="0" 
			border="0" 
			style="overflow:hidden;height:0;width:0;display: none;float:left;mso-hide:all;margin:0 auto;">
```
* main, gutter class
* re-ordering elements for mobile


## Client specific issues

* Gmail: No responsive design possible
* Gmail Android: to avoid the "Gmail Responsiveness", add an image the size of the email in the parent table and set its min-width to the email width (i.e. 580px)

* Outlook: Tables must be "breakable" around 1790px or less. Place a `page-break-before: always`  on the element where it would be OK to break (word rendering engine);
* IOS/Apple Mail: The rendering is generally pretty good. If you would like to show a custom "content-exerpt" in the list view, you can add the copy to the Alt tag of the first image in the email (i.e. the logo, assuming there is no text before). This should work in other platforms as well.




bug list
========

* Outlook 2007 and 2010 render HTML through Word Html engine, and therefore all **tables longer than 1790px will cause a line break**. The solution is to add a 'style="page-break-before: always"' on the containing tr element. [source: http://mikethecoder.tumblr.com/post/861597102/outlook-2007-screws-up-spacing-where-page-breaks-would] [read also: http://www.emailonacid.com/blog/details/C13/horizontal_spacing_issues_in_outlook_2007_and_2010]
* Your {br/} tags now won't work as expected. You will need to **add tables and trs everywhere** you want line breaks.
* Yahoo will render inline ALL your styles EVEN THOUGH it is a media query. A fix for this is to add a random attribute to your body tag and then prepend all your css classes with it. For example `<body yahoo>` > `body[yahoo] .someclass {width:600px;}`
* To **hide elements** in Gmail you need to add height=0 and width=0 and float on your element (display:none is not enough). The oposite is true for other readers (you might need to add "mso-hide:all" on your elements for Outlook 2007-2013 [source: http://www.copernica.com/en/blog/quick-tip-how-to-hide-mobile-content-in-desktop-email-clients]).
* To **hide an image** in Outlook 2010/2007 you cannot simply add the styles on the image. You have to wrap the image in a span or other element and hide that element.
* The Gmail app will NOT render any media queries (or anything inside a style element), so **forget about "responsive" emails in Gmail**.
* [Not able to fully test] Don't use half percentage (use plain numbers) on images or HTC android **might** not display them.
* Gmail app for Android add a "responsive mode" to your "non-reponsive email" (your media queries are stripped). To avoid having the broken "responsive mode" showing, you can add an image in the parent table and having a min-width attribute equal to the width of the email.
* Gmail will cut your html and add a "show more" button if your html is longer than **~100k characters**
