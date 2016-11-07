# gulp-rev-timestamp

gulp-rev-timestamp provides you an option to either read your file and generate a hash out of it or just generate a hash(timestamp or revision) without checking the existance of the files and just replacing the query string every time regardless of file being changed or not.

## Install
```sh
$ npm install --save-dev gulp-rev-timestamp
```
## Why another plugin?

This plugin is based on gulp-rev-append which is very good and in some cases even better, because it relies on file hash, so if file didn't change between versions, the hash will remain the same so file can stay in cache.

gulp-rev-timestamp provides you an option to either read your file and generate a hash out of it what rev-append does or just generate a hash(timestamp or revision) and replace the query string every time regardless of file being changed or not. This way regardless of file contents changes or not, you have a new query string every time appended to file. This is bit faster than the first option, as it does not require to read the contents of file every time and generate a hash based on it.  

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

Type : `String`<br>
Default: `timestamp`

```js
var gulp = require('gulp');
var revts = require('gulp-rev-timestamp');

gulp.task('rev-timestamp', function() {
  gulp.src("index.html")
    .pipe(revts({strict: false, mode: 'revision', revision: '55'}))
    .pipe(gulp.dest('.'))
});

```
## License

[MIT](http://opensource.org/licenses/MIT) © [Vinoth Babu]
