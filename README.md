# Project Pink Jellyfish — Static Website

A responsive website starter built with plain HTML and CSS. It has no JavaScript, frameworks, build tools, package dependencies, or server-side features. GitHub Pages can publish the files as they are.

## Project structure

```text
.
├── index.html                 # Home page and featured journal posts
├── blog.html                  # Manually maintained journal index
├── about.html                 # About page
├── contact.html               # Contact page
├── experiments.html           # Experiment listings and game links
├── css/
│   ├── tokens.css             # Shared colors, typography, and layout variables
│   ├── base.css               # Global element defaults and accessibility focus styles
│   ├── layout.css             # Header, page containers, sections, and footer
│   ├── components.css         # Brand, menu, buttons, post cards, and text styles
│   └── responsive.css         # Small-screen and reduced-motion adjustments
├── images/                    # Images used by pages and journal posts
└── posts/
    ├── hello-world.html       # Editable example post
    └── getting-started.html   # Editable example post
```

## Editing the site

### Pages and navigation

Edit the relevant `.html` file to change its title, description, page content, or links. The navigation is shown along the header on larger screens and uses a native `<details>` and `<summary>` hamburger menu on screens 640px wide or narrower, so it works without JavaScript.

HTML does not have built-in reusable includes. To keep this site static and avoid a build step, the header and footer markup is repeated on each page. When changing the shared header, update it in every HTML page, including the pages in `posts/`. Update the footer on the pages where it appears as well.

### Styles

Each page loads the CSS files in order: tokens, base, layout, components, then responsive styles. Preserve this order when adding stylesheets because later files can override earlier rules.

- Change colors, fonts, and the shared content width in `css/tokens.css`. The current palette uses `--color-background` (`#101514`), `--color-primary` (`#F500C4`), `--color-secondary` and `--color-highlight` (`#00F5EC`), and `--color-extra` (`#A0358A`). Text, surface, border, and on-accent colors are supporting contrast colors.
- All heading levels (`h1`, `h2`, and `h3`) use Luckiest Guy from Google Fonts, and body text uses Cabin. Both have system-font fallbacks if Google Fonts is unavailable. Each HTML page includes the font stylesheet link because static HTML has no shared document head.
- Change global defaults in `css/base.css`.
- Change page structure and shared spacing in `css/layout.css`.
- Change specific visual elements in `css/components.css`.
- Change mobile or reduced-motion behavior in `css/responsive.css`.
- For an unavailable action on the Experiments page, use a disabled `<button class="button button--disabled" type="button" disabled>...</button>`. The `.button--disabled` modifier in `css/components.css` provides the grey appearance, while the native `disabled` attribute prevents interaction.

Keep shared styles in these files rather than adding inline styles to individual pages. All pages in the site root link to `css/`; pages one folder deeper use `../css/`.

### Adding images

Put image files in `images/` and use relative paths in your HTML. From a page in the site root, use `images/photo.jpg`. From a page inside `posts/`, use `../images/photo.jpg`. For example:

```html
<figure class="image-frame">
  <img src="../images/photo.jpg" alt="Describe what is shown in the image">
</figure>
```

The reusable `.image-frame` component keeps images at a 16:9 ratio and crops them to fit. Use a descriptive `alt` value for meaningful images, or `alt=""` for decorative images. Common web formats such as JPEG, PNG, GIF, WebP, and SVG work as static assets. Match the filename capitalization exactly; GitHub Pages paths are case-sensitive.

For a square thumbnail beside a post listing, add the `image-frame--thumbnail` modifier and place it beside the post text inside `.post-card`:

```html
<article class="post-card">
  <figure class="image-frame image-frame--thumbnail">
    <img src="images/photo.jpg" alt="Describe the image">
  </figure>
  <div class="post-card-content">
    <p class="post-meta">October 23, 2026</p>
    <h2><a href="posts/example.html">Post title</a></h2>
    <p>Short post description.</p>
  </div>
</article>
```

### Adding a journal post

1. Copy `posts/hello-world.html` to a new `.html` file in `posts/`.
2. Edit its `<title>`, description, heading, date, author, and article content.
3. Keep its stylesheet links as `../css/...` and its navigation links as `../index.html`, `../blog.html`, `../about.html`, and `../contact.html`.
4. Add a post card linking to the new file in `blog.html`. For example, a file called `my-post.html` is linked with `posts/my-post.html`.
5. Optionally add or replace a featured post card in the home page's journal section.

The journal list is maintained by hand: plain static HTML cannot automatically discover files in a folder. Keep the post title, date, and summary consistent between the post page, journal index, and home page.

## GitHub Pages

1. Push this repository to GitHub.
2. In the repository, open **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, then select the branch and folder containing `index.html` (commonly `main` and `/(root)`).
4. Save and open the published URL shown in the Pages settings.

All internal links and stylesheets use relative paths. This supports both user/organization sites and project sites hosted beneath a repository path. Keep `index.html` at the published root so GitHub Pages can use it as the home page. No Node.js installation, workflow, or build command is required.

## Static-site constraints

- Content and journal listings are edited directly in HTML.
- There is no automatic post discovery, templating, search, or client-side behavior.
- Files and links are case-sensitive on GitHub Pages; use matching filename capitalization.
- Do not use root-absolute paths such as `/css/...` for site assets. Relative links preserve project-site paths.
