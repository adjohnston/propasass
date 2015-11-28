# PropaSass

The idea behind PropaSass is to abstract state and modifier styling from base classes, using JSON-like syntax using a Sass map. I am dubbing it SAMN or Sass Map Notation… pronounced salmon ;D

I have written about it [here](https://medium.com/@adrjohnston/propasass-aaa0966efe1e) if you would like more  information.

##A Quick Demo
I am going to use a simple button example to show off the syntax and how it can be applied:

    //  _button.scss

    $btnProps: (
      width: 150px,
      height: 40px,
      background: grey,
      border: 1px solid darken(grey, 10%),
      color: white,
      display: inline-block,
      vertical-align: bottom,
    );

    $btnModifyProps: (
      &: (
        ':hover, :focus': (height: (map-get($btnProps, height) - 2px), margin-top: 2px, background: darken(map-get($btnProps, background), 10%)),
        ':focus': (outline: none),
        ':active': (height: (map-get($btnProps, height) - 4px), margin-top: 4px)
      ),
      '--': (
        'primary': (background: blue, border-color: darken(blue, 10%)),
        'primary:hover, primary:focus': (background: darken(blue, 10%)),
        'warning': (background: red, border-color: darken(red, 10%)),
        'warning:hover, warning:focus': (background: darken(red, 10%))
      ),
      '.is-': (
        'active': (animation: glow infinite 3s)
      )
    );
    

    .btn {
      @include define-with($btnProps);
      @include modify-with($btnModifyProps);
    }
    
    
    //  _another-partial.scss
    
    $dialogProps: (
      ...
    );
    
    $dialogBtnProps: (
      //  specific dialog button styles mixed
    );
    
    
    .dialog {
      @include define-with($dialogProps);
      
      &__btn {
        @include define-with(assign($btnProps, $dialogBtnProps));
      }
    }
