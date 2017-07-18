# bbsh
Bitbake Shell Wrapper Script
  
# Description:
Script to create a 'clean' shell environment for Bitbake builds to occur.  
   The intent is to prevent contamination of the host shell environment *AND* to prevent contamination of the build shell.

# Modes of operation
* direct execution mode:  bbsh < options > -- < command > < command options >  
   Ex:  bbsh -d -b ../ -- bitbake-layers --help
* shell creation mode  :  bbsh < options >  
   Ex:  bbsh -d -b ../
  
# Configuration Files
Configuration files tailor the defaults of this script.  
   Files will be searched and sourced in the following order:
* Location of the script file itself, e.g. ~/bin/bbsh.conf
* Current working directory, e.g. ./bbsh.conf
* Build directory, if it exists, e.g. \${BUILD_DIR}/bbsh.conf
* Command line specified configuration file.

### Allowed Configuration File Variables
DEBUG, INIT_ARGS, INIT_SETUP_SCRIPT, PREPEND_PATHS, SETUP_SCRIPT

### LIMITATIONS
1) Currently, configuration parsing is rudimentary and only works for single line entries.

# Usage

```
bbsh < options > -- < command > < command options >  
    -b|--build <build dir>   build execution directory, defaults to ./  
    -c|--config <file>       add a configuration file to use  
    -d|--debug               enable debug output  
    -h|--help  
    -i|--init                initial invocation will create the build directory  
      |--init-args           arguments to pass during the initial invocation  
      |--init-setup--script  script to call for the initial invocation  
    -l|--layer <layer dir>   meta-data layers directory, defaults to <build>/../  
    -p|--paths <paths>       paths, delimited by ':', to prepend to \$PATH  
                               e.g.  --paths \"a:b:c\"  
    -s|--script <file>       setup script to run before execution  
                               defaults to <layer directory>/oe-init-build-env  
    -u|--user-conf-only      only use the conf file specified with -c  
```

# NOTE(s):
* Shells can be nested and will be indicated by the prompt
* Options that specify files assume relative paths to the calling directory for this script.
* Command line options should override anything in a configuration file
* Renaming the script will change the default configuration files searched
  
# TODO: 
1) Explore using chroot/schroot to provide more isolation to the build environment.
2) Make more shell agnostic and remove bash-isms
3) Add color to output
  
# MIT License
Copyright (c) 2017 Sean Hudson
  
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:
  
The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.


THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
