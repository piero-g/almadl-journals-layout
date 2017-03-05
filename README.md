AlmaDL Journals Standard Layout
===============================

> _Better Late Than Never_

This is a simple [SASS](http://sass-lang.com/) solution that can be used generating a Cascading Style Sheet (CSS) for journals based on [Open Journal Systems 2.4.X](https://github.com/pkp/ojs). Please note that this solution is only suitable for OJS 2.4.X and not for OJS 3.0.

The stylesheet is meant to offer a standard OJS experience, with a focus on responsiveness and readability. It was created as a modern layout for the openaccess journals of [AlmaDL Journals](https://journals.unibo.it/), the Digital Library publishing platform of the University of Bologna.

It implies some tweaks to the standard code of OJS, as the introduction of viewports in every header and some specific HTML elements in header, footer etc. Please see "Notice" for further details.

List of the files:

- `AlmaDL-journalStyleSheet.scss`: a SCSS file to generate the CSS with
- `_journalTest.scss`: the template with the customizations for a single journal

Requirements:

- [SASS](http://sass-lang.com/) installed on your computer
- a text editor



## Deployment

1. copy `_journalTest.scss` as `_yourJournalTitle.scss` and set the appropriate values for each custom parameter (see Details)
2. open `AlmaDL-journalStyleSheet.scss` and change the `@import 'journalTest';` as `@import 'yourJournalTitle';` (line 2)
3. generate your new CSS with `sass --style expanded AlmaDL-journalStyleSheet.scss output.css`
4. as a Journal Manager, please upload the `output.css` in 5.6 Journal Layout in the setup of your journal, and check the result.



## Details

The theme is based on a few options to customize your journal easily but as in depth as possible - without having to edit manually the CSS. It covers several cases: as an example it could be used by a journal that does't adopt the OJS workflow (the CSS will hide the appropriate elements). Although it won't adapt to every possible scenario.

With the exception of improvements to readability of tables and of general responsiveness, every cosmetic element that differs from the standard OJS experience is optionally rendered under the "clear-style" rule-set, enabled by default.


### Main Settings

- `$journal-title` and `$subversion` are useful if you are dealing with more than one journal, it allows to record in the final CSS the title and a subversion number specific to the single journal, to keep track of the differences
- the `$no-publication` option is included in the main settings because is meant to be used only by new journals that are waiting for their first issue to be published. It hide all the elements that could create false expectations to the reader. Default value is "false", of course.


### Fonts
It is possible to specify custom fonts: the first field is meant for `@import` rules or `@font-face`, the default values are two Google Fonts.

In the second field you should specify the font-families for titles and body (please keep the `!important` in the `$font-titles` example). `$font-content-size` allow to specify a bigger size for your font, if your custom font needs it, while `$justified-text` define whether all the text will be justified or not (not relevant with minor screen sizes)


### Colors
It is possible to set various colors for your journal, 4 mandatory and 3 optional colors (listed as "Secondary colors").

The `a-color` is the color of every link and should be considered as the main color of your theme (default = red).
The `$header-color` define the background of your header and could be the same as `a-color` (default), the same as `body-color` (the background body color, default is white) or a custom color.  
Depending on the color, the font of you banner would be the same of your `body-color` if the header background is `a-color` (eg: white if the background is red). If your header has the same background as your body, on the other hand, your header font color will be `a-color` (eg: red if the background is white). If the solutions are not so good with your colors combination you can define a custom `$header-font-color`.

Other optional colors that can be defined are:

- a different color for links in hover and active (`$a-hoover-color`), by default if will use `a-color` and the reader will be able to distinguish them only by the underline
- a specific color for buttons (`$button-color`, with `a-color` as the default option)


### Header
Currently there are 3 parameters to set the journal header:

- `$header-centered` is self explanatory: when set to false the header will be aligned to the left
- `$header-textual` should be used if you haven't an image for the header; currently it implies a better spacing
- `header-banner` is meant to adjust the spacing of the header when you are using a large image that should extend itself (mostly) at full width


### Home
The parameter `$home-image` should be used when uploading an image to appear in homepage. Please see the notice about html in home below.
`$no-current-home` (default "false") controls if your journal is including the "Current Issue" in the homepage. **Please set to true if you are not including your current issue in home.** 


### Issue Cover
If you are willing to upload an issue cover, there are 3 parameters to take care:

- `$issue-cover-main` is "false" to default and should be set to "true" only if you are enabling (via Editor > Issue > Issue Data > Cover) the display of the cover before the table of contents (which is difficult to recommend). If will load some rules to allow a responsive issue cover
- `$issue-cover-archive` should be set to "true" if you are going to display issue covers as thumbnail in the Archive; it will take also care of the correct alignment of issues without a cover
- `$issue-cover-size` (default "650px") define the maximum width of a cover when displayed before the table of contents. If you are going for a wider size be sure to be consistent with the cover quality over the years.


### Workflow
The parameter `$only-publication` is recommended for journals that don't use the online submission process offered by OJS; this will hide some elements that may be confusing for authors and readers, such as the "Online Submission" paragraph in "About > Submissions" and the workflow schema in "About this Publishing System"


### Publisher and Sponsor
Since OJS 2.4.X does not consider the possibility of more than one publisher, a possible workaround is to go to Setup, step 1.5:

- insert both publishers in the "Institution", separated by a semicolon; leave the "URL" empty
- insert both publishers in the "Note" in HTML, as you would them to appear
- set in the SCSS template `$double-publisher` as true so that OJS will display only the "Note" field (while still exporting two publishers in metadata)

If you have also sponsors or support organizations please change `$sponsor` to "true", thus to display an otherwise inappropriate separator.


### Other styles
The theme comes with `clear-style` enabled by default. It changes the style of buttons, forms, separators and some other elements as the Announcements in home (greyed and in a box in bigger screens). This style is meant to provide a more modern and clean experience.

If you need or prefer to stick with a layout as similar as possible to the default OJS 2.4.X than you should set this to "false".

`$button-border-rad` is an additional parameter that alter the border radius of buttons and forms; the default value offers rounded corners, other values are suggested in the comment. 



## Notice

This theme relies on several customizations of the OJS base code or on the way it is populated in the Setup.


### Edits to the OJS code

#### Viewport

The correct implementation implies that a viewport is set for each header `.tpl` of OJS, as:

```
<meta name="viewport" content="width=device-width, initial-scale=1">
```

Without a viewport every effort is useless since at smaller resolutions the browser will render font sizes inconsistently.

List of the headers where you should specify the viewport:
```
templates/article/header.tpl
templates/rt/header.tpl
templates/about/editorialTeamBio.tpl
pkp/lib/templates/common/header.tpl
pkp/lib/templates/help/header.tpl
```

#### Editorial Bio

Another small edit to the OJS code was made in order to easily select the bio popup pages:

in `templates/about/editorialTeamBio.tpl` was slightly changed the id of `<body>`

from `<body id="pkp-{$pageTitle|replace:'.':'-'}">`  
to `<body id="pkp-bio-{$pageTitle|replace:'.':'-'}">`


### Journal Description

The theme hide the main journalDescription from the homepage (so it can be populated more wisely without having it to be "as we would the homepage appear"; so please use only "additionalHomeContent" for your homepage or remove the following:
```
body#pkp-common-openJournalSystems #journalDescription {
	display: none;
}
```


### Home Image

If adding an image to the Homepage please consider that the CSS is not based on the standard "Home Image" for OJS. Our implementation is based based on the following HTML:

```
<div id="additionalHomeContent">
	<p>Lorem ipsum</p>
	<div class="homeImage">
		<img></img>
		<p>This is a caption</p>
	</div>
	<div class="homeText">
		<p>Lorem Ipsum</p>
	</div>
</div>
```


### Footer

In OJS 2.4.X the footer has poor consistency, to style it appropriately the stylesheet implies that you enclose it in `<div id="footer">..</div>` (possible as Journal Manager in 5.4 Journal Page Footer).


