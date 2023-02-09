<h1 align="center">Haaga-Helia - Information Security - H4 Hash</h1>
<h2 align="center">Matthieu Brühwiler - February 2023</h2>
<br>

## Table of Contens
1. [ Schneier 2015 - Summary. ](#one-way-functions)
2. [ Hashcat - Installation. ](#hashcat)
3. [ Hash- Crack. ](#crackhash)
4. [ John the Ripper - Compile. ](#john)
5. [ Zip file - Crack.](#crackjohn)
<br>

----
<a name="one-way-functions"></a>
# Schneier 2015: Applied Cryptography
## [2.3 ONE-WAY FUNCTIONS](https://learning.oreilly.com/library/view/applied-cryptography-protocols/9781119096726/10_chap02.html#chap02-sec003)
* Public-key cryptography is based on the notion of one-way function.
* A one-way function is easy to compute, but hard to reverse.
  * Hard means that a very long time is needed to reverse the function, but it is not impossible.
* Mathematically speaking, we can't prove the existence of a one-way function.
* A one-way function could be used to encrypt a message. However, if you can't decrypt the message it is useless.
* A **trapdoor one-way function** is a kind of one-way function that has a secret trapdoor.
  * It is hard to reverse the function without the trapdoor.
  * On the other hand, if you know the trapdoor, you can easily reverse the function.

## [2.4 ONE-WAY HASH FUNCTIONS](https://learning.oreilly.com/library/view/applied-cryptography-protocols/9781119096726/10_chap02.html#chap02-sec004)
* A **one-way hash function** (has several names, such as message digest) is central to modern cryptography.
* Is a function that converts a variable (*pre-image*) to a fixed-length output string (*hash value*).
* Is used to compare a real pre-image with one or multiple candidate.
  * So, you can know if it is the same pre-image or not.
* With one-way hash function, you can easily calculate the hash value of a pre-image. However, it is hard to generate the pre-image from a specific hash value.
  * A real one-way hash function makes it difficult that two pre-image has the same hash value.
* A hash function is public, you can easily know the process.
  * The security of a one-way hash function is on its one way.
  * A single bit of the pre-image changes, and the hash value is different.
  * It is impossible to find the pre-image with only having the hash value.
* One-way hash function is used to help us to ensure that a file has not been modified (so, it is the same version).
  * Usually, you can find hash value, when you download an application from a website. So, you can ensure you that the application has not been altered by someone.
* A **message authentication code** (MAC) is a one-way hash function with a secret key.
  * The hash value is based on the pre-image and the key.
  * You can't verify the hash value without the pre-image and the key.

----
<a name="hashcat"></a>
# Hashcat
## [Installation source](https://terokarvinen.com/2022/cracking-passwords-with-hashcat/)
As long as you are working on a Linux distro (or others operating systems), it is important to regularly update your components. In my case, I try to do at least one time every two weeks and also before I install a new component. To update my components, I wrote the following commands:

    $ sudo apt-get update
    $ sudo apt-get upgrade

After that, I am now ready to install a new component. In the case of the installation of Hashcat, I wrote the following command:

    $ sudo apt-get -y install hashid hashcat wget

Magic, the installation is now done!! :clap:

----
<a name="crackhash"></a>
# Crack this hash
## [Sources](https://terokarvinen.com/2022/cracking-passwords-with-hashcat/)
So, to work correctly, I think it is important to create a dedicated work environment. I created it directly in my personal home directory.

    $ mkdir crack
    $ cd crack

We can already install the rockyou file in this directory: 

    $ wget https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt

We can now create a new file and write in it the hash that we have to crack: *8eb8e307a6d649bc7fb51443a06a216f*.

    $ nano hash.txt
    # Using the nano editor, I copy-pasted the hash in the file and I saved the modification.

We are now ready to work! <br />
Let's find the hash type by using the command:

    $ hashid -m hash.txt
    
Let's now see the result:

<p align="center"> <img alt="Hashid result" src="https://github.com/MatthieuBruh/h4_Hash/blob/main/screenshots/hashid.PNG"> </p>

As we can see, we have the kind of hash that is possible for our hash. Generally, one of the three first should be the right one. Let's try with MD5, because it is the most popular. So, I entered the following command:

    $ hashcat -m 0 hash.txt rockyou.txt -o solved

And, the hash is cracked:

<p align="center"> <img alt="Hashcat result" src="https://github.com/MatthieuBruh/h4_Hash/blob/main/screenshots/hascat.PNG"> </p>

To find the hash password let's execute the command:

    $ cat solved

<p align="center"> <img alt="Cat solved result" src="https://github.com/MatthieuBruh/h4_Hash/blob/main/screenshots/catSolved.PNG"> </p>

----
<a name="john"></a>
# John the Ripper
## [Sources](https://terokarvinen.com/2023/crack-file-password-with-john/)


----
<a name="crackjohn"></a>
# Zip file
## [Crack a zip file password](https://terokarvinen.com/2023/crack-file-password-with-john/)


