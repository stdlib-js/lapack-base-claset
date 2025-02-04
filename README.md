<!--

@license Apache-2.0

Copyright (c) 2025 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# claset

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Set the off-diagonal elements and the diagonal elements of a single-precision complex floating-point matrix to specified values.



<section class="usage">

## Usage

To use in Observable,

```javascript
claset = require( 'https://cdn.jsdelivr.net/gh/stdlib-js/lapack-base-claset@umd/browser.js' )
```

To vendor stdlib functionality and avoid installing dependency trees for Node.js, you can use the UMD server build:

```javascript
var claset = require( 'path/to/vendor/umd/lapack-base-claset/index.js' )
```

To include the bundle in a webpage,

```html
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/lapack-base-claset@umd/browser.js"></script>
```

If no recognized module system is present, access bundle contents via the global scope:

```html
<script type="text/javascript">
(function () {
    window.claset;
})();
</script>
```

#### claset( order, uplo, M, N, alpha, beta, A, LDA )

Sets the off-diagonal elements and the diagonal elements of a single-precision complex floating-point matrix to specified values.

```javascript
var Complex64Array = require( '@stdlib/array-complex64' );
var Complex64 = require( '@stdlib/complex-float32-ctor' );
var realf = require( '@stdlib/complex-float32-real' );
var imagf = require( '@stdlib/complex-float32-imag' );

var A = new Complex64Array( 4 );

var alpha = new Complex64( 1.0, 2.0 );
var beta = new Complex64( 3.0, 4.0 );

claset( 'row-major', 'all', 2, 2, alpha, beta, A, 2 );

var z = A.get( 0 );
// returns <Complex64>

var re = realf( z );
// returns 3.0

var im = imagf( z );
// returns 4.0

z = A.get( 1 );
// returns <Complex64>

re = realf( z );
// returns 1.0

im = imagf( z );
// returns 2.0
```

The function has the following parameters:

-   **order**: storage layout.
-   **uplo**: specifies whether to set the upper or lower triangular/trapezoidal part of a matrix `A`.
-   **M**: number of rows in `A`.
-   **N**: number of columns in `A`.
-   **alpha**: value assigned to off-diagonal elements.
-   **beta**: value assigned to diagonal elements.
-   **A**: input [`Complex64Array`][@stdlib/array/complex64].
-   **LDA**: stride of the first dimension of `A` (a.k.a., leading dimension of the matrix `A`).

Note that indexing is relative to the first index. To introduce an offset, use [`typed array`][mdn-typed-array] views.

<!-- eslint-disable stdlib/capitalized-comments -->

```javascript
var Complex64Array = require( '@stdlib/array-complex64' );
var Complex64 = require( '@stdlib/complex-float32-ctor' );
var realf = require( '@stdlib/complex-float32-real' );
var imagf = require( '@stdlib/complex-float32-imag' );

// Initial array:
var A0 = new Complex64Array( 5 );

// Create offset view:
var A1 = new Complex64Array( A0.buffer, A0.BYTES_PER_ELEMENT*1 ); // start at 2nd element

var alpha = new Complex64( 1.0, 2.0 );
var beta = new Complex64( 3.0, 4.0 );

claset( 'row-major', 'all', 2, 2, alpha, beta, A1, 2 );

var z = A0.get( 1 );
// returns <Complex64>

var re = realf( z );
// returns 3.0

var im = imagf( z );
// returns 4.0
```

#### claset.ndarray( uplo, M, N, alpha, beta, A, sa1, sa2, oa )

Sets the off-diagonal elements and the diagonal elements of a single-precision complex floating-point matrix to specified values using alternative indexing semantics.

```javascript
var Complex64Array = require( '@stdlib/array-complex64' );
var Complex64 = require( '@stdlib/complex-float32-ctor' );
var realf = require( '@stdlib/complex-float32-real' );
var imagf = require( '@stdlib/complex-float32-imag' );

var A = new Complex64Array( 4 );

var alpha = new Complex64( 1.0, 2.0 );
var beta = new Complex64( 3.0, 4.0 );

claset.ndarray( 'all', 2, 2, alpha, beta, A, 2, 1, 0 );

var z = A.get( 0 );
// returns <Complex64>

var re = realf( z );
// returns 3.0

var im = imagf( z );
// returns 4.0

z = A.get( 1 );
// returns <Complex64>

re = realf( z );
// returns 1.0

im = imagf( z );
// returns 2.0
```

The function has the following parameters:

-   **uplo**: specifies whether to set the upper or lower triangular/trapezoidal part of a matrix `A`.
-   **M**: number of rows in `A`.
-   **N**: number of columns in `A`.
-   **alpha**: value assigned to off-diagonal elements.
-   **beta**: value assigned to diagonal elements.
-   **A**: input [`Complex64Array`][@stdlib/array/complex64].
-   **sa1**: stride of the first dimension of `A`.
-   **sa2**: stride of the second dimension of `A`.
-   **oa**: starting index for `A`.

While [`typed array`][mdn-typed-array] views mandate a view offset based on the underlying buffer, the offset parameter supports indexing semantics based on a starting index. For example,

```javascript
var Complex64Array = require( '@stdlib/array-complex64' );
var Complex64 = require( '@stdlib/complex-float32-ctor' );
var realf = require( '@stdlib/complex-float32-real' );
var imagf = require( '@stdlib/complex-float32-imag' );

var A = new Complex64Array( 5 );

var alpha = new Complex64( 1.0, 2.0 );
var beta = new Complex64( 3.0, 4.0 );

claset.ndarray( 'all', 2, 2, alpha, beta, A, 2, 1, 1 );

var z = A.get( 0 );
// returns <Complex64>

var re = realf( z );
// returns 0.0

var im = imagf( z );
// returns 0.0

z = A.get( 1 );
// returns <Complex64>

re = realf( z );
// returns 3.0

im = imagf( z );
// returns 4.0
```

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   `claset()` corresponds to the [LAPACK][lapack] routine [`claset`][lapack-claset].

</section>

<!-- /.notes -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```html
<!DOCTYPE html>
<html lang="en">
<body>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/array-complex64@umd/browser.js"></script>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/complex-float32-ctor@umd/browser.js"></script>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-base-to-array@umd/browser.js"></script>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-base-numel@umd/browser.js"></script>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-base-shape2strides@umd/browser.js"></script>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/lapack-base-claset@umd/browser.js"></script>
<script type="text/javascript">
(function () {

var shape = [ 5, 8 ];
var order = 'row-major';
var strides = shape2strides( shape, order );

var N = numel( shape );

var A = new Complex64Array( N );
console.log( ndarray2array( A, shape, strides, 0, order ) );

var alpha = new Complex64( 1.0, 2.0 );
var beta = new Complex64( 3.0, 4.0 );

claset( order, 'all', shape[ 0 ], shape[ 1 ], alpha, beta, A, strides[ 0 ] );
console.log( ndarray2array( A, shape, strides, 0, order ) );

})();
</script>
</body>
</html>
```

</section>

<!-- /.examples -->

<!-- C interface documentation. -->



<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library for JavaScript and Node.js, with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2025. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/lapack-base-claset.svg
[npm-url]: https://npmjs.org/package/@stdlib/lapack-base-claset

[test-image]: https://github.com/stdlib-js/lapack-base-claset/actions/workflows/test.yml/badge.svg?branch=main
[test-url]: https://github.com/stdlib-js/lapack-base-claset/actions/workflows/test.yml?query=branch:main

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/lapack-base-claset/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/lapack-base-claset?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/lapack-base-claset.svg
[dependencies-url]: https://david-dm.org/stdlib-js/lapack-base-claset/main

-->

[chat-image]: https://img.shields.io/gitter/room/stdlib-js/stdlib.svg
[chat-url]: https://app.gitter.im/#/room/#stdlib-js_stdlib:gitter.im

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/lapack-base-claset/tree/deno
[deno-readme]: https://github.com/stdlib-js/lapack-base-claset/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/lapack-base-claset/tree/umd
[umd-readme]: https://github.com/stdlib-js/lapack-base-claset/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/lapack-base-claset/tree/esm
[esm-readme]: https://github.com/stdlib-js/lapack-base-claset/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/lapack-base-claset/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/lapack-base-claset/main/LICENSE

[lapack]: https://www.netlib.org/lapack/explore-html/

[lapack-claset]: https://www.netlib.org/lapack/explore-html/d0/de5/group__laset_ga7149b3d5cf0e2b410d4664110a43139f.html#ga7149b3d5cf0e2b410d4664110a43139f

[@stdlib/array/complex64]: https://github.com/stdlib-js/array-complex64/tree/umd

[mdn-typed-array]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray

</section>

<!-- /.links -->
