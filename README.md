# Jekyll Bigfoot Boilerplate
A basic Jekyll Boilerplate structure perfect to use with CloudCannon CMS
---

## Overview
This boilerplate uses the following technologies and frameworks:
- Jekyll (4.0.0)
- Sass
- jQuery (3.5.0)

### Structure

Modular code blocks (_sections_) can be used to build the layout of the site. The sections are configured in the `_config.yml` file and blocks are stored in the `_includes/blocks` folder. Editors can use the CloudCannon UI to add, remove or modify positioning of the structural components according to their requirements.

When adding custom sections, configure both the `_config.yml` file and the `default.html` layout

For more information on configuring array structures, follow this comprehensive documentation from CloudCannon: [Managing Complex Array Structures](https://cloudcannon.com/features/2019/05/22/array-structures/).

### Global Site Settings

Global site variables are stored in the `settings.yml` file located inside the `_data` folder.

All metadata for Open Graph tags is pulled directly from the `settings.yml` file through Liquid syntax. Modification of the `settings.yml` arrays must be followed by changes in the `og.html` file located inside the `_includes/essentials` folder.

### Styles

#### Setting-up `Sass` variables

`Sass` variables are populated by values declared on `settings.yml`. These variables are then declared on the `main.scss` stylesheet in order to make them available to the whole stylesheet & partials, like so:

```
$variable-name: {{site.data.settings.the-yaml-array-location}};
```

_Note 1:_ the `Sass` variables pulled from `settings.yml` need to be placed **before** the variable is called (i.e. in any partials) and cannot be placed in `Sass` variables located in the `_sass` folder.
_Note 2:_ `Sass` partials cannot feature empty front matter (double `---` at top of file)

#### Padding/margin

Use the pre-defined classes located on the `_padding.scss` partial for uniformity of design. Edit the padding and margin defaults on the same file.

```
# Default padding classes:

.padding-lg {
  padding : 8%;
}

.padding-md {
  padding : 5%;
}

.padding-sm {
  padding : 2%;
}
```

_Note 1:_ If using Gridlex flexbox framework, you **cannot apply padding** to items with class including `col`. This can be reset on the `_resets` file by using global selectors like `[class=*col-]`.
