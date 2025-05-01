# Week 11.1

## Caesar Cipher Code Names
Using a key of three we must create a Caesar cipher to encrypt our codename. Mine is the below:
Edqdqd Pxiilqv --> Banana Muffins

## Decoding

48 61 20 48 61 20 48 61 21 20 59 6f 75 20 63 61 6e 20 6e 65 76 65 72 20 63 61 74 63 68 20 74 68 65 20 41 6c 70 68 61 62 65 74 20 42 61 6e 64 69 74 21 20 53 65 65 20 69 66 20 79 6f 75 20 63 61 6e 20 66 6f 6c 6c 6f 77 20 6d 65 20 68 65 72 65 3a 0a 30 31 31 30 31 30 30 30 20 30 31 31 31 30 31 30 30 20 30 31 31 31 30 31 30 30 20 30 31 31 31 30 30 30 30 20 30 30 31 31 31 30 31 30 20 30 30 31 30 31 31 31 31 20 30 30 31 30 31 31 31 31 20 30 31 31 31 30 31 31 31 20 30 31 31 31 30 31 31 31 20 30 31 31 31 30 31 31 31 20 30 30 31 30 31 31 31 30 20 30 31 31 31 30 30 30 30 20 30 31 31 30 30 30 30 31 20 30 31 31 30 30 31 31 31 20 30 31 31 30 30 31 30 31 20 30 31 31 30 31 31 31 31 20 30 31 31 31 30 30 31 30 20 30 31 31 30 30 30 30 31 20 30 31 31 30 31 31 30 31 20 30 31 31 30 30 30 30 31 20 30 30 31 30 31 31 31 30 20 30 31 31 30 30 30 31 31 20 30 31 31 30 31 31 31 31 20 30 31 31 30 31 31 30 31 20 30 30 31 30 31 31 31 31 20 30 30 31 31 31 31 31 31 20 30 31 31 31 30 30 30 30 20 30 30 31 31 31 31 30 31 20 30 31 31 30 30 30 30 31 20 30 31 31 30 30 30 31 30 20 30 31 31 31 30 31 30 31 20 30 31 31 31 30 30 31 30 20 30 31 31 30 30 31 31 31 20 30 31 31 30 31 31 30 30 20 30 31 31 30 30 30 30 31 20 30 31 31 31 30 30 31 30 20 30 30 31 31 30 30 30 31

We must decode the above Hexadecimal code:

Ha Ha Ha! You can never catch the Alphabet Bandit! See if you can follow me here:
01101000 01110100 01110100 01110000 00111010 00101111 00101111 01110111 01110111 01110111 00101110 01110000 01100001 01100111 01100101 01101111 01110010 01100001 01101101 01100001 00101110 01100011 01101111 01101101 00101111 00111111 01110000 00111101 01100001 01100010 01110101 01110010 01100111 01101100 01100001 01110010 00110001

Next we must decode the binary from the above message:

http://www.pageorama.com/?p=aburglar1<br>
The Mayor is just the beginning of my Reign, My next target will be:  68 74 74 70 73 3a 2f 2f 77 77 77 2e 70 61 67 65 6f 72 61 6d 61 2e 63 6f 6d 2f 3f 70 3d 63 6c 75 65 2d 32

Again we find a Hexadecimal code to convert:

https://www.pageorama.com/?p=clue-2<br>
Impressive work solving my puzzles, my next target will be: 68 111 99 116 111 114 32 66 114 111 119 110 39 115 32 72 111 117 115 101

This time we are given a decimal which I needed to convert to Hexadecimal and then into text revealing the final clue:

D o c t o r   B r o w n ' s   H o u s e

## Ciphers

Caesars cipher again will be use to decrypt the below message. We were given the Key {123456} = {341256}<br>
I broke this down into chunks of 6 and then just moved the first digits to the middle which unscrambled the words.

Message:  u Yocanen vecar tcthh e phAlab Betant,di Mney xtar Tgeist  Cvialnsou Hse
You ca_n neve_r catc_h the _Alphab_et Ban_dit, M_y next_ Targe_t is C_alvins_ House

## OpenSSL

To complete this activity we will use wget to download the encrypted message. We will then use cat to find our key and IV. Using openssl we will decrypt the message:
```console
wget https://gist.githubusercontent.com/jmmeacham/d894fcde2f5ed5613fe49fee433a6bbc/raw/809ea931822ac3ed30e93d864bf251f7c106166e/key-iv to download the file
wget https://gist.githubusercontent.com/jmmeacham/d894fcde2f5ed5613fe49fee433a6bbc/raw/809ea931822ac3ed30e93d864bf251f7c106166e/key-iv
cat key-iv
openssl enc -pbkdf2 -nosalt -aes-256-cbc -in communication.txt.enc -d -base64 -K 346B3EFB4B899E8205C4B35E91F5A4605A54F89730AE65CA2C43AB464E76CA99 -iv 759D1B9BF335985F55E3E9940E751B67
```
From: Captain Strickland 
 
Great job cracking all the Alphabet's coded messages so 
far, but we need to act faster. 
 
I need you and your partner to meet me at Lou's Cafe 
tomorrow at noon. 
I have some additional information to share about the 
Alphabet Bandit. 
 
I need you to do the following things: 
 
1) Write a message called "meetingplace.txt" for your 
partner, letting them know about the secret meeting 
tomorrow.  
2) In the message, don't use your real names! 
3) Create a new key and IV with OpenSSL. 
4) Use OpenSSL with that key and IV to encrypt the message. 
5) Don't send the message until we give you the green 
light.

# Week 11.2

## Cryptography Refresher
Continuing off of the last activity we will send our partner the below encrypted message to meet at a location:

Dear kxqwhu,
We must meet a Lou's Cafe at 6pm. See you then...
From,
Edqdqd Pxiilqv

```console
nano meeting.txt
# We must hten encrypt our message for our partner: 
openssl enc -pbkdf2 -nosalt -aes-256-cbc -in meeting.txt 
-out meeting.txt.enc -base64 -K 5284A3B154D99487D9D8D8508461A478C7BEB67081A64AD9A15147906E8E8564 -iv 1907C5E255F7FC9A6B47B0E789847AED
# I send my partner my KEY, IV, and the meeting file.
# They will decrpyt it using the following:
openssl enc -pbkdf2 -nosalt -aes-256-cbc -d -in 
meetingplace_update.txt.enc -base64 -K 5284A3B154D99487D9D8D8508461A478C7BEB67081A64AD9A15147906E8E8564 -iv 1907C5E255F7FC9A6B47B0E789847AED

```

## Optinmzing with Asymmetric Public Keys
In this activity we will calculate how many keys would be needed for each team on the police force. We will also take note that we will need far fewer Asymmetric keys.

1. To calculate for the SWAT team, with 10 officers: 
Symmetric: (10 * 9)/2 = 45 
Asymmetric: 10 * 2 = 20 
Difference: 45 - 20 = 25 
2. To calculate for the Canine Unit, with 25 officers: 
Symmetric: (25 * 24)/2 = 300
Asymmetric: 25 * 2 = 50 
Difference: 300 - 50 = 250 
4. To calculate for Internal Affairs, with 45 officers: 
Symmetric: (45 * 44)/ 2 = 990 
Asymmetric: 45 * 2 = 90 
Difference: 990 - 90 = 900 
 
## GPG
```console
gpg --gen-key
gpg --list-keys
gpg --armor --output matthew_key.gpg --export example@hotmail.com
more matthew_key.gpg
# My public key that I generated for this lab.

-----BEGIN PGP SIGNATURE-----
iQGzBAABCgAdFiEEQe/4IKvsKhoc3b63BCXHdCgcySoFAmfPbYoACgkQBCXHdCgc
ySr7IQv+KYyTpWQpO/erLOwS51qWfpnRjGzi75h/kTBEsvN+RW9QJXNhGQbvKSih
C3WJFDq30o/bJcg55ou3tMocA/CsHItwdLQBTnCOWld5eb8WNPqsA6/qwhDAwF1X
WFhe/Xc8SMTsPaFOHvBVcERu6qNHRnMHZ2hSQU1068UcE+ydJ8K02l8+ffgdCbL8
6qz7B+spHalgTmvYTxWGrGo4vB0TOREHJ21ar6StGAbRMbAJf5NneuPTjIO8YY3G
TwVM+eBF+qQ93aILxzksYItjtPFWrUFeBTbFrM2KviTyqCKngkzVN4SBRoP3mae9
stQbe+W1NeiIiUvVmBpycwfGWIwITkOV24Nt+LXxUmHtvCYNZd0mrWAegJOaiiFF
xBBvEWkwkmHdaaS783MH6nsq1qpLQ5MfD3TWKkI33RN6FbR5bPzsLtQf7h8CA+Z1
hDlHY90i+Q05EDozk9Vizxsay+uAO3BNtkQh4J7iy39PtppH/84csIXuKIhA5m2x
L7mIvEwc
=D2sj
-----END PGP SIGNATURE-----
# Then I must import my partners key to complete the two way encryption and send them my message.
gpg --import partner_key.gpg
gpg --output matthew_secret_idea.txt.enc --encrypt --recipient 
partner_key.gpg secret_idea.txt
# After we exchange messages I will decrypt the message my partner sent me by using
gpg --output decrypted_message.txt --decrypt partner_secret_idea.txt.enc
```
## Digital Signatures
We need to validate the messages we recieved from our captain. <br>
First we will extract the messages we recieved and import the senders key:
```console
gpg --import strickland_publickey.gpg
gpg --verify message1.sig
gpg --verify message2.sig
gpg --verify message3.sig
# Verification is successful on the first two messages but fails on the final message indicating it is forged.

```
# Week 11.3

## Steganography
We will use steganohide to pull text embedded in an image:
```console
steghide extract -sf mydreamcar.jpg
cat list_of_targets.txt 
# Contents
List of Homes to Break into

Doctor Brown House - Done
Mayor Wilson's House - Done
Mrs Peaboday's House - Done
Captain Stricklands house - Next
```
## SSL Certificates
In this lab we used the below link to learn where to find SSL certificates and how to verify them.

https://view.genial.ly/6515deaad55b010011ae9cd8/interactive-image-hillvalley

## Cryptographic Attacks
We are given the encrpyted password cbzhptmm and need to decrypt it.<br>
We are provided a script to decrypt the password python3 encrypter.py<br>
We test the script by seeing what some other plaintext encrypts into. We determine the encryption is in a key of 12.<br>
Therefore our password is jigowatt
## Hashcat
For this activity we are given a hash (f31663d6c912b0b1ced885a6c6bbab7c) and a (secret.zip) file. 
```console
echo f31663d6c912b0b1ced885a6c6bbab7c > hashwork.txt
hashcat -m 0 -a 0 -o solved.txt hashwork.txt /usr/share/wordlist/rockyou.txt --force
cat solved.txt
f31663d6c912b0b1ced885a6c6bbab7c:ilovelorraine
```
