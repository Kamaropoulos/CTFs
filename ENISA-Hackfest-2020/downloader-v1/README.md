# ENISA Hackfest 2020: downloader-v1

![date](https://img.shields.io/badge/date-16.11.2020-brightgreen.svg)  
![solved in time of CTF](https://img.shields.io/badge/solved-in%20time%20of%20CTF-brightgreen.svg)  
![web category](https://img.shields.io/badge/category-web-lightgrey.svg)
![easy dificulty](https://img.shields.io/badge/difficulty-easy-green.svg)
![score](https://img.shields.io/badge/score-50-blue.svg)
![solves](https://img.shields.io/badge/solves-123-brightgreen.svg)

## Description
Don't you find it frustrating when you have uploaded some files on a website but you're are not sure if the download button works? Me neither. But some people did. Is there even demand for such a service?

## Summary
Improper user input sanitization allows as to perform at LFI attack and obtain the flag.

## Flag
```
DCTF{6789af26f90396678909a99bf46ba3a78b2f1b349fbc4385e6c50556c1d0c9ff}
```

## Detailed solution

First visiting the provided URL, we are greeted with the following form:

![1](images/1.png)

Entering the URL of an image has the following result:

![2](images/2.png)

Here we can see that it performs the following operations, showing us the results:

1. It `cd`'s into a new directory, the path of which, upon multiple trials, looks to be time-based and unique every time,
2. It runs `wget` against the provided URL,
3. Removes all files matching any of the `php,pht,phtml,php4,php5,php6,php7` extensions from the directory.

First thing we can try is whether the input gets sanitized before passed to wget. Here we'll be trying to pass some extra parameters to `wget`.

![3](images/3.png)

Surely enough, we can control `wget`'s parameters. That allows us to perform an LFI attack using the `--post-file` argument, when using a URL where we can see the requests. In this case we are going to use requestbin.

![4](images/4.png)

![5](images/5.png)

Displaying the source of the web page, reveals the existance of a `flag.php` file.

![6](images/6.png)

But trying to open it on the browser proves pointless as it only displays a `GET ME!` message.

![7](images/7.png)

On the other hand, trying to post the file to our requestbin server, should give us the flag.

![8](images/8.png)

but there seems to be a check in place for the `flag.php` string.

Turns out we can bypass this by having out request not end with `flag.txt`.

![9](images/9.png)

![10](images/10.png)
