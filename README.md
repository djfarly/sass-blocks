# SassBlocks 
SassBlocks introduces a pattern to make working with bem-blocks/modules in Sass/Scss a little more oop.

# Install
Install SassBlocks via Bower or npm.

## Bower
```
bower install sass-blocks --save-dev
```

## npm
```
npm install sass-blocks --save-dev
```

# Usage
Make sure to import the _sass-blocks.scss file.
```scss
@import "path/to/sass-blocks";
```

SassBlocks proposes a pattern where you first declare all variables that should be local to the current block into the sass map `$this`.
Inside the block only those variables are used. Block variables are only ever accessed via the `this()` function.
After the blocks execution `$this` is reset.

```scss
// Each block should live in it's seperate file.
// To begin declare all internal variables for this block.
// Reference any external variables that will be used in here.
// Think of this as a 'constructor'.

$this: (
    // Block name
    block:                  my-block,

    // Block variables
    height:                 100px,
    subheight:              $global-height-value,
    somecolor:              $global-color-brand,
);

// Define your block.
// This does not need to follow bem-principles, but it certainly can't hurt. ;)
// Do not use any global variables in here!

.#{this(block)} {
    height: this(height);

    &__element {
        height: this(subheight);

        &--modifier {
            color: this(somecolor);
        }
    }
}

// Remember to unset $this. This way we fake scoping it to that file.
$this: null;
```

Remember that using SassBlocks reserves the `$this` variable.

The actual function itself isn't that big of deal. `this()` just makes accessing the `$this` map a bit less verbose.
```scss
// 'old'
$foo = map-get($this, bar);
// the SassBlocks way
$foo = this(bar);
```
