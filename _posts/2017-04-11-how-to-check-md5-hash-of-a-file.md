---
layout: mypost
title:  "How to check MD5 hash of a file"
date:   2017-04-11 09:35:00 +0100
category: security
tags: windows md5 checksum security mac linux openssl
---

When you download software from Internet, a lot of websites show the MD5 hash of the binary executable. This is for the users to make sure that the binary they have downloaded has not been tampered with and someone has not injected something malicious and then replaced the original with the infected one.

MD5 **must** not be used for hashing sensitive things like passwords etc because it has been cracked. However it's still widely used as [checksum](https://en.wikipedia.org/wiki/Checksum) for quick verification checks especially for binary files. Even for these kind of checksums it's slowly being replaced by other hashing functions like SHA-2. But while it's still being used I will show you how to check MD5 hash of a file.

> Let's say we have a file called `file.txt` that contains only 6 characters hello (5) and one newline character. It can be created using:
```bash
echo 'hello' > file.txt
```
{: .prompt-info }

## Linux
On a Linux machine you can use `md5sum`.

```bash
md5sum file.txt
```

Output:

```
b1946ac92492d2347c6235b4d2611184    file.txt
```

Also if you have the file you are verifying and you also have the DIGEST file which is basically a text file containing names of files and their respective hashes. The output above from command can be saved in a digest file i.e. `md5sum file.txt > file.DIGEST`. So if you received the digest file as well then you can easily verify files against their hases using `md5sum` as below:

```bash
# c is for check
md5sum -c file.DIGEST
```

Output:

```
file.txt: OK
```
## MacOS
On a Mac you would use the following command to compute the MD5 hash for the file.

```bash
md5 file.txt
```

Output:

```
MD5 (file.txt) = b1946ac92492d2347c6235b4d2611184
```

If you want to use the command in a script where you need to read the output back then you can use the `-q` flag which is for quiet. With this flag it only shows the md5 hash without any other information.

```bash
md5 -q file.txt
```

Ouput

```
b1946ac92492d2347c6235b4d2611184
```

## OpenSSL
Regardless of which operating system you are using, if you have openssl installed then you can use it to compute MD5 hashes.

```bash
openssl md5 file.txt
```

Output:

```
MD5 (file.txt) = b1946ac92492d2347c6235b4d2611184
```

## Windows
On Windows desktop WinMD5Free can be used to compute MD5 checksums of files. It can be downloaded from the [WinMD5.com](http://winmd5.com/). Once downloaded, extract the zip file and run WinMD5Free.exe.
Browse and select the file. WinMD5Free will compute the MD5 hash and display it.

You can use WinMD5 to make sure that the hash you received from the website and the one that is computed from the file are the same. For verification just paste the original in the lower text box and click on verify.
