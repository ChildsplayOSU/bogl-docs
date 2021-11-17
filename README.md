# BoGL Docs 
BoGL Docs is the official tutorial website for BoGL (Board Game Language), a domain specific teaching language designed to introduce computer science concepts.

## Site Structure

BoGL Docs was created with [Jekyll](https://jekyllrb.com/) and uses a modified version of the [rundocs](https://rundocs.io) theme.

### Directories
- **_data:**  
There is a single file in this directory named *glossary_terms.yml*. The glossary page is populated with the definitions that are written in this file.
- **_includes:**  
Several partials are contained here (like the footer and header, which are located in the *class* subdirectory). Inside this folder are also *code\_module\_template.html* and *excercise\_module\_template.html*, which are the modular BoGL interpreters that are used inside the tutorials.
- **_layouts:**  
Located in this directory is *default.liquid*, which uses the partials from *_includes/class*.
- **assets:**  
Site assets such as fonts and the favicon images are located here.
- **imgs:**  
The images used in the tutorials are located here.
- **tutorials:**  
This is where the tutorials are located. Each tutorial is written as a markdown (.md) file.

### Files
- **README.md:**  
The file you are reading right now. Contains information about the repository for the website.
- **_config.yml**  
Configuration file. Contains various options for the site.
- **index.md**  
The BoGL Docs index page.


## Source Info

This website was created from a fork of the [rundocs/starter-slim](https://github.com/rundocs/starter-slim/) jekyll theme, which is available as open source under the terms of the MIT License.
Documentation for the rundocs theme can be found at [rundocs.io](https://rundocs.io).

## How to run the website locally

# Mac
### 1) Install Ruby
  - If you don't have [homebrew](https://brew.sh/) already installed, install it
  - In terminal, use the command `brew install ruby` to install [ruby](https://jekyllrb.com/docs/installation/macos/)
### 2) Add ruby and gem baths to your shell configuration
  - To find shell configuration type the command `echo $SHELL`
    - If you have Zsh enter the command: `echo 'export PATH="/usr/local/opt/ruby/bin:/usr/local/lib/ruby/gems/3.0.0/bin:$PATH"' >> ~/.zshrc`
    - If you have Bash enter the command: `echo 'export PATH="/usr/local/opt/ruby/bin:/usr/local/lib/ruby/gems/3.0.0/bin:$PATH"' >> ~/.bash_profile`
### 3) Install Jekyll
  - Relaunch terminal and type the command: `gem install --user-install bundler jekyll`
  - Get your ruby version by using the command `ruby -v`
### 4) Append ruby to path file
  - Depeding on shell, use the following command AND replace the X.X with the version of ruby
    - Zsh: `echo 'export PATH="$HOME/.gem/ruby/X.X.0/bin:$PATH"' >> ~/.zshrc`
    - Bash: `echo 'export PATH="$HOME/.gem/ruby/X.X.0/bin:$PATH"' >> ~/.bash_profile`
### 5) Clone bogl-docs to your local computer
  - Click the green code button on the home page & copy the https link
  - In terminal, find the directory you want bogl-docs to go to and use the command: git clone "PASTE HTTPS"
### 6) Adding webrick to gemfile
  - Add this line of code into your gemfile: `gem "webrick", "~>1.7"`
    - To do this, either vim into "Gemfile" or use a text editor and append the webrick line of code to the end of the file.
### 7) Running a local version
  - To run a local version, use the command: `bundle exec jekyll serve`
  - There will be an IP address generated in your terminal, paste that into your browser
  - Use ctl+c to cancle the local server running

