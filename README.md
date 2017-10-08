# Summary
The purpose of cvs2hg is to convert a CVS repository to a Mercurial repository. 
All mechanism of conversion is based on [reposurgeon](http://www.catb.org/~esr/reposurgeon/) tool.
The conversion uses the version 3.1.2 of mercurial provided on jessie.


# Launch conversion
    docker run -it lroche/cvs2hg modulecvs cvs_remote_url

# Examples
    docker run -it lroche/cvs2hg a2ps cvs.savannah.gnu.org

# How to retrieve hg conversion ?

At the end of process, the script launchs a bash session to allow to check the result, here from the example you can get the a2ps-hg directory by using `docker cp` command :

    docker cp <containerId>:/work/a2ps/a2ps-hg .

You can also use a bind mount volume during your run:

    docker run -it -v ~/hgconversion/a2ps:/work/a2ps lroche/cvs2hg a2ps cvs.savannah.gnu.org

So here the mercurial repository will be in ~/hgconversion/a2ps/a2ps-hg directory on host machine.

# Troubleshooting

- Reposurgeon uses rsync to connect on remote server so sometimes you could get some issues with it:  there is a workaround, only if you have access on cvs server files (,v files), you can copy them on host machine in a directory
named ${project-name}-mirror.
If your project is a2ps and your workdir is ~/hgconversion/a2ps:

    * create a directory named :
~/hgconversion/a2ps/a2ps-mirror
    * place all your files ,v in a directory named ~/hgconversion/a2ps/a2ps-mirror/a2ps
    * create a empty directory named CVSROOT here:
    ~/hgconversion/a2ps/a2ps-mirror/CVSROOT

You should have in ~/hgconversion/a2ps/ this structure now:
```
├── a2ps-mirror
│   ├── CVSROOT
│   └── a2ps
└── a2ps.map
```

- Encoding issues "<code>utf8 codec can't decode byte 0xe9 in position xx</code>" : the process of conversion expects to have commit logs in utf-8 format only so if you have another encoding format you need to modify all logs of ,v files with utf-8 format.    



# Author map

- The author map allows to specify a full name and email address for each local user ID in the repo you are converting. The expected name file is ${moduleCVSName}.map

So to set a author map file, create a map file in your host machine and use
a bind mount volume to get it in container:

    docker run -it -v ~/hgconversion/a2ps:/work/a2ps lroche/cvs2hg a2ps cvs.savannah.gnu.org
