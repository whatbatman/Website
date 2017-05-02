+++
creatordisplayname = "whatbatman"
creatoremail = "whatbatman@protonmail.com"
date = "2017-05-02T13:28:30Z"
description = "Fixing the 'Invalid character names in local volume name' error for Docker"
lastmodifierdisplayname = "whatbatman"
lastmodifieremail = "whatbatman@protonmail.com"
tags = ["docker"]
title = "'Invalid characters for a local volume name' -- A Docker struggle"

[menu]

  [menu.main]
    identifier = "docker_struggle"
    parent = "Docker"
    weight = 10

+++

I'm working on a platform to auto-deploy CTF challenges, using docker and python. Today I ran into an interesting error,

<code>
"path/path/path" includes invalid characters for a local volume name, only "[a-zA-Z0-9][a-zA-Z0-9_.-]" are allowed."
</code>

This occurred when I was trying to set up a local mount for a container, which is hilarious. So I can't have `/` in my path name? Well it turns out it's an issue with running docker on OSX and Windows.
The solution to this is to provide the full path, rather than a relative path, because Docker gets messed up with the `/Users/` path in OSX. So instead of `path/path/path`, I had to write `/Users/me/path/path/path`. That was a fun hour...
