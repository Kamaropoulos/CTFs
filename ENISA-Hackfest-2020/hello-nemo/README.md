# ENISA Hackfest 2020: hello-nemo

![date](https://img.shields.io/badge/date-16.11.2020-brightgreen.svg)  
![solved in time of CTF](https://img.shields.io/badge/solved-in%20time%20of%20CTF-brightgreen.svg)  
![misc category](https://img.shields.io/badge/category-misc-lightgrey.svg)
![forensics category](https://img.shields.io/badge/category-forensics-lightgrey.svg)
![easy dificulty](https://img.shields.io/badge/difficulty-easy-green.svg)
![score](https://img.shields.io/badge/score-50-blue.svg)
![solves](https://img.shields.io/badge/solves-128-brightgreen.svg)

## Description
We just managed to intercept Cpt. Nemo of the Nautilus submarine. Something's fishy over here...

Download `nemo.pcapng` and start the investigation.

## Attached files
- [nemo.pcapng](nemo.pcapng)

## Summary
A `.pcapng` file with some cleartext FTP traffic from which we can extract a zip file and a text file. Using the password from the txt file to unlock the zip file's contents gives us the flag.

## Flag
```
DCTF{3907879c7744872694209e3ea9d2697508b7a0a464afddb2660de7ed0052d7a7}
```

## Detailed solution

After opening the `nemo.pcapng` file and checking the Protocol Hierarchy Statistics:

![1](images/1.png)

our attention is driven to the FTP traffic in the file.

![2](images/2.png)

Here, we can see a user trying to connect to an FTP server. Then they upload `flag.zip`:

![3](images/3.png)

and download `password.txt`:

![4](images/4.png)

We can retreive both files from the FTP-DATA packets.

![5](images/5.png)

![6](images/6.png)

Inside `flag.zip` is a `flag.txt` file, which is password protected.

![7](images/7.png)

Using the password from the `password.txt` file, gives us the flag.

![8](images/8.png)
