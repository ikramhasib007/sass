# SASS
SASS Documentation
## Setup
> Editor: I use sublime. you can use whatever you want
  - Plugins list:
    - SASS
    - SASS Build
    - SCSS
    - SublimeOnSaveBuild
> Need to install Ruby
  - go to [RubyInstaller](https://rubyinstaller.org/) download and install
  - then go to your command prompt and install sass on your machine using this command: `gem install sass`
> Sublime auto build setup:
  - setup your project folder structures like 
    - css
    - scss
  - go to on your sublime menu: Tools > Build System > New Build System
  - then setup like this.
  ```
 {

  "cmd": ["sass", "--update", "$file:${file_path}/../css/${file_base_name}.css", "--stop-on-error", "--no-cache"],

  "osx":
  {
      "path": "/usr/local/bin:$PATH"
  },

  "windows":
  {
      "shell": "true"
  }

}
```
  > [x] Then write your scss code and save it and enjoy!

## Create partials 
  - Partials file name should be start with a underscore and extension scss
  - Underscore define it's a partials file and that file shouldn't compiled

  - setup your `SublimeOnSaveBuild` plugins for partials file not compiled like this.
  - go to Preferences > Package Settings > SublimeOnSaveBuild > Settings - User
  - copy and paste the code below and save it.
  ```
{
    "filename_filter": "(/|\\\\|^)(?!_)(\\w+)\\.(css|js|sass|less|scss)$",
    "build_on_save": 1
}
```
  - Import the partials
    - Using `@import` with filename without underscore. like:
    - `@import "variables";`

## Create Mixin
  - Mixin is a reusable style pattern. Reusable pieces of style.
  - create mixin like:
    ```
    @mixin warning {
      background-color: orange;
      color: #fff;
    }
    ```
  - Use mixin like:
    ```
    .btn-warning {
      @include warning;
      padding: 8px 12px;
    }
    ```

## Short syntax for styles
  - Normal syntax:
    ```
      font-size: 22px;
      font-weight: bold;
    ```
  - SASS or SCSS syntax:
    ```
      font: {
          size: 22px;
          weight: bold;
        }
    ```

## Mixin with arguments
  - Syntax:
    ```
    @mixin rounded($radius) {
      border-radius: $radius;
    }

    @mixin box($radius, $border) {
      @include rounded($radius);
      border: $border;
    }
    ```
  - Use case:
    ```
    #header {
      @include box(4px, 1px solid #eee);
      height: $header-height;
      background-color: #ccc;
    }
    ```

## Mixin with default arguments
  - Syntax:
    ```
    @mixin rounded($radius: 4px) {
      border-radius: $radius;
    }

    @mixin box($radius: 4px, $border: 1px solid #ccc) {
      @include rounded($radius);
      border: $border;
    }
    ```
  - Use case:
    ```
    /* With two parametter */
    #header {
      @include box(4px, 1px solid #eee);
      height: $header-height;
      background-color: #ccc;
    }
    
    /* With no parametter */
    #header {
      @include box;
      height: $header-height;
      background-color: #ccc;
    }

    /* With first parametter */
    #header {
      @include box(4px);
      height: $header-height;
      background-color: #ccc;
    }

    /* With second parametter. when use only second parametter then use exact variable name of your mixin */
    #header {
      @include box($border: 1px solid #eee);
      height: $header-height;
      background-color: #ccc;
    }

    /* Expicity use with argument name of your mixin */
    #header {
      @include box($border: 1px solid #eee, $radius: 4px);
      height: $header-height;
      background-color: #ccc;
    }
    ```

## Mixin with multiple argument value (bar arc)
  - Syntax:
    ```
    @mixin box-shadow($shadows...) {
      box-shadow: $shadows;
      -moz-box-shadow: $shadows;
      -webkit-box-shadow: $shadows;
    }
    ```
  - Use case:
    ```
    #header {
      @include box(4px, 1px solid $ternary-color);
      @include box-shadow(2px 0px 4px #999, 1px 1px 6px $secondary-color);
      height: $header-height;
      background-color: #ccc;
    }
    ```

## Mixin content passing for specific browser.
  - For IE 6
    - Syntax:
      ```
      @mixin apply-to-ie-6 {
        * html {
          @content;
        }
      }
      ```
    - Use case:
      ```
      @include apply-to-ie-6 {
        body {
          font-size: 125%;
        }
      }
      ```

## Import
  - 4 types of import in css
    - @import url();
    - @import "http://...."
    - @import "filename.css"
    - @import "style-screen" screen; // this stylesheet only apply for screen

  - Import using interpolation `#{variable_name}`
    - Syntax:
      ```
      @mixin google-font($font) {
        $font: unquote($font);
        @import url(http://fonts.googleapis.com/css?family=#{$font})
      }
      ```
    - Use case:
      ```
      @include google-font("Archivo");
      ```