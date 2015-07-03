# watson-perl  
### an inline todo and issue manager
[watson](http://goosecode.com/watson) ([mirror](http://nhmood.github.io/watson-perl)) is a tool for creating and tracking bug reports, issues, and internal notes in code.    

### See watson in action [here](http://goosecode.com/watson) ([mirror](http://nhmood.github.io/watson-perl))

## Installation
watson-perl has been tested with **Perl v5.18.1** (on **Arch Linux**)  
watson-perl is self contained in a single file and has **no** CPAN dependencies.  

### From Repo  
The easiest way to get watson-perl is probably...
```
# Download watson to current directory with wget
# and set watson to executable
wget https://raw.github.com/nhmood/watson-perl/master/watson -O watson
sudo chmod +x watson 

# OR Download watson to current directory with curl
# and set watson to executable
curl http://github.com/nhmood/watson-perl/watson-perl -o watson
sudo chmod +x watson 

# Copy watson to /usr/bin, which is most likely in your PATH
sudo cp watson /usr/bin

# OR make a soft link to it into /usr/bin
sudo ln -s watson /usr/bin

```
You could clone the repo and then perform the linking step so all you need to do to update watson-perl is a ```git pull``` to stay up to date without having to redownload.  


### Script Install (Coming soon...)  
There will probably be a install script in the style of ``` wget link-to-script | sh ``` at some point.  
Some people aren't a fan of this but it is the most convinient. Feel free to implement this and submit a pull request!

## Usage
For a quick idea of how to use watson, check out the [app demo](http://goosecode.com/watson)! ([mirror](http://nhmood.github.io/watson-perl))   
See below for a description of what all the command line arguments do.

## Command line arguments
```
Usage: watson [OPTION]...
Running watson with no arguments will parse with settings in RC file
If no RC file exists, default RC file will be created
List elements are space separated

   -d, --dirs                   list of directories to search in
   -f, --files                  list of files to search in
   -h, --help                   print help
   -i, --ignore                 list of files, directories, or types to ignore
   -p, --parse-depth            depth to recursively parse directories
   -r, --remote                 list / create tokens for Bitbucket/Github
   -t, --tags                   list of tags to search for
   -v, --version                print watson version and info

Report bugs to: eugene@kolobyte.com
watson home page: <http://goosecode.com/projects/watson>
[kolobyte] | 2015-
[goosecode] labs | 2012-2013
```
### -d, --dirs [DIRS]  
This parameter specifies which directories watson should parse through.  
It should be followed by a space separated list of directories that should be parsed.  
If watson is run without this parameter, the current directory is parsed.  


### -f, --files [FILES]
This parameter specifies which files watson should parse through.  
It should be followed by a space separated list of files that should be parsed.  


### -h, --help
This parameter displays the list of avaliable options for watson.


### -i, --ignore [IGNORES]
This parameter specifies which files and directories watson should ignore when parsing.  
It should be followed by a space separated list of files and/or directories to be ignored.  
This parameter should be used as an opposite to -d/-f, when there are more files that should be parsed in a directory than should be ignored.


### -p, --parse-depth [PARSE_DEPTH]
This parameter specifies how deep watson should recursively parse directories.  
The 'depth' is defined as how many levels deep from the top-most specified directory to parse.  
If individual directories are passed with the -d (--dirs) flag, each will be parsed PARSE_DEPTH layers, regardless of their depth from the current directory.  
If watson is run without this parameter, the parsing depth is unlimited and will search through all subdirectories found.


### -r, --remote [GITHUB, BITBUCKET]
This parameter is used to both list currently established remotes as well as setup new ones.  
If passed without any options, the currently established remotes will be listed.  
If passed with a github or bitbucket argument, watson will proceed to ask some questions to set up the corresponding remote.  


### -t, --tags [TAGS]
This parameter is used to specify which tags watson should look for when parsing.  
The tag currently supports any regular character and number combination, no special (!@#$...) characters.  


## -v, --version
This parameter displays the current version of watson you are running.


## .watsonrc
watson supports an RC file that allows for reusing commong settings without repeating command line arguments every time.  

The .watsonrc is placed in every directory that watson is run from as opposed to a unified file (in ~/.watsonrc for example). The thinking behind this is that each project may have a different set of folders to ignore, directories to search through, and tags to look for.  
For example, a C/C++ project might want to look in src/ and ignore obj/ whereas a Ruby project might want to look in lib/ and ignore assets/.  

The .watsonrc file is fairly straightforward...  
**[dirs]** - This is a newline separated list of directories to look in while parsing.  
**[tags]** - This is a newline separated list of tags to look for while parsing.  
**[ignore]** - This is a newline separated list of files / folders to ignore while parsing.
This supports wildcard type selecting by providing .filename (no * required)  
**[(github/bitbucket)]** - If a remote is established, the API key for the corresponding remote is stored here.  
Currently, OAuth has yet to be implemented for Bitbucket so the Bitbucket username is stored here.
**[(github/bitbucket)_repo]** - The repo name / path is stored here.  
**[tag_format]** - The format of the comment tag to search for, TAG, COMMENT, and USERNAME are required.
The remote related .watsonrc options shouldn't need to be edited manually, as they are automatically populated when the -r, --remote setup is called.

## Special Thanks
Special thanks to [@samirahmed](http://twitter.com/samirahmed) for his super Ruby help and testing watson-ruby!  
Special thanks to [@eugenekolo](http://twitter.com/eugenekolo) [[email](eugene@kolobyte.com)] for his super Perl help!
Special thanks to [@crowell](http://github.com/crowell) for helping test out watson-ruby!
