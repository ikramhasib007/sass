# SASS
SASS documentary
# Setup
> Editor: I use sublime
  - Plugins list:
    - SASS
    - SASS Build
    - SCSS
    - SASSonSaveBuild
> Need to install Ruby
  - go to [RubyInstaller](https://rubyinstaller.org/) download and install
  - then go to your command prompt and install sass on your machine using this command: `gem install sass`
> Sublime auto build setup:
  - setup your project folder structures like 
    - css
    - scss
  - go to on your sublime menu: Tools > Build System > New Build System
  - then setup like this.
  ```{

  "cmd": ["sass", "--update", "$file:${file_path}/../css/${file_base_name}.css", "--stop-on-error", "--no-cache"],

  "osx":
  {
      "path": "/usr/local/bin:$PATH"
  },

  "windows":
  {
      "shell": "true"
  }

}```
