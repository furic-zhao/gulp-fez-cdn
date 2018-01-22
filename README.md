# gulp-fez-cdn

添加静态资源CDN地址

## install
```
npm install gulp-fez-cdn --save-dev
```

## Usage
```
    gulp.task('cdnify', function () {

      var cdnify = require('gulp-fez-cdn');

      return gulp.src([
        'dist/**/*.{css,html}'
      ])
        .pipe(cdnify({
          base: 'http://pathto/your/cdn/'
        }))
        .pipe(gulp.dest('dist/'))
    });
```

### For those who want to rewrite the url with their own specific rules.
```
pipe($.cdnify({
  rewriter: function(url, process) {
    if (/eot]ttf|woff|woff2/.test(url)) {
      return 'http://myfontcdn.com/' + url;
    } else if (/(png|jpg|gif)$/.test(url)) {
      return 'http://myimagecdn.com/' + url;
    } else {
      return process(url);
    }
  }
}));
```

### If you want to read custom source (Eg. favicon)
```
pipe($.cdnify({
  html: {
    'link[rel="shortcut icon"]': 'href',
    'link[rel="apple-touch-icon-precomposed"]': 'href'
  }
}));
```

### Default sources:
```
sources = {
  'img[src]': 'src',
  'link[rel=stylesheet]': 'href',
  'script[src]': 'src',
  'video[poster]': 'poster',
  'source[src]': 'src'
}
```
