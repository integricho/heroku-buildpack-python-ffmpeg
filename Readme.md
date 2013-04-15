Heroku buildpack: Python-ffmpeg
========================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for Python apps. The only difference from the clean Python buildpack is that this one includes ffmpeg. A pre-built version is simply cloned from [dzello's repo](https://github.com/dzello/ffmpeg-heroku), which was built on Heroku.

It uses [virtualenv](http://www.virtualenv.org/) and [pip](http://www.pip-installer.org/).

Usage
-----

Example usage:

    $ ls
    gunicorn.py.ini  Procfile  requirements.txt  wsgi.py
    $ git init
    Initialized empty Git repository in /path/to/app/.git/
    $ heroku create --stack cedar --buildpack git://github.com/integricho/heroku-buildpack-python-ffmpeg.git
    Creating random-app-name-1234... done, stack is cedar
    BUILDPACK_URL=git://github.com/integricho/heroku-buildpack-python-ffmpeg.git
    http://random-app-name-1234.herokuapp.com/ | git@heroku.com:random-app-name-1234.git
    Git remote heroku added
    $ git add .
    $ git commit -m "Initial commit."
    [master (root-commit) 16d444a] Initial commit.
     4 files changed, 29 insertions(+)
     create mode 100644 Procfile
     create mode 100644 gunicorn.py.ini
     create mode 100644 requirements.txt
     create mode 100644 wsgi.py
    $ git push heroku master
    Counting objects: 6, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (5/5), done.
    Writing objects: 100% (6/6), 786 bytes, done.
    Total 6 (delta 0), reused 0 (delta 0)
    -----> Fetching custom git buildpack... done
    -----> Python app detected
    -----> Cloning pre-built ffmpeg repository...
    -----> Preparing Python interpreter (2.7.2)
    -----> Creating Virtualenv (1.8.4)
           Also creating executable in .heroku/venv/bin/python
           Installing distribute...done.
           Installing pip...done.
           Running virtualenv with interpreter /usr/local/bin/python2.7
    -----> Installing dependencies using pip (1.1)
           Downloading/unpacking gevent==0.13.8 (from -r requirements.txt (line 2))
             Storing download in cache at /app/tmp/repo.git/.cache/pip_downloads/http%3A%2F%2Fpypi.python.org%2Fpackages%2Fsource%2Fg%2Fgevent%2Fgevent-0.13.8.tar.gz
             Running setup.py egg_info for package gevent

           Downloading/unpacking gunicorn==0.14.3 (from -r requirements.txt (line 3))
             Storing download in cache at /app/tmp/repo.git/.cache/pip_downloads/http%3A%2F%2Fpypi.python.org%2Fpackages%2Fsource%2Fg%2Fgunicorn%2Fgunicorn-0.14.3.tar.gz
             Running setup.py egg_info for package gunicorn

           Downloading/unpacking greenlet (from gevent==0.13.8->-r requirements.txt (line 2))
             Storing download in cache at /app/tmp/repo.git/.cache/pip_downloads/http%3A%2F%2Fpypi.python.org%2Fpackages%2Fsource%2Fg%2Fgreenlet%2Fgreenlet-0.4.0.zip
             Running setup.py egg_info for package greenlet

           Installing collected packages: gevent, gunicorn, greenlet
             Running setup.py install for gevent
               building 'gevent.core' extension
               gcc -pthread -fno-strict-aliasing -g -O2 -DNDEBUG -g -fwrapv -O3 -Wall -Wstrict-prototypes -fPIC -I/usr/local/include/python2.7 -c gevent/core.c -o build/temp.linux-x86_64-2.7/gevent/core.o
               gcc -pthread -shared build/temp.linux-x86_64-2.7/gevent/core.o -levent -o build/lib.linux-x86_64-2.7/gevent/core.so
               Linking /tmp/build_3fhn8k1szm2sp/.heroku/venv/build/gevent/build/lib.linux-x86_64-2.7/gevent/core.so to /tmp/build_3fhn8k1szm2sp/.heroku/venv/build/gevent/gevent/core.so

             Running setup.py install for gunicorn

               Installing gunicorn_paster script to /tmp/build_3fhn8k1szm2sp/.heroku/venv/bin
               Installing gunicorn script to /tmp/build_3fhn8k1szm2sp/.heroku/venv/bin
               Installing gunicorn_django script to /tmp/build_3fhn8k1szm2sp/.heroku/venv/bin
             Running setup.py install for greenlet
               building 'greenlet' extension
               gcc -pthread -fno-strict-aliasing -g -O2 -DNDEBUG -g -fwrapv -O3 -Wall -Wstrict-prototypes -fPIC -I/usr/local/include/python2.7 -c greenlet.c -o build/temp.linux-x86_64-2.7/greenlet.o
               greenlet.c: In function 'g_switch':
               greenlet.c:543: warning: 'err' may be used uninitialized in this function
               gcc -pthread -shared build/temp.linux-x86_64-2.7/greenlet.o -o build/lib.linux-x86_64-2.7/greenlet.so
               Linking /tmp/build_3fhn8k1szm2sp/.heroku/venv/build/greenlet/build/lib.linux-x86_64-2.7/greenlet.so to /tmp/build_3fhn8k1szm2sp/.heroku/venv/build/greenlet/greenlet.so

           Successfully installed gevent gunicorn greenlet
           Cleaning up...
    -----> Discovering process types
           Procfile declares types -> web
    -----> Compiled slug size: 79.3MB
    -----> Launching... done, v5
           http://random-app-name-1234.herokuapp.com deployed to Heroku

    To git@heroku.com:random-app-name-1234.git
     * [new branch]      master -> master
    $ heroku run bash
    Running `bash` attached to terminal... up, run.1627
    ~ $ ffmpeg
    ffmpeg version git-2012-11-15-62006b5 Copyright (c) 2000-2012 the FFmpeg developers
      built on Nov 15 2012 09:35:53 with gcc 4.4.3 (Ubuntu 4.4.3-4ubuntu5)
      configuration: --enable-shared --disable-asm --prefix=/app/vendor/ffmpeg
      libavutil      52.  6.100 / 52.  6.100
      libavcodec     54. 71.100 / 54. 71.100
      libavformat    54. 36.100 / 54. 36.100
      libavdevice    54.  3.100 / 54.  3.100
      libavfilter     3. 23.100 /  3. 23.100
      libswscale      2.  1.102 /  2.  1.102
      libswresample   0. 16.100 /  0. 16.100
    Hyper fast Audio and Video encoder
    usage: ffmpeg [options] [[infile options] -i infile]... {[outfile options] outfile}...

    Use -h to get full help or, even better, run 'man ffmpeg'
    ~ $ exit

You can also add it to upcoming builds of an existing application:

    $ heroku config:add BUILDPACK_URL=git://github.com/integricho/heroku-buildpack-python-ffmpeg.git

You should then append ffmpeg to `PATH` and `LD_LIBRARY_PATH`.
<code>
$ heroku config:set PATH=/app/.heroku/python/bin:/app/.heroku/python/bin:/usr/local/bin:/usr/bin:/bin<strong>:/app/vendor/ffmpeg/bin</strong>
</code>
<code>
$ heroku config:set LD_LIBRARY_PATH=/app/.heroku/vendor/lib<strong>:/app/vendor/ffmpeg/lib</strong>
</code>

The buildpack will detect your app as Python if it has the file `requirements.txt` in the root. It will detect your app as Python/Django if there is an additional `settings.py` in a project subdirectory.

It will use virtualenv and pip to install your dependencies, vendoring a copy of the Python runtime into your slug.  The `bin/`, `include/` and `lib/` directories will be cached between builds to allow for faster pip install time.

Hacking
-------

To use this buildpack, fork it on Github.  Push up changes to your fork, then create a test app with `--buildpack <your-github-url>` and push to it.

To change the vendored virtualenv, unpack the desired version to the `src/` folder, and update the virtualenv() function in `bin/compile` to prepend the virtualenv module directory to the path. The virtualenv release vendors its own versions of pip and setuptools.
