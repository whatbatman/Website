+++
creatordisplayname = "whatbatman"
creatoremail = "whatbatman@protonmail.com"
date = "2017-05-02T13:01:31Z"
description = "How to get the MISP docker container up and running"
lastmodifierdisplayname = "whatbatman"
lastmodifieremail = "whatbatman@protonmail.com"
tags = ["docker", "threat_intel"]
title = "Running the MISP Docker Container"

[menu]

  [menu.main]
    identifier = "MISP"
    parent = "Docker"
    weight = 10

+++

I recently learned about [MISP](https://github.com/MISP), a malware IOC sharing platform. While it doesn't have windows or OSX support, it does have a [docker container](https://github.com/xme/misp-docker)!

The issue is, the Docker container doesn't work out of the box. The issue I ran into is you can't log into the webapp, because it thinks your credentials are incorrect.

The specific error is:

     The request has been black-holed
     Error: The requested address '/users/login' was not found on this server.

To fix this, you have to attempt to log in twice. This will populate the database with some password we don't know. Then, you use the `cake` binary to change the password, like so:

    docker exec -it misp bash
    # /var/www/MISP/app/Console/cake Password [email] [password]

The password complexity is pretty decent, despite the default password, so pick a good one otherwise you keep getting errors from `cake`.
