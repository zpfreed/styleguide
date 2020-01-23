# [Sass](http://sass-lang.com)

Preference to `.scss` syntax over `.sass`.

## SUIT + BEM

Both [SUIT CSS][1] and [BEM][2] are really great conventions to follow, but BEM can lack specificity and SUIT can lead to too much specificity. There is a happy medium that we can follow that combines the best of both worlds.

### Examples

#### Good
```
.t-btn {
  display: block;
  color: $color--orange;
  @include u-weight(demi);

  &:hover {
    opacity: 0.4;
  }

  @at-root #{&}-- {

    &primary {
      background-color: $color--gray-1;
    }
  }
}
```

Notice the spacing between things that represent new selectors or new blocks. This makes it easier to parse and organize properties and child selectors.

#### Bad
```
.t-btn {
  display: block; color: $color--orange;  // 1

  @include u-weight(demi);                // 2
  &:hover {                               // 3
    opacity: 0.4;
  }
  @at-root #{&}-- {                       // 4
    &primary {                            // 3
      background-color:$color--gray-1;    // 5
      color: white                        // 6
    }
  }
}
```
1. Don't inline multiple properties
2. Pay attention to whitespace between neighboring nested blocks and mixins that produce properties as opposed to something like the `@include media()` mixin. Use space between these blocks, but not before or after.
3. When forming a new selector via `&`, new child classes, etc, skip a line.
4. Same as #3, when forming new selectors or child selectors, skip a line.
5. Make sure to keep property structure clean with a single space between . `property: value;`.
6. Always use semi-colons, even at the end of a block of properties.

### Class naming
```
.t-btn {}
.t-btn__container {}
.t-btn--primary {}
```

#### Compound classes

```
.t-btn {
  // t-btn properties

  // elements
  @at-root #{&}__ {

    &container {}

    &block {}
  }

  // modifiers
  @at-root #{&}-- {

    &primary {}

    &secondary {}
  }
}
```

* prefer [BEM][3] convention for selectors
* prefer `is-` syntax for states and utilities over BEM modifiers whenever possible (if needed)
* prefer double quotes (unless single is required)

[1]: https://suitcss.github.io/
[2]: http://getbem.com/introduction/
[3]: http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/
