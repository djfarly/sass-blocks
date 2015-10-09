# SassBlocks 
SassBlocks introduces a pattern to make working with bem-blocks/modules a little more oop.

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
Import the _sass-blocks.scss file.
```
scss
@import "path/to/dist/math";
```

SassBlocks is intended to be used like this:

```
scss
// Each block should live in it's seperate file.
// To begin declare all internal variables for this block.
// Reference any external variables that will be used in here.
// Think of this as a constructor.

$this: (
    // Modulename
    module:                 module,

    // Module Variables
    height:                 100px,
    subheight:              $global-height-value,
    somecolor:              $color-brand,
);

// Define your module.
// This does not need to follow bem-principles, but it certainly can't hurt. ;)
// Do not use any global variables in here!

.#{this(module)} {
    height: this(height);

    &__element {
        height: this(subheight);

        &--modifier {
            color: this(somecolor);
        }
    }
}

// Remember to unset $this. This way we fake scoping to that file.
$this: null;
```

Remember that using SassBlocks reserves the $this variable.
