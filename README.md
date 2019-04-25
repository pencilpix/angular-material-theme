# Theming Angular Material

These settings contains the settings of scss for `angular material` and provides
helpers that helps in applications styling.

## table of content
1. modules that is customizable depending on the theme
2. global functions the work as helpers during theming the application
3. placeholders that could be extended to reduce the bundle size instead of classes (coming soon)
4. useful mixins to be used amoung different modules through the app.
5. it makes life easier when it comes to define a new theme for angular material.




## installation.

1. create a new file at your styles folder for example: `theme.scss`
2. import `src/theming.scss`
3. customize the theme and palette and settings variables if you need as:
    ```scss
    // settings of padding and base font size
    $font-size-base: 16; // by default
    $font-size-html: unquote('#{$font-size-base}px')

    // $primary, $accent, $warn, $gray
    // note gray is not used in theming but will be used
    // in global settings, variables, mixins and functions.
    @include override-palettes($mat-indigo, $mat-yellow, $mat-red, $mat-gray)

    // or with custom tones
    // will be compiled
    // $primary: mat-palette($mat-indigo, A400, A500)
    @include override-palettes($mat-indigo A400 A500, $mat-yellow, $mat-red, $mat-gray)
    ```

4. at the global `styles.scss` that is in your app root, import the aforementioned file `theme.scss`
   (created file in step 1) then include `init-material-theme`

   ```scss
   // this would initialize light theme by default
   @include init-material-theme();

   // to multiple themes
   .dark-theme {
     @include init-material-theme($dark-theme);
   }

  .light-theme {
     @include init-material-theme($theme);
  }
   ```

5. at `angular.json` add the following lines at `build.options`:
    ```json
      "stylePreprocessorOptions": {
          "includePaths": [
              "projects/project-name/src/styles"
          ]
        }
    ```

    then you are free to import the file created in step `1` (theme.scss)
    at any scss file for any component like `@import 'theme'`



full example

```scss
// app/src/styles/theme.scss
@import '~@angular/material/theming'
@import '~angular-material-theme/src/theming'

/* overriding palettes and variables */
$font-size-base: 16; /* by default */
$font-size-html: unquote('#{$font-size-base}px')
@include override-palettes($mat-purple, $mat-amber, $mat-red, $mat-gray);



// app/src/styles.scss
@import 'theme';
@include init-material-theme();


// at any scss/sass file
.classname {
  @extend %demo-placeholder;
  color: get(primary, 500);
}

// also you can extend whole element using `bem` mixin
// @include bem(placeholder, blockClass, element1 element2, modifier1 modifier2)
// instead of multiple includes for each block and it's elements.
@include bem(avatar, author, img icon, small medium large inverted);
// that would compile: author, author__img, author__icon, author--small, author--medium, ... etc
// with the applied styles to the placeholder
```
