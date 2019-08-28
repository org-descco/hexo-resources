# Hexo resources

[![licence mit](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](http://hemersonvianna.mit-license.org/)
[![GitHub issues](https://img.shields.io/github/issues//org-descco/hexo-resources.svg)](https://github.com//org-descco/hexo-resources/issues)
![GitHub package.json version](https://img.shields.io/github/package-json/v//org-descco/hexo-resources.svg)
![GitHub Release Date](https://img.shields.io/github/release-date//org-descco/hexo-resources.svg)
![GitHub top language](https://img.shields.io/github/languages/top//org-descco/hexo-resources.svg)
![GitHub repo size](https://img.shields.io/github/repo-size//org-descco/hexo-resources.svg)
![GitHub All Releases](https://img.shields.io/github/downloads//org-descco/hexo-resources/total.svg)

Pipeline for [Hexo](https://hexo.io/).
- Hexo 3.x.x

## Configuration
Add the following snippet in `_config.yml`.

Minimal config to enable filters for HTML, CSS, Js and images.
```yaml
descco_pipeline:
  revisioning:
    enable: true
  node_sass:
    enable: true
  webpack:
    enable: true
  imagemin:
    enable: true
  html_minifier:
    enable: true
  jsonContent:
    enable: true
```

## Components
Following are the modules that are being used to process differnet types of assets.

### HTML (html_minifier)
[html-minifier](https://www.npmjs.com/package/html-minifier) is used to minify the HTML files.

Following is the config for html-minifier.

#### Options
``` yaml
html_minifier:
  enable: true
  ignore_error: false
  exclude:
```
- **enable** - Enable the plugin. Defaults to `false`.
- **ignore_error** - Ignore the error occurred on parsing html
- **exclude**: Exclude files

#### html_minifier defaults
```yaml
html_minifier
  ignoreCustomComments: [/^\s*more/]
  removeComments: true
  removeCommentsFromCDATA: true
  collapseWhitespace: true
  collapseBooleanAttributes: true
  removeEmptyAttributes: true
  minifyJS: true
  minifyCSS: true
```

**Note**: Check [html-minifier](https://www.npmjs.com/package/html-minifier#options-quick-reference) for more options.

### Images (imagemin)
[imagemin](https://www.npmjs.com/package/imagemin) is used to optimize images.

Following is the config for imagemin.
#### Options
```yaml
imagemin:
  enable: true
  interlaced: false
  multipass: false
  optimizationLevel: 2
  pngquant: false
  progressive: false
```
- **enable** - Enable the plugin. Defaults to `false`.
- **interlaced** - Interlace gif for progressive rendering. Defaults to `false`.
- **multipass** - Optimize svg multiple times until it’s fully optimized. Defaults to `false`.
- **optimizationLevel** - Select an optimization level between 0 and 7. Defaults to `2`.
- **pngquant** - Enable [imagemin-pngquant](https://github.com/imagemin/imagemin-pngquant) plugin. Defaults to `false`.
- **progressive** - Lossless conversion to progressive. Defaults to `false`.
- **exclude** - Exclude specific types of image files, the input value could be `gif`,`jpg`, `png`, or `svg`. Default to null.

#### imagemin defaults
```yaml
imagemin:
  interlaced: false
  multipass: false
  optimizationLevel: 3
  pngquant: false
  progressive: false
```

**Note**: Check [imagemin](https://www.npmjs.com/package/clean-css#use) for more options.

### Revisioning
```yaml
revisioning:
  enable: true
  keep: true
  exclude: ['robots.txt', '*.json']
  selectors:
    'img[data-orign]':  data-orign
    'img[data-src]': 'data-src'
    'img[src]': 'src'
```
- **enable** - Enable revisioning of assets. Defaults to `false`.
- **keep** - Keep original assets. Defaults to `false`.
- **exclude** - Exclude files from revisioning.
- **selectors** - It is used so that custom implementations can be processed. Any attribute matching the key should have the asset url in the value. For instance in above example any element matching to `img[data-orign]` will have the URL for asset in `data-origin` attribute, this specific case can be helpful for [jquery lazyload](https://github.com/tuupola/jquery_lazyload) implementations.

#### Revisioning defaults;
```yaml
revisioning:
  enable: false
  keep: false
  exclude: []
  selectors:
    'img[data-src]': 'data-src'
    'img[src]': 'src'
    'link[rel="apple-touch-icon"]': 'href'
    'link[rel="icon"]': 'href'
    'link[rel="shortcut icon"]': 'href'
    'link[rel="stylesheet"]': 'href'
    'script[src]': 'src'
    'source[src]': 'src'
    'video[poster]': 'poster'
```

#### Note: To match paths in `exclude` option, glob matching is done using [minmatch](https://github.com/isaacs/minimatch).


## Observation

imagemin (Mac OS)

```
brew install libpng
```
