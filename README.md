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
