# Linux


[Explain shell][explainshell] — help text for each command line argument.

[explainshell]: https://explainshell.com/

***

`mkdir -p` creates parent directories if necessary

    mkdir -p path/to/directory/{file1,file2,file3}

***
    :::bash
    Ctrl+R      #reverse-i-search
    date -u     #UTC data

    info command
    command --help
    xdg-open .
    xdg-open http://codebicycle.com

    nslookup -debug rogifts.com. 8.8.8.8
    dig rogifts.com
    traceroute -w 2 rogifts.com

    grep --color=always "search string" * | less -R
    less -M     # progress indicator
    /           # search in man pages (n next occurrence, p)


Process tree

    pstree

Equivalent?

    echo $(which python)
    echo `which python`

Globing (glob patterns)

    mv *.txt textfiles/

Auto-complete filenames

    Alt + /

Shell expand

    $HOME Ctrl + Alt + E

Command substitution

    $(command)
    touch file-$(date +%y-%m-%d)

This should tell us if any of the intermediate directories are blocking the `www-data` user from opening the socket.

    sudo -u ww-data ls /var/opt/gitlab/gitlab-workhorse/socket

Batch rename files

```sh
# rename [ -v ] [ -n ] [ -f ] perlexpr [ files ]
# test run
rename -n ’s/\.htm$/\.html/’ *.htm
# verbose rename
rename -v ’s/\.htm$/\.html/’ *.htm
```
