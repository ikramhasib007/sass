# SASS
SASS documentary
# Setup
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
