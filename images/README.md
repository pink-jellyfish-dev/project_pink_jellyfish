# Images

Place images used by the static site in this folder. Reference image files with relative paths:

- From a page in the site root: `images/photo.jpg`
- From a page in `posts/`: `../images/photo.jpg`

Example for a journal post:

```html
<img src="../images/photo.jpg" alt="Describe what is shown in the image">
```

Use meaningful alternative text for informative images, or `alt=""` for decorative images. Keep filenames simple and match their capitalization in HTML links; GitHub Pages paths are case-sensitive.
