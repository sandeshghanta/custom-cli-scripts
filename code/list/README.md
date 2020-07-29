# list
A cli tool which can be used to select (files and directories) and either list them or delete them.

1. This command uses the `find` command internally to get list of files/directories which satisfy users requirement.
2. While listing the selected files/directories we use `ls -lAhdG` to provide colourful and long information of the items
3. While removing the selected files/directories we use `trash` instead of `rm`, `trash` moves the files to Trash folder instead of permanently deleting them like `rm`. Although `trash` is slower than `rm` we use it so that user can recover information in case an unintended recursive delete was performed.  

**Note** This tool has been tested for MacOS, it requires `getopts` (should be installed by default) and the `trash` cli installed. Install the `trash` cli from [link](https://github.com/sindresorhus/trash)

#### Usage
```
list [ -a=action ] [ -t=type ] [-r] [ -p=path ] [ -n=regex ]
```

#### Documentation:
```
-a	:	Represents the kind of action that has to take place, supported values are
              'list':	lists the selected files or directories [Default],
              'del':	deletes the selected files or directories.

-t 	:	Represents the type of content to display, supported values are
              'all':	 both files and dirs will be selected [Default],
              'files': only files will be selected
              'dirs':	 only directories will be selected

-p	:	Represents the path where the list command is to be executed, default value is . or pwd

-r	:	If -r is passed then recursive dfs search would be enabled, by default -r is unset

-n	:	Selects only those items whose name satisfies the regex passed to this option. If no regex is passed action will be applied on all items.
           Supports '[', ']', '*' and '?' pattern matching characters, these characters may be matched explicitly by escaping them with backslash '\'
```


#### Sample commands

- Command to list all files and dirs at current path
  - `list`
  - `list -a=list -t=all`


- Command to list all files at current path
  - `list -t=files`
  - `list -t=files -a=list`


- Command to recursively list everything from current path
  - `list -r`
  - `list -r -a=list -t=all`


- Command to list all files and directories recursively from current path which have tmp in their name
  - `list -r -n="*tmp*"`


- Command to recursively delete all files from current path which have .txt extension
  - `list -r -a=del -t=files -n="*.txt"`


- Command to recursively delete all files and dirs from current path
  - `list -r -a=del`
