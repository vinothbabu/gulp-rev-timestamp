## Install

```sh
$ npm install --save gulp-rev-timestamp
```
## Why another plugin?

This plugin is based on gulp-rev-append which is very good and in some cases even better, because it relies on file hash, so if file didn't change between versions, the hash will remain the same so file can stay in cache.

gulp-rev-timestamp provides you an option to either read your file and generate a hash out of it what rev-append does or just generate a hash(timestamp or revision) and replace the query string every time regardless of file being changed or not. This way regardless of file contents changes or not, you have a new query string every time appended to file. This is bit faster than the first option, as it does not require to read the contents of file every time and generate a hash based on it.  

## RegularExpression

```sh
var FILE_DECL = /(?:href=|src=|url\()['|"]([^\s>"']+?)\?rev=([^\s>"']+?)['|"]/gi;
```


## Usage

We can use [gulp-rev-timestamp](https://github.com/vinothbabu/gulp-rev-timestamp) to cache-bust several assets and generate timestamp or hash or revision.

```js
var gulp = require('gulp');
var revts = require('gulp-rev-timestamp');

gulp.task('rev-timestamp', function() {
  gulp.src("index.html")
    .pipe(revts())
    .pipe(gulp.dest('.'))
});



```

### Options

#### default

With no optional parameter sent, the strict mode would false, mode would be type of timestamp.

```js
var gulp = require('gulp');
var revts = require('gulp-rev-timestamp');

gulp.task('rev-timestamp', function() {
  gulp.src("index.html")
    .pipe(revts({strict: true}))
    .pipe(gulp.dest('.'))
});


```

The above task would replace any

```js
<!-- Minified Files -->
<script src="../path/config.min.js?rev=@@hash"></script>
<script src="../path/app.min.js?rev=@@hash"></script>
<script src="../path/serivices.min.js?rev=@@hash"></script>
<!-- Minified Files -->

```

to below with a hash of timestamp, regardless of file being changed or not:

```js
<!-- Minified Files -->
<script src="../path/config.min.js?rev=1e7aa69df74343571bf4977b685cb496"></script>
<script src="../path/app.min.js?rev=1ed8a9d8c7aa5de44043ca86e9624248"></script>
<script src="../path/serivices.min.js?rev=341a3c405f3445e8a0d908ff1a4542ab"></script>
<!-- Minified Files -->

```


#### strict

Type : `Boolean`<br>
Default: `false`

You set a flag, strict, which will check if the file exist in relative path and also generate a hash and append to query string only if file content has changed. Default value is `false`.

```js
var gulp = require('gulp');
var revts = require('gulp-rev-timestamp');

gulp.task('rev-timestamp', function() {
  gulp.src("index.html")
    .pipe(revts({strict: true}))
    .pipe(gulp.dest('.'))    
});


```

The above task would replace any

```js
<!-- Minified Files -->
<script src="../path/config.min.js?rev=@@hash"></script>
<script src="../path/app.min.js?rev=@@hash"></script>
<script src="../path/serivices.min.js?rev=@@hash"></script>
<!-- Minified Files -->

```

to below with a hash of content of file only if the file content has changed:

```js
<!-- Minified Files -->
<script src="../path/config.min.js?rev=51dc1baa4a2dac96097d56de62d860a3"></script>
<script src="../path/app.min.js?rev=7a5a2adc42842b0e2b317440cdc2957f"></script>
<script src="../path/serivices.min.js?rev=46abc154eb09e362ad9ae4f7e69868dc"></script>
<!-- Minified Files -->

```

#### mode

Type : `String`<br>
Default: `timestamp`

Specifies the type of hash you would like to append to your query string (timestamp or revision)

```js
var gulp = require('gulp');
var revts = require('gulp-rev-timestamp');

gulp.task('rev-timestamp', function() {
  gulp.src("index.html")
    .pipe(revts({strict: false, mode: 'timestamp'}))
    .pipe(gulp.dest('.'))
});

```

When mode => revision

```js
var gulp = require('gulp');
var revts = require('gulp-rev-timestamp');

gulp.task('rev-timestamp', function() {
  gulp.src("index.html")
    .pipe(revts({strict: false, mode: 'revision', revision: '55'}))
    .pipe(gulp.dest('.'))
});

```

The above task would replace any

```js
<!-- Minified Files -->
<script src="../path/config.min.js?rev=@@hash"></script>
<script src="../path/app.min.js?rev=@@hash"></script>
<script src="../path/serivices.min.js?rev=@@hash"></script>
<!-- Minified Files -->

```

to below with a revision, preferrably coming from svn repo global version also does not check whether the contents of file has been changed or not:

```sh
<!-- Minified Files -->
<script src="../path/config.min.js?rev=55"></script>
<script src="../path/app.min.js?rev=55"></script>
<script src="../path/serivices.min.js?rev=55"></script>
<!-- Minified Files -->

```

## License

[MIT](http://opensource.org/licenses/MIT) © [Vinoth Babu]
