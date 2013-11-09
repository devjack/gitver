gitver
======

Simple class to parse version tags from a git working directory.

[![Build Status](https://travis-ci.org/sydnerdrage/gitver.png?branch=master)](https://travis-ci.org/sydnerdrage/gitver)
[![Coverage Status](https://coveralls.io/repos/sydnerdrage/gitver/badge.png?branch=master)](https://coveralls.io/r/sydnerdrage/gitver?branch=master)

Usage
-----------
Gitver defaults to the current working directory.  As such it requires no immediate configuration

~~~php
use \Gitver\Git;

$gitver = new Git(__DIR__);
echo $gitver->version();
~~~

This will output a `git describe` of the current working directory.
e.g.  v0.1.1-0-abcdefg

This is a combination of:
 - Most recent tag (matching a $prefixX.Y.Z format - see configuration below)
 - Number of commits since that tag
 - Current commit prefixed with 'g' (identifying the repository as git).



## Configuration
 - Working directory to retrieve version from (defaults to the current working directory)
 - Tag match prefix (defaults to "v")

For example if you version tags are in the format of release-X.Y.Z then you  would call
~~~php
$gitver = new Git(__DIR__, "version-");
~~~



#### CakePHP Sample
~~~php
<?php
use \Gitver\Git;

App::uses('Controller', 'Controller');

class AppController extends Controller
{
    public function beforeFilter()
    {
        parent::beforeFilter();
        $this->set("VERSION", (new Git(__DIR__))->version());
    }
}
~~~
