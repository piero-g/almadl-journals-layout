AlmaDL Journals Standard Layout
===============================

> _Better Late Than Never_

This is a SASS solution that can be used to generate a Cascading Style Sheet (CSS) for journals based on [Open Journal Systems 2.4.X](https://github.com/pkp/ojs). Please note that this solution is only suitable for OJS 2.4.X and not for OJS 3.0.

The stylesheet is meant to offer a standard OJS experience, with a focus on responsiveness and readability. It was created as a modern layout for the openaccess journals of [AlmaDL Journals](https://journals.unibo.it/), the publishing platform of the Digital Library of the University of Bologna.

It implies some tweaks to the standard code of OJS, as the introduction of viewports in every header and some specific HTML elements in header, footer etc. Please see "Notice" for further details.

List of the files:

- `AlmaDL-journalStyleSheet.scss`: a SASS to generate the CSS with
- `_journalTest.scss`: the template with the customization for each journal


## Deployment

1. copy `_journalTest.scss` as `_yourJournalTitle.scss` and set the appropriate values for each custom parameter (see Details)
2. open `AlmaDL-journalStyleSheet.scss` and change the `@import 'journalTest';` as `@import 'yourJournalTitle';` (line 2)
3. generate your new CSS with `sass --style expanded AlmaDL-journalStyleSheet.scss output.css`
4. as a Journal Manager, please upload the `output.css` in 5.6 Journal Layout in the setup of your journal, and check the result.


## Details

The theme is based on a few options to customize your journal easely but as in depth as possible - without having to edit manually the CSS.

### Template Informations
_todo_

### Fonts
_todo_

### Colors
_todo_

### Header
_todo_

### Issue Cover
_todo_

### Various options
_todo_

### Double Publisher

Since OJS 2.4.X doesn't consider the possibility of more than one publisher, a possible workaround is to go to Setup, step 1.5:

- insert both publishers in the "Institution", separated by a semicolon; leave the "URL" empty
- insert both publishers in the "Note" in HTML, as you would them to appear
- set in the SCSS template `$double-publisher` as true so that OJS will display only the "Note" field (while still exporting two publishers in metadata)


## Notice

This theme relies on several customizations of the OJS base code or on the way it is populated in the Setup.

### Edits to the OJS code

#### Viewport

The correct implementation implies that a viewport is set for each header `.tpl` of OJS, as:

```
<meta name="viewport" content="width=device-width, initial-scale=1">
```

Without a viewport every effort is useless since at smaller resolutions the browser will render font sizes unconsistently.

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

In OJS 2.4.X the footer has poor consistency, to style it appropriately the stylesheet implies that you enclose it in `<div id="footer">..</div>`


