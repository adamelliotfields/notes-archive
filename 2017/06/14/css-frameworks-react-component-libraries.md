# CSS Frameworks and React Component Libraries
This is a list of CSS Frameworks and React Component Libraries that I've found and some that I've actually used.  

If it sounds like I'm biased towards Bootstrap, that's because I am :kissing_heart:

## CSS

#### [Bootstrap](https://github.com/twbs/bootstrap)
Notes:
* Insanely fast prototyping without touching any CSS.
* BootstrapCDN (which also hosts Font Awesome) is faster than CDNJS or UNPKG.
* Beta 4 Alpha 6 was rebuilt entirely in Flexbox and works flawlessly.
* Simply nest containers, rows, and columns as much as you want.
* Responsive grid that *just works* without writing any media queries.
* Change layouts based on viewport size by simply adding another class.
* Ships with a grid-only option.
* Includes utility classes for just about everything - padding, margin, borders, border radius, images, etc.
* Tons of components.
* Use's Bootstrap's custom Reboot CSS reset.
* Unfortunately, components that rely on jQuery or Tether are not clearly defined.
* Requires heavy custom styling to avoid looking like a *Bootstrap* site.
* Typography is NOT responsive, although this can easily be solved with PostCSS Responsive Type.

---

#### [Foundation](https://github.com/zurb/foundation-sites)
Notes:
* Comes with both Flexbox and float-based distributions.
* Flexbox distribution works magically.
* Website has videos for almost every component.
* Components that require JavaScript/jQuery are clearly marked.
* Base styles are almost non-existent as it's meant to be a _foundation_ for your styles.
* No utility classes.
* No containers?

---

#### [Materialize](https://github.com/Dogfalo/materialize)
Notes:
* Based on Google's Material design language.
* Uses Flexbox.
* Classes are similar to Bootstrap, so it's easy to pick up.
* Base styles are more attractive than Bootstrap or Foundation.
* No utility classes.
* I ran into Flexbox issues (collumns collapsing and text spilling out) that I could not solve.

---

#### [Pure](https://github.com/yahoo/pure)
Notes:
* Ultra lightweight grid.
* Styling for buttons, forms, tables, and menus.
* Grid is based on 24 units instead of the usual 12, which gives more fine-grained control.
* I was unable to get nested rows and columns to work.
* I found this to be the most difficult to use out of all the CSS frameworks I tried.

---

#### [Bulma](https://github.com/jgthms/bulma)
Notes:
* Based entirely on Flexbox.
* Very attractive base styles.
* Good documentation.
* Some really nice components.
* Column breakpoints can be set using the "mobile", "tablet", and "desktop" helper classes.
* Rows can have breakpoints set too, which is cool, but also introduces another layer of complexity.
* Requires knowledge of Flexbox, as I ran into some gotchas that I could not fix despite following the examples in the docs.
* Requires CSS to be written alongisde HTML while prototyping as there are no utility classes.
* Headers must use a title or subtitle class, otherwise a `<h1>` will appear like a `<p>`.
* Overall, I found it harder to use than Bootstrap or Foundation.

---  

#### [UIKit](https://github.com/uikit/uikit)
Notes:
* Most robust set of components of any framework I've tried.
* Because it can do so much, the learning curve can be steeper since there's a lot to learn.
* Base styles look great out of the box.
* Includes a custom SVG icon set.
* Use this if you want to build a site using their components and jQuery (there are some awesome examples); overkill if you just need a grid and base styles.
* Despite almost 10,000 stars on GitHub, anytime I ran into a gotcha, I found nothing on Google.

---

#### [GitHub Primer](https://github.com/primer/primer-css)
Notes:
* Very simple to learn as it's very similar to Bootstrap.
* Base styles are simple and very attractive if you like GitHub's design aesthetic.
* Some awesome components (like styled tooltips in pure CSS that don't require Tether or jQuery).
* Requires setting your own media queries as it's not responsive out of the box (unless I missed something in the docs).
* No Navbar?

---

[Skeleton](https://github.com/dhg/Skeleton)  

[Milligram](https://github.com/milligram/milligram)  

[Tachyons](https://github.com/tachyons-css/tachyons)  

[Topcoat](https://github.com/topcoat/topcoat)  

[Spectre](https://github.com/picturepan2/spectre)  

[Hack](https://github.com/egoist/hack)  

[VMware Clarity](https://github.com/vmware/clarity)  


### React
[HP Grommet](https://github.com/grommet/grommet)  

[Palantir Blueprint](https://github.com/palantir/blueprint)  

[Rebass](https://github.com/jxnblk/rebass)  

[Semantic UI React](https://react.semantic-ui.com/introduction)  

[React Toolbox](https://github.com/react-toolbox/react-toolbox)  

[Material UI React](https://github.com/callemall/material-ui)  
