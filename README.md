# watson-kolo
### an inline todo and issue manager
Watson is a tool for creating and tracking bug reports, issues, and internal notes in code.    
See watson in action [here](http://goosecode.com/watson) ([mirror](http://nhmood.github.io/watson-perl))

## Installation
watson-kolo is self contained in a single file and has **no** CPAN dependencies.  
```
# Download watson and set watson to executable
wget https://raw.github.com/nhmood/watson-perl/master/watson -O watson
sudo chmod +x watson 
sudo cp watson /usr/bin
```
You might want updates, if so you should clone the repo instead.
```
git clone git@github.com:eugenekolo/watson-perl.git
sudo chmod +x watson 
sudo ln -s watson /usr/bin
```

## Command line arguments
```
Usage: watson [OPTION]...
Running watson with no arguments will parse with settings in RC file
If no RC file exists, default RC file will be created
List elements are space separated

   -d, --dirs                   list of directories to search in, default: current dir
   -f, --files                  list of files to search in
   -h, --help                   print help
   -i, --ignore                 list of files, directories, or types to ignore
   -p, --parse-depth            depth to recursively parse directories, default: unlimited
   -r, --remote                 list / create tokens for 'GITHUB' or 'BITBUCKET'
   -t, --tags                   list of tags to search for, limited to [Aa-Zz0-9]
   -v, --version                print watson version and info

Report bugs to: eugene@kolobyte.com
watson home page: <http://goosecode.com/projects/watson>
[kolobyte] | 2015-
[goosecode] labs | 2012-2013
```

## .watsonrc
watson supports an RC file that allows for reusing common settings without repeating command line arguments every time.  

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
Special thanks to [@eugenekolo](http://twitter.com/eugenekolo) for his super Perl help!  
Special thanks to [@crowell](http://github.com/crowell) for helping test out watson-ruby!
