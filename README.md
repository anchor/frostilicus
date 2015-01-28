#Frostilicus-lite

[Namesake] (http://en.wikipedia.org/wiki/Lisa_the_Simpson)

![Frostilicus!](http://yinette.beta.anchortrove.com/Xsp6T.jpg)

Frostilicus is released under BSD License, so go nuts! (but tell me about what you're working on too)

#### Requirements:

 - Python 2.7+

covered in depth in installation

#### Intro

Frostilicus is a python based program that can either passively or actively look for
web-based malware based on signatures found common in malicious files/malicious modifications.

It will then set chmod 0000 on files that it has 'high confidence' of being malicious.


Frostilicus will run in one of two modes:

##### ACTIVE

Will recursively find files modified in the last 24 hours and then run them through a bunch of score tests.

##### PASSIVE

On supported systems will plug into the fanotify syscall and test files as they are modified. Requires butter.

#### What Frostilicus looks for

Frostilicus operates on a scoring system based on confidence of a file being compromised.

It takes several things into account when tallying this score:

 - The inclusion of `base64_decode` on a line longer than 700 Characters.

 - The inclusion of `base64_decode` and a line that exceeds 700 Characters

 - If `GIF89a` and `<?php` exist in the same file, DEAD GIVE AWAY.

 - Common variables defined in popular PHP shells.

 - Looks for a string found in the Rodecap spam Trojan.

 - Other stuff that has not been added yet!

#### INSTALL:

Frostilicus runs best in a virtualenv, however it's perfectly fine to run this on a system as is.

The prerequisites you will require on the system are:

 - python-virtualenv
 - python-pip
 - build-essential
 - libpython2.7

Some of these may already be installed.

Install all these fun things first:
`apt-get install build-essential python-virtualenv python-pip libpython2.7`


(packages might be named different on non-debian based systems)


now, go to where you cloned frostilicus and start the virtualenv.

<pre>
$ virtualenv env  #"env" can be whatever you want to call it.
$ . env/bin/activate
</pre>
Now, inside the virtualenv you can pip install required modules for frostilicus-lite.

Now once that's all done, you're ready to go.

`./frostilicus-lite.py`

#### USE:

`frostilicus-lite.py [-v,--verbose] [-f,--freeze] <DIR>`

Frostilicus will recursively search and scan files in the given directory.
Files modified in the last 24 hours will be scanned for malware.

Freeze mode will chmod 000 files that gain a score of 10+
