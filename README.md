#Summary
The purpose of cvs2hg is to convert a CVS repository to a Mercurial repository. 
All mechanism of conversion is based on [reposurgeon](http://www.catb.org/~esr/reposurgeon/) tool.
The conversion uses the version 3.1.2 of mercurial provided on jessie.


#Launch conversion
    docker run -it lroche/cvs2hg modulecvs cvs_remote_url

#Examples
    docker run -it lroche/cvs2hg a2ps cvs.savannah.gnu.org

At the end of process, the script launchs a bash session to allow to check the result, here from the example you can check the a2ps-hg directory.

#How to retrieve hg conversion ?
Here, you can use docker cp, for example
    docker cp <containerId>:/work/a2ps/a2ps-hg .
