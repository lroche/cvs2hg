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

# Author map

- The author map allows to specify a full name and email address for each local user ID in the repo you are converting. The expected name file is ${moduleCVSName}.map

So to set a author map file, create a map file in your host machine and use
a bind mount volume to get it in container:

    docker run -it -v ~/hgconversion/a2ps:/work/a2ps lroche/cvs2hg a2ps cvs.savannah.gnu.org
