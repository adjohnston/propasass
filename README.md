# PropaSass

The idea behind PropaSass is to abstract state and modifier styling from base classes, using JSON-like syntax using a Sass map. (_I am dubbing it SAMN or Sass Map Notation… pronounced salmon ;D_)

##A Quick Demo
I am going to use a simple button example to show off the syntax and how it can be applied:

    $props: (
      null: (
        ':hover, :focus': (
          height: 38px, margin-top: 2px, background: darken(grey, 10%)
        ),
        ':focus': (
          outline: none
        ),
        ':active': (
          height: 36px, margin-top: 4px
        )
      ),
      '--': (
        'primary': (
          background: blue, border-color: darken(blue, 10%)
        ),
        'primary:hover, primary:focus': (
          background: darken(blue, 10%)
        ),
        'warning': (
          background: red, border-color: darken(red, 10%)
        ),
        'warning:hover, warning:focus': (
          background: darken(red, 10%)
        )
      ),
      '.is-': (
        'active': (
          animation: glow infinite 3s
        )
      )
    );

    .btn {
      width: 150px;
      height: 40px;
      background: grey;
      border: 1px solid darken(grey, 10%);
      color: white;
      display: inline-block;
      vertical-align: bottom;
    
      @include modify-with($props);
    }
