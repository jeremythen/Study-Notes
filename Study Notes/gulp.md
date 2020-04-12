
Each gulp task is an asynchronous JavaScript function

# Exporting
Tasks can be considered public or private.

* Public tasks are exported from your gulpfile, which allows them to be run by the gulp command.
* Private tasks are made to be used internally, usually used as part of series() or parallel() composition.

# Compose tasks

* To have your tasks execute in order, use the series() method.
* For tasks to run at maximum concurrency, combine them with the parallel() method.


series() and parallel() can be nested to any arbitrary depth.

```javascript
exports.build = series(
  clean,
  parallel(
    cssTranspile,
    series(jsTranspile, jsBundle)
  ),
  parallel(cssMinify, jsMinify),
  publish
);
```
