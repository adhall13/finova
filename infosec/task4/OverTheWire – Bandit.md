# Bandit Level 11 → Level 12

## Level Goal 
The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions
Commands you may need to solve this level: grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd
Helpful Reading Material: Rot13 on Wikipedia

## Solve
```
C:\Users\anuhy>ssh bandit11@bandit.labs.overthewire.org -p 2220
bandit11@bandit.labs.overthewire.org's password:
bandit11@bandit:~$ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

## Theory Concepts
* **ROT13:** This is a specific version of the Caesar Cypher that nudges every letter **13 spots** forward. Since the alphabet has 26 letters, shifting twice brings right back to where it started, making it a "self-deciphering" loop.
> *Note:* It’s strictly for **obfuscation** (like hiding a movie spoiler), not real security; anyone with a basic understanding of code can "break" it instantly.

* **The `tr` Utility:** Short for "translate," this command swaps one set of characters for another. By telling it to map the standard alphabet to a version starting 13 letters in, it effectively automated the rotation.
  
* **The Pipe (`|`):** This acts as a digital "conveyor belt," grabbing the text from `cat` and feeding it straight into `tr`. It allows to process data in one fluid motion instead of saving intermediate files to the disk.


# Bandit Level 12 → Level 13

## Level Goal 
The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work. Use mkdir with a hard to guess directory name. Or better, use the command “mktemp -d”. Then copy the datafile using cp, and rename it using mv (read the manpages!)
Commands you may need to solve this level: grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd, mkdir, cp, mv, file
Helpful Reading Material: Hex dump on Wikipedia

## Solve
```
bandit12@bandit:~$ cd /tmp
bandit12@bandit:/tmp$ mktemp -d
/tmp/tmp.mXShNC2Q1D
bandit12@bandit:/tmp$ cd /tmp/tmp.mXShNC2Q1D
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ cp ~/data.txt .
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ ls
data.txt
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ mv data.txt hexdump_data
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ ls
hexdump_data
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ cat hexdump_data | head
00000000: 1f8b 0808 2817 ee68 0203 6461 7461 322e  ....(..h..data2.
00000010: 6269 6e00 013c 02c3 fd42 5a68 3931 4159  bin..<...BZh91AY
00000020: 2653 59cc 46b5 2d00 0018 ffff da5f e6e3  &SY.F.-......_..
00000030: 9fcd f59d bc69 ddd7 f7ff a7e7 dbdd b59f  .....i..........
00000040: fff7 cfdd ffbf bbdf ffff ff5e b001 3b58  ...........^..;X
00000050: 2406 8000 00d0 6834 6234 d000 6869 9000  $.....h4b4..hi..
00000060: 1a7a 8003 40d0 01a1 a006 8188 340d 1a68  .z..@.......4..h
00000070: d340 d189 e906 8f41 0346 4d94 40d1 91a0  .@.....A.FM.@...
00000080: 681a 0681 a068 0680 c400 3207 a269 a189  h....h....2..i..
00000090: a326 8000 c800 c81a 1883 1000 00d0 c023  .&.............#
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ xxd -r hexdump_data compressed_data
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ ls
compressed_data  hexdump_data
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ cat compressed_data | head
(�hdata2.bin<��BZh91AY&SY�F�-���_������i�������ݵ������������^�;X$��h4b4�hi�␦␦h�@щ��AFM�@ё�h␦��h��2�i���&���␦���#C�40�h����hh�hhh�L�M���0�� 2h�
                                                                  �d��h`5A,���{�G��i0�P��d�@1/KȰ
                    �l�ת3j폻{�?�DX�N����a.�'������-hf��'Tu�9
                                                            ��x(F����C��9z��#*ڛ�M�]J��2䔮�'�0�S<f�`��Fp�2+qt��R��
&{qe �w��"�35OƎ����Z
�hȔ'I�G�S�s/ݐ�hqƒg^�����9�s�(�����I:�uM#q�I4Ǣ��\���e�1=|�Q*2��^P֥OW���iDȊP5B�@�QL�#�FW���>�(-�=d�A�6��O�@�9`�^�:wb�bvY���5����姍�$�f��B��N��H�D!_3
                                                                     ^�'   �xn�7u����,]��R���ܑN$3�K@��7<bandit12@bandit:/tmp/tmp.mXShNC2Q1D$  cat hexdump cat hexdump_data
00000000: 1f8b 0808 2817 ee68 0203 6461 7461 322e  ....(..h..data2.
00000010: 6269 6e00 013c 02c3 fd42 5a68 3931 4159  bin..<...BZh91AY
00000020: 2653 59cc 46b5 2d00 0018 ffff da5f e6e3  &SY.F.-......_..
00000030: 9fcd f59d bc69 ddd7 f7ff a7e7 dbdd b59f  .....i..........
00000040: fff7 cfdd ffbf bbdf ffff ff5e b001 3b58  ...........^..;X
00000050: 2406 8000 00d0 6834 6234 d000 6869 9000  $.....h4b4..hi..
00000060: 1a7a 8003 40d0 01a1 a006 8188 340d 1a68  .z..@.......4..h
00000070: d340 d189 e906 8f41 0346 4d94 40d1 91a0  .@.....A.FM.@...
00000080: 681a 0681 a068 0680 c400 3207 a269 a189  h....h....2..i..
00000090: a326 8000 c800 c81a 1883 1000 00d0 c023  .&.............#
000000a0: 4311 a034 30ca 6800 0680 0681 a680 6868  C..40.h.......hh
000000b0: d068 6868 c04c d400 0003 4d06 87a8 d000  .hhh.L....M.....
000000c0: 3086 8c20 3268 068d 000c 9a64 0698 8d04  0.. 2h.....d....
000000d0: 0600 6860 3541 2c85 c8e1 7bc9 479e e369  ..h`5A,...{.G..i
000000e0: 30a1 0250 82e9 64ef 9d40 312f 4bc8 b00f  0..P..d..@1/K...
000000f0: 0c8f 026c d5ca 1008 d7aa 336a ed8f bb7b  ...l......3j...{
00000100: b43f d544 1658 824e a4af 9ce5 612e 8a27  .?.D.X.N....a..'
00000110: c303 0512 cbff dccd f42d 6866 ceec 8127  .........-hf...'
00000120: 5475 ed39 100b f897 7828 46e2 fdf3 efa7  Tu.9....x(F.....
00000130: 43b0 1701 a114 397a 1d81 8d1f 1f23 2ada  C.....9z.....#*.
00000140: 9b18 ee4d d05d 4ae3 d032 e494 ae98 27b0  ...M.]J..2....'.
00000150: 30a0 533c 6696 60ad c546 70c4 322b 7174  0.S<f.`..Fp.2+qt
00000160: 8bb1 52c6 ed0a 267b 7165 208b 77fe 1294  ..R...&{qe .w...
00000170: 2280 3311 354f c68e e004 93e3 abf4 5a0a  ".3.5O........Z.
00000180: a568 c894 27c2 9015 49bb 0147 c253 8e73  .h..'...I..G.S.s
00000190: 2fdd 90e1 6871 c692 1d67 5ebc a5f9 b8a1  /...hq...g^.....
000001a0: 3913 f073 1919 b628 9ae2 c1bf 15ee 493a  9..s...(......I:
000001b0: e375 4d23 71e0 4934 c7a2 15ff 985c a0ba  .uM#q.I4.....\..
000001c0: 9e65 d613 313d 7cef 512a 32bf 835e 50d6  .e..1=|.Q*2..^P.
000001d0: a54f 57ba bceb 6944 03c8 8a50 3542 9140  .OW...iD...P5B.@
000001e0: eb51 0f4c 8a23 9401 0246 0457 d1c0 c33e  .Q.L.#...F.W...>
000001f0: c328 2de7 3d1d 64be 4190 36b0 b803 4f80  .(-.=.d.A.6...O.
00000200: 40bc 3960 ac5e 13a9 3a77 0162 d662 7659  @.9`.^..:w.b.bvY
00000210: fdfd 9535 1188 8588 e8e5 a78d 9b24 c066  ...5.........$.f
00000220: 91c6 4212 fac6 4ed8 ce48 161f cc44 215f  ..B...N..H...D!_
00000230: 330c 5ed7 2709 e578 6efd 3775 c703 8aa1  3.^.'..xn.7u....
00000240: 10b6 2c5d 16bf f352 c7ff c5dc 914e 1424  ..,]...R.....N.$
00000250: 3311 ad4b 40d0 18b2 373c 0200 00         3..K@...7<...
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ mv compressed_data compressed_data.gz
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ ls
compressed_data.gz  hexdump_data
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ gzip -d compressed_data.gz
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ ls
compressed_data  hexdump_data
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ xxd compressed_data
00000000: 425a 6839 3141 5926 5359 cc46 b52d 0000  BZh91AY&SY.F.-..
00000010: 18ff ffda 5fe6 e39f cdf5 9dbc 69dd d7f7  ...._.......i...
00000020: ffa7 e7db ddb5 9fff f7cf ddff bfbb dfff  ................
00000030: ffff 5eb0 013b 5824 0680 0000 d068 3462  ..^..;X$.....h4b
00000040: 34d0 0068 6990 001a 7a80 0340 d001 a1a0  4..hi...z..@....
00000050: 0681 8834 0d1a 68d3 40d1 89e9 068f 4103  ...4..h.@.....A.
00000060: 464d 9440 d191 a068 1a06 81a0 6806 80c4  FM.@...h....h...
00000070: 0032 07a2 69a1 89a3 2680 00c8 00c8 1a18  .2..i...&.......
00000080: 8310 0000 d0c0 2343 11a0 3430 ca68 0006  ......#C..40.h..
00000090: 8006 81a6 8068 68d0 6868 68c0 4cd4 0000  .....hh.hhh.L...
000000a0: 034d 0687 a8d0 0030 868c 2032 6806 8d00  .M.....0.. 2h...
000000b0: 0c9a 6406 988d 0406 0068 6035 412c 85c8  ..d......h`5A,..
000000c0: e17b c947 9ee3 6930 a102 5082 e964 ef9d  .{.G..i0..P..d..
000000d0: 4031 2f4b c8b0 0f0c 8f02 6cd5 ca10 08d7  @1/K......l.....
000000e0: aa33 6aed 8fbb 7bb4 3fd5 4416 5882 4ea4  .3j...{.?.D.X.N.
000000f0: af9c e561 2e8a 27c3 0305 12cb ffdc cdf4  ...a..'.........
00000100: 2d68 66ce ec81 2754 75ed 3910 0bf8 9778  -hf...'Tu.9....x
00000110: 2846 e2fd f3ef a743 b017 01a1 1439 7a1d  (F.....C.....9z.
00000120: 818d 1f1f 232a da9b 18ee 4dd0 5d4a e3d0  ....#*....M.]J..
00000130: 32e4 94ae 9827 b030 a053 3c66 9660 adc5  2....'.0.S<f.`..
00000140: 4670 c432 2b71 748b b152 c6ed 0a26 7b71  Fp.2+qt..R...&{q
00000150: 6520 8b77 fe12 9422 8033 1135 4fc6 8ee0  e .w...".3.5O...
00000160: 0493 e3ab f45a 0aa5 68c8 9427 c290 1549  .....Z..h..'...I
00000170: bb01 47c2 538e 732f dd90 e168 71c6 921d  ..G.S.s/...hq...
00000180: 675e bca5 f9b8 a139 13f0 7319 19b6 289a  g^.....9..s...(.
00000190: e2c1 bf15 ee49 3ae3 754d 2371 e049 34c7  .....I:.uM#q.I4.
000001a0: a215 ff98 5ca0 ba9e 65d6 1331 3d7c ef51  ....\...e..1=|.Q
000001b0: 2a32 bf83 5e50 d6a5 4f57 babc eb69 4403  *2..^P..OW...iD.
000001c0: c88a 5035 4291 40eb 510f 4c8a 2394 0102  ..P5B.@.Q.L.#...
000001d0: 4604 57d1 c0c3 3ec3 282d e73d 1d64 be41  F.W...>.(-.=.d.A
000001e0: 9036 b0b8 034f 8040 bc39 60ac 5e13 a93a  .6...O.@.9`.^..:
000001f0: 7701 62d6 6276 59fd fd95 3511 8885 88e8  w.b.bvY...5.....
00000200: e5a7 8d9b 24c0 6691 c642 12fa c64e d8ce  ....$.f..B...N..
00000210: 4816 1fcc 4421 5f33 0c5e d727 09e5 786e  H...D!_3.^.'..xn
00000220: fd37 75c7 038a a110 b62c 5d16 bff3 52c7  .7u......,]...R.
00000230: ffc5 dc91 4e14 2433 11ad 4b40            ....N.$3..K@
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ mv compressed_data compressed_data.bz2
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ ls
compressed_data.bz2  hexdump_data
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ bzip2 -d compressed_data.bz2
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ mv compressed_data compressed_data.gz
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$  gzip -d compressed_data.gz
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ cat compressed_data
data5.bin0000644000000000000000000002400015073413450011242 0ustar  rootrootdata6.bin0000644000000000000000000000033315073413450011246 0ustar  rootrootBZI22L�SL�d␦<��Pi~��2hɓ[#���␦��r�y?�
�P��TŴ��4H�*C�'jb�7)�z4���t��p�&5��Z�4�V#´e^�y
ڼ�+>�K-��J�՞lBI��L*�
                    6;>�d.(J"N��d9�d��(�2@@?��"�(HD$���bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ mv compressed_data compressed_data.tar
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$  tar -xf compressed_data.tar
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ ls
compressed_data.tar  data5.bin  hexdump_data
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ tar -xf data5.bin
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$  xxd data6.bin
00000000: 425a 6839 3141 5926 5359 8849 ff13 0000  BZh91AY&SY.I....
00000010: 8d7f cfdc 6a00 c0c0 7dff e120 5b23 8074  ....j...}.. [#.t
00000020: 61fe 8000 0840 0000 6682 0108 014c 0820  a....@..f....L.
00000030: 0094 0d49 3d08 3232 0003 4c80 0f53 4c9a  ...I=.22..L..SL.
00000040: 641a 3ca7 a350 6914 7ea9 9032 6800 c993  d.<..Pi.~..2h...
00000050: 09a1 a01a 068c 8d03 72dd 793f c810 180c  ........r.y?....
00000060: 0204 0d07 8d50 9691 54c5 b411 101e f798  .....P..T.......
00000070: 3448 bc2a 4385 276a 62d5 3729 b77a 34fb  4H.*C.'jb.7).z4.
00000080: 0fcc dc1d 74c3 0004 ed70 02aa 2635 c0fd  ....t....p..&5..
00000090: 5a81 34c0 5623 c2b4 655e dd79 0ada bc86  Z.4.V#..e^.y....
000000a0: 2b3e d24b 2d8e ee4a f6d5 9e6c 4249 c5d1  +>.K-..J...lBI..
000000b0: 4c2a fa0e 0c10 0f36 3b3e e864 2e28 4a02  L*.....6;>.d.(J.
000000c0: 224e a3c8 6439 8964 aa85 28b0 3240 403f  "N..d9.d..(.2@@?
000000d0: 8bb9 229c 2848 4424 ff89 80              ..".(HD$...
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ bzip2 -d data6.bin
bzip2: Can't guess original name for data6.bin -- using data6.bin.out
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ ls
compressed_data.tar  data5.bin  data6.bin.out  hexdump_data
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$  tar -xf data6.bin.out
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ ls
compressed_data.tar  data5.bin  data6.bin.out  data8.bin  hexdump_data
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ xxd data8.bin
00000000: 1f8b 0808 2817 ee68 0203 6461 7461 392e  ....(..h..data9.
00000010: 6269 6e00 0bc9 4855 2848 2c2e 2ecf 2f4a  bin...HU(H,.../J
00000020: 51c8 2c56 70f3 374d 2977 2b4e 3648 4e4a  Q.,Vp.7M)w+N6HNJ
00000030: f4cc f430 c8b0 f032 4a0d cd2e 362a 4b09  ...0...2J...6*K.
00000040: 7129 77cc e302 003e de32 4131 0000 00    q)w....>.2A1...
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ mv data8.bin data8.gz
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$  gzip -d data8.gz
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ ls
compressed_data.tar  data5.bin  data6.bin.out  data8  hexdump_data
bandit12@bandit:/tmp/tmp.mXShNC2Q1D$ cat data8
The password is FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

## Theory Concepts
Concepts: binary data manipulation and recursive decompression

1. Hexadecimal Reversal: A Hex Dump is a text representation of binary data. To work with the file; use `xxd -r`, which "reverses" the text back into its original binary format. This is necessary because binary files contain non-text characters that terminals cannot display.

2. Magic Numbers & File Identification: On Linux, you cannot trust file extensions. Instead, use the `file` command to identify a file's "Magic Numbers" —unique byte sequences at the start of a file that define its true type (e.g., Gzip, Bzip2, or Tar).

3. Decompression "Layers": The challenge uses Recursive Compression. Steps are:
* Identify: Use `file` to see the compression type.
* Rename: Use `mv` to add the correct extension (like `.gz` or `.bz2`) so decompression tools recognise it.
* Extract: Use the matching tool (`gunzip`, `bunzip2`, `tar`, etc.).
* Repeat: Must do this multiple times until the final result is a text file containing the password.

4. Secure Temp Spaces: Using `mktemp -d` creates a private, uniquely named directory in `/tmp`. This is a standard security practice to prevent working files from being overwritten or seen by other users on a shared system.


# Bandit Level 13 → Level 14

## Level Goal 
The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Look at the commands that logged you into previous bandit levels, and find out how to use the key for this level.
Commands you may need to solve this level: ssh, scp, umask, chmod, cat, nc, install
Helpful Reading Material: SSH/OpenSSH/Keys

## Solve
```

```

## Theory Concepts
Concept: Asymmetric Cryptography and the practical application of SSH Private Keys.

This level shifts focus from cracking codes to **Identity and Access Management** using SSH keys. Here is the summary:

1. Key-Based Authentication: Unlike previous levels that used passwords, this level uses asymmetric cryptography. Given a private key (an identity file). When present, this key to the server matches a stored public Key to verify identity.

2. The Identity Flag (`-i`): To log in with a specific file instead of a password, use the `-i` (Identity) flag with the `ssh` command.

4. File Permissions and Security: SSH requires private keys to be kept strictly confidential. If the file permissions are too "loose" (e.g., if other users can read your key), the SSH client will block the connection for security reasons.
> *The Fix:* Use `chmod 600 <keyfile>` to ensure only you have access to it.

4. Lateral Movement: By using the key to log in as `bandit14@localhost`, perform a lateral move within the same system. Assuming a new identity that has higher privileges, specifically the permission to read the password file located in `/etc/bandit_pass/`.


# Bandit Level 14 → Level 15

## Level Goal 
The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.
Commands you may need to solve this level: ssh, telnet, nc, openssl, s_client, nmap
Helpful Reading Material:
How the Internet works in 5 minutes (YouTube) (Not completely accurate, but good enough for beginners)
IP Addresses
IP Address on Wikipedia
Localhost on Wikipedia
Ports
Port (computer networking) on Wikipedia

## Solve
```
```

## Theory Concepts
Concpet: Network Socket Communication

1. Localhost (`127.0.0.1`): Localhost is a hostname that refers to "this computer." In networking, the loopback address allows a machine to communicate with itself. This is used here because the password service is not exposed to the public internet; it only listens for connections coming from within the Bandit server.

2. Ports and Services: Think of an IP address as a building and a port as a specific door.
* Port 30000: The designated "door" where a background process is waiting for input.
* Listening: The service is in a "listen" state, meaning it is idle until a client initiates a connection.

3. Netcat (`nc`): While commands like `ssh` are for secure logins, `nc` is used to send raw data across a network. It allows:
* Open a raw TCP connection to a specific port.
* Pipe text directly into a network service.

4. The Network Handshake -> pattern:

i. Connect: use `nc` to "call" port 30000 on `localhost`.
ii. Authenticate: provide the `bandit14` password as your "token."
iii. Receive: The service validates the token and returns the `bandit15` password.


# Bandit Level 15 → Level 16

## Level Goal 
The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL/TLS encryption.

Helpful note: Getting “DONE”, “RENEGOTIATING” or “KEYUPDATE”? Read the “CONNECTED COMMANDS” section in the manpage.

Commands you may need to solve this level: ssh, telnet, nc, ncat, socat, openssl, s_client, nmap, netstat, ss

Helpful Reading Material:
Secure Socket Layer/Transport Layer Security on Wikipedia
OpenSSL Cookbook - Testing with OpenSSL


## Solve
```
```

## Theory Concepts
Concept: Network Encryption

1. SSL/TLS (Encryption in Transit): While the previous level sent data in "cleartext," this level uses SSL/TLS. This protocol ensures that even if someone intercepted the network traffic between you and the service, they would only see scrambled gibberish. 

2. OpenSSL `s_client`: Standard tools like `nc` (Netcat) cannot "speak" the complex language of SSL/TLS. You must use `openssl s_client`, which acts as a specialized negotiator.

3. Ports & Service Interaction
* Port 30001: Unlike the previous level's port, this one is configured to refuse any connection that isn't encrypted.
* The Workflow: Once the `openssl` connection is successful, the terminal will wait for your input. You provide the `bandit15` password, and the server replies with the `bandit16` password.


# Bandit Level 16 → Level 17

## Level Goal 
The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL/TLS and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

Helpful note: Getting “DONE”, “RENEGOTIATING” or “KEYUPDATE”? Read the “CONNECTED COMMANDS” section in the manpage.

Commands you may need to solve this level: ssh, telnet, nc, ncat, socat, openssl, s_client, nmap, netstat, ss

Helpful Reading Material: Port scanner on Wikipedia

## Solve
```
```

## Theory Concepts
Concepts: Network Reconnaissance with Identity Extraction

1. Port Scanning (Reconnaissance): Unlike previous levels where the port was provided, a range (31000–32000) is provided. Using `nmap` to scan the server and identify which ports are "listening." This is the first step in any security audit; discovering the attack surface.

2. Service Discovery: An open port doesn't mean it’s the right port. Some ports might be running different services. Need to find the one that:
* Is open.
* Uses SSL/TLS (encrypted).

3. RSA Key Extraction: The "prize" for this level isn't a text password; it is an **RSA Private Key**. This is a multi-line cryptographic block. You must capture this entire block and save it to a file. This represents a shift from "something you know" (password) to "something you have" (a private key file).

4. Permissions & Lateral Movement: Once you have the key, apply level 13 concepts:
* Security: Use `chmod 600` on the key file, or SSH will reject it for being too "exposed."
* Access: Use `ssh -i [keyfile] bandit17@localhost` to log in as the next user.


# Bandit Level 17 → Level 18

## Level Goal 
There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new

NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19

Commands you may need to solve this level: cat, grep, ls, diff

## Solve
```
```

## Theory Concepts

# Bandit Level 18 → Level 19

## Level Goal 
The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.

Commands you may need to solve this level: ssh, ls, cat

## Solve
```
```

## Theory Concepts

# Bandit Level 19 → Level 20

## Level Goal 
To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

Helpful Reading Material: setuid on Wikipedia

## Solve
```
```

## Theory Concepts

# Bandit Level 20 → Level 21
There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

NOTE: Try connecting to your own network daemon to see if it works as you think

Commands you may need to solve this level: ssh, nc, cat, bash, screen, tmux, Unix ‘job control’ (bg, fg, jobs, &, CTRL-Z, …)

## Level Goal 


## Solve
```
```

## Theory Concepts

# Bandit Level 21 → Level 22

## Level Goal 
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

Commands you may need to solve this level: cron, crontab, crontab(5) (use “man 5 crontab” to access this)

## Solve
```
```

## Theory Concepts

# Bandit Level 22 → Level 23

## Level Goal 
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

Commands you may need to solve this level: cron, crontab, crontab(5) (use “man 5 crontab” to access this)

## Solve
```
```

## Theory Concepts


