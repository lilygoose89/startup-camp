# Plugins
These are the installed plugins
- jekyll-sitemap (no defined version)
- jekyll-feed (no defined version)
- jekyll-responsive-image (1.5.5)
- jekyll-archives (2.2.1)
- jekyll-webp (1.0.0)

## Configurations

### `jekyll-responsive-image`
_NB: This plugin has its own dependency: you must install `rmagick` on your system for it to work._

This plugin automatically resizes images into the provided size scope and renders `srcset` values for the image tags. The code and use have been refactored in order to use partials for image code blocks. It **also renders Markdown images** by use of `Jekyll hooks` declared in `img-tag-transform.rb`([check this implementation on this article](https://www.ivovalchev.com/blog/jekyll-responsive-images-with-srcset/) by Ivo Valchev).

- Link to the official documentation: [jekyll-responsive-image](https://github.com/wildlyinaccurate/jekyll-responsive-image)

#### Site-specific usage
Insert the following tag in place of a regular `<img>` tag:

```
{% assign path = "assets/images/your-image.jpg" %}
{% assign alt = "Your alt text" %}
{% include image.html %}

```

**Alternatively make use of this block:**

```
{% assign path = page.main_image %} # YAML front matter version
{% assign alt = page.main_image_alt_text %} # YAML front matter version
{% include image.html %}
```
where the `path` and `alt` are values extracted from the page front matter (configure at will).

#### Image templates
Located inside the `_includes/templates` folder.

1. `image.html`
The `image.html` template generates a `<picture>` element with two `srcset` sources: resized `jpg` images and generated `WebP` versions. An important mention is that it takes in consideration the viewport size and **NOT** the image container size; hence it is not fully responsive **BUT** already saves a lot of time and effort resizing images and generating `srcset` files.

2. `image-lazy.html`
In similar fashion to the above template, but counting on `lazysizes` for lazy loading images. The `lazysizes` script is added to the `scripts.html` file, and the feature is implemented by adding the `class="lazyload"` to the `image-lazy.html` template. Recommended to have this template as default for the majority of the images, and use `image.html` for above-the-fold images.

Head to `_config.yml` to get this customized according to the guidelines below; note that *some keys are not required but recommended*:

```
responsive_image:
# [Optional, Default: 85]
  # Quality to use when resizing images.
  default_quality: 90

  # [Optional, Default: []]
  # An array of resize configuration objects. Each object must contain at least
  # a `width` value.
  sizes:
    - width: 480  # [Required] How wide the resized image will be.
      quality: 80 # [Optional] Overrides default_quality for this size.
    - width: 800
    - width: 1400
      quality: 90

  # [Optional, Default: false]
  # Rotate resized images depending on their EXIF rotation attribute. Useful for
  # working with JPGs directly from digital cameras and smartphones
  auto_rotate: false

  # [Optional, Default: false]
  # Strip EXIF and other JPEG profiles. Helps to minimize JPEG size and win friends
  # at Google PageSpeed.
  strip: false

  # [Optional, Default: assets]
  # The base directory where assets are stored. This is used to determine the
  # `dirname` value in `output_path_format` below.
  base_path: assets

  # [Optional, Default: assets/resized/%{filename}-%{width}x%{height}.%{extension}]
  # The template used when generating filenames for resized images. Must be a
  # relative path.
  #
  # Parameters available are:
  #   %{dirname}     Directory of the file relative to `base_path` (assets/sub/dir/some-file.jpg => sub/dir)
  #   %{basename}    Basename of the file (assets/some-file.jpg => some-file.jpg)
  #   %{filename}    Basename without the extension (assets/some-file.jpg => some-file)
  #   %{extension}   Extension of the file (assets/some-file.jpg => jpg)
  #   %{width}       Width of the resized image
  #   %{height}      Height of the resized image
  #
  output_path_format: assets/resized/%{width}/%{basename}

  # [Optional, Default: true]
  # Whether or not to save the generated assets into the source folder.
  save_to_source: false

  # [Optional, Default: false]
  # Cache the result of {% responsive_image %} and {% responsive_image_block %}
  # tags. See the "Caching" section of the README for more information.
  cache: false

  # [Optional, Default: []]
  # By default, only images referenced by the responsive_image and responsive_image_block
  # tags are resized. Here you can set a list of paths or path globs to resize other
  # images. This is useful for resizing images which will be referenced from stylesheets.
  extra_images:
    - assets/foo/bar.png
    - assets/bgs/*.png
    - assets/avatars/*.{jpeg,jpg}
```

### `jekyll-webp`

This plugin automatically generates `WebP` versions of the image assets. `WebP` is a next-gen format for web images and considerably reduces the size of the files; `WebP` files are stored in the same directory as the original asset, use the same name but a _different extension_.

- Link to the official documentation: [jekyll-webp](https://github.com/sverrirs/jekyll-webp)

Head to `_config.yml` to get this customized according to the guidelines below:
```
# The values here represent the defaults if nothing is set
webp:
  enabled: true

  # The quality of the webp conversion 0 to 100 (where 100 is least lossy)
  quality: 75

  # List of directories containing images to optimize, nested directories will only be checked if `nested` is true
  # By default the generator will search for a folder called `/img` under the site root and process all jpg, png and tiff image files found there.
  img_dir: ["/img"]

  # Whether to search in nested directories or not
  nested: false

  # add ".gif" to the format list to generate webp for animated gifs as well
  formats: [".jpeg", ".jpg", ".png", ".tiff"]

  # File extensions for animated gif files
  gifs: [".gif"]

  # Set to true to always regenerate existing webp files
  regenerate: false

  # Local path to the WebP utilities to use (relative or absolute)
  # Omit or leave as nil to use the utilities shipped with the gem, override only to use your local install
  webp_path: nil

  # List of files or directories to exclude
  # e.g. custom or hand generated webp conversion files
  exclude: []

  # append '.webp' to filename after original extension rather than replacing it.
  # Default transforms `image.png` to `image.webp`, while changing to true transforms `image.png` to `image.png.webp`
  append_ext: false

```
