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
bandit13@bandit:~$ ls
sshkey.private
bandit13@bandit:~$ exit
logout
Connection to bandit.labs.overthewire.org closed.
scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .         
bandit13@bandit.labs.overthewire.org's password: 
sshkey.private
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
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
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
bandit14@bandit:~$ nc localhost 30000
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
Correct!
BfMYroe26WYalil77FoDi9qh59eK5xNr
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
bandit15@bandit:~$ openssl s_client -connect localhost:30001
...
BfMYroe26WYalil77FoDi9qh59eK5xNr
Correct!
cluFn7wTiGryunymYOu4RcffSxQluehd
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
bandit16@bandit:~$ nmap -sV localhost -p 31000-32000
Starting Nmap 7.40 ( https://nmap.org ) at 2021-06-12 16:17 CEST
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00026s latency).
Not shown: 996 closed ports
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
31691/tcp open  echo
31790/tcp open  ssl/unknown
31960/tcp open  echo
bandit15@bandit:~$ openssl s_client -connect localhost:31790
...
cluFn7wTiGryunymYOu4RcffSxQluehd
Correct!
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----
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
bandit17@bandit:~$ diff passwords.old passwords.new 
42c42
< w0Yfolrc5bwjS4qw5mq1nnQi6mF03bii
---
> kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
```

## Theory Concepts
Concept: File Forensics and identifying the "delta" (change) between two sets of data.

1. The `diff` Utility: The `diff` command is the standard tool for line-by-line comparison. It ignores everything that matches and only highlights the discrepancies.
* **`<` Symbol:** Shows content only found in the *first* file.
* **`>` Symbol:** Shows content only found in the *second* file.

2. File Integrity Monitoring (FIM): This level simulates a real-world security practice. System admins use tools like `diff` to ensure that critical files (like password lists or system configurations) haven't been altered by unauthorized users. If a comparison shows a change that wasn't expected, it's a red flag for a potential breach.

3. Side-by-Side Comparison (`diff -y`): Instead of showing a list of changes, the `-y` flag splits your terminal into two columns.
* **Identical lines** appear side-by-side.
* **Modified lines** are marked with a `|`.
* **Unique lines** (the ones you are looking for) are marked with `<` or `>`.

4. The Unified Format (`diff -u`): While `-y` is great for humans, the `-u` (Unified) flag is the industry standard for **patches**. It shows the changes in a compact format with "context lines" around the difference.

* **`-` lines:** Content removed from the original.
* **`+` lines:** Content added to the new version.

> note:
> `-y` side-by-side = visually scanning two files manually
> `-u` unified = creating "patch" files for software updates
> `-w` ignore whitespace = finding changes when the only difference is tabs or spaces


# Bandit Level 18 → Level 19

## Level Goal 
The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.

Commands you may need to solve this level: ssh, ls, cat

## Solve
```
ssh bandit18@bandit.labs.overthewire.org -p 2220 ls         
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit18@bandit.labs.overthewire.org's password: 
readme

ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme 
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit18@bandit.labs.overthewire.org's password: 
IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x
```

## Theory Concepts
Concept: Bypassing Environment Restrictions**. It teaches ya forced logout can often be avoided by changing how you initiate the connection.

1. The Forced Logout Trap: In Linux, certain files like `.bashrc` or `.profile` execute automatically the moment you log in. If an admin places an `exit` command in these files, effectively locking them out of an interactive session, the system kicks the user out before a command can be typed.

2. Remote Command Execution: SSH allows to bypass the standard login process by passing a command directly. Instead of asking for a shell, ask for a specific result.
* **The Logic:** You tell SSH, "Don't give me a terminal; just run `cat readme` and show me what happens."
* **The Outcome:** The server executes that single command and sends the text back to your screen, often finishing the task before the restrictive "logout" script can trigger.

3. Interactive vs. Non-Interactive
* **Interactive:** Want to "stay" on the server and work (blocked in this level).
* **Non-Interactive:** Want the server to do one specific thing and report back (the solution for this level).


# Bandit Level 19 → Level 20

## Level Goal 
To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

Helpful Reading Material: setuid on Wikipedia

## Solve
```
bandit19@bandit:~$ ls -la
total 28
drwxr-xr-x  2 root     root     4096 May  7  2020 .
drwxr-xr-x 41 root     root     4096 May  7  2020 ..
-rwsr-x---  1 bandit20 bandit19 7296 May  7  2020 bandit20-do
-rw-r--r--  1 root     root      220 May 15  2017 .bash_logout
-rw-r--r--  1 root     root     3526 May 15  2017 .bashrc
-rw-r--r--  1 root     root      675 May 15  2017 .profile
bandit19@bandit:~$ ./bandit20-do 
Run a command as another user.
  Example: ./bandit20-do id
bandit19@bandit:~$ ./bandit20-do ls /etc/bandit_pass
bandit0   bandit12  bandit16  bandit2   bandit23  bandit27  bandit30  bandit4  bandit8
bandit1   bandit13  bandit17  bandit20  bandit24  bandit28  bandit31  bandit5  bandit9
bandit10  bandit14  bandit18  bandit21  bandit25  bandit29  bandit32  bandit6
bandit11  bandit15  bandit19  bandit22  bandit26  bandit3   bandit33  bandit7
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
```

## Theory Concepts
Concept: Privilege Escalation through a special Linux permission called the **SetUID bit**.

1. The SetUID Bit (Set User ID): In Linux, programs usually run with the permissions of the person who started them. However, if a file has the **SetUID bit** enabled, it runs with the permissions of the **file owner**.

* **The "s" Bit:** Identify these files by looking for an `s` in the permission string (e.g., `-rwsr-xr-x`).
* **The Power:** This allows a low-privileged user to perform a task that usually requires higher permissions.

2. Privilege Escalation: This is a fundamental security concept where an attacker (or researcher) finds a way to "step up" their authority. In this case:

* You are **bandit19**.
* The password file for the next level is only readable by **bandit20**.
* There is a "wrapper" tool owned by **bandit20** with the SetUID bit set.
* By running that tool; effectively "borrow" bandit20's identity to access the file.

3. The "Wrapper" Logic: The binary provided acts as a middleman. It is programmed to execute whatever command you give it, but it does so using the authority of its owner.

* **The Command:** Use the wrapper to run `cat /etc/bandit_pass/bandit20`.
* **The Result:** Because the wrapper "is" bandit20 in the eyes of the system, it is allowed to read the file and print the password to the screen.


# Bandit Level 20 → Level 21

## Level Goal 
There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

NOTE: Try connecting to your own network daemon to see if it works as you think

Commands you may need to solve this level: ssh, nc, cat, bash, screen, tmux, Unix ‘job control’ (bg, fg, jobs, &, CTRL-Z, …)

## Solve
```
bandit20@bandit:~$ echo -n 'GbKksEFF4yrVs6il55v6gwY5aVje5f0j' | nc -l -p 1234 &
[1] 24661
bandit20@bandit:~$ ./suconnect 1234
Read: GbKksEFF4yrVs6il55v6gwY5aVje5f0j
Password matches, sending next password
gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr
[1]+  Done               
```

## Theory Concepts
Concept: Inter-Process Communication (IPC) - through local network sockets, requiring a coordinated "handshake" between two separate programs.

1. Local Network Sockets: Sockets are endpoints for communication between processes. Even on a single machine, programs can "talk" to each other by treating the internal network (localhost) as a bridge. This interaction requires one process to act as a **Server** and the other as a **Client**.

2. The Listener-Connector Model: The challenge involves a Request-Response cycle.
* **The Listener:** A utility (like `nc`) is configured to sit in a "Listen" state on a specific port, holding the current level's password as a payload.
* **The Connector:** A SetUID binary is executed to find and connect to that specific port.
* **The Exchange:** Upon connection, the binary reads the password from the listener. If the data is correct, the binary transmits the next level's password back through the same connection.

3. Asynchronous Execution (Backgrounding): Since a terminal typically only handles one foreground task at a time, **Backgrounding** is used to manage multiple processes. By appending the `&` symbol to a command, the shell is instructed to run the task in the background. This allows the listener to remain active and waiting while the connector binary is launched in the same session.

4. Privilege Verification: The connector binary uses its **SetUID** status to access restricted data. It acts as the "judge," verifying that the string provided by the listener matches the authorized password for the current level before releasing the new credentials.


# Bandit Level 21 → Level 22

## Level Goal 
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

Commands you may need to solve this level: cron, crontab, crontab(5) (use “man 5 crontab” to access this)

## Solve
```
bandit21@bandit:~$ ls -la /etc/cron.d
total 36
drwxr-xr-x  2 root root 4096 Jul 11  2020 .
drwxr-xr-x 87 root root 4096 May 14  2020 ..
-rw-r--r--  1 root root   62 May 14  2020 cronjob_bandit15_root
-rw-r--r--  1 root root   62 Jul 11  2020 cronjob_bandit17_root
-rw-r--r--  1 root root  120 May  7  2020 cronjob_bandit22
-rw-r--r--  1 root root  122 May  7  2020 cronjob_bandit23
-rw-r--r--  1 root root  120 May 14  2020 cronjob_bandit24
-rw-r--r--  1 root root   62 May 14  2020 cronjob_bandit25_root
-rw-r--r--  1 root root  102 Oct  7  2017 .placeholder
bandit21@bandit:~$ cat /etc/cron.d/cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
bandit21@bandit:~$ cat /usr/bin/cronjob_bandit22.sh
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
bandit21@bandit:~$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI
```

## Theory Concepts
This level introduces **System Automation** and the exploitation of **Scheduled Tasks** to retrieve credentials.

1. The Cron Daemon: The **cron** service is a background process in Linux that executes commands or scripts at predefined intervals. It is essential for routine system maintenance, such as log rotation or clearing temporary directories.

* **The Crontab:** Schedules are defined in "cron tables." These files specify the timing (minute, hour, day) and the specific command to be executed.
* **The Opportunity:** Scheduled tasks often run with the permissions of the user who created them. If a task is scheduled by a higher-privileged user, it may inadvertently leave behind data that lower-privileged users can access.

2. Service Discovery in `/etc/cron.d/`: System-wide cron jobs are typically stored in `/etc/cron.d/`. By examining the configuration files within this directory, the following can be determined:

* Which scripts are active.
* How frequently the scripts execute.
* Which user (e.g., `bandit22`) is running the script.

3. Script Logic and Data Redirection: Scheduled tasks frequently involve shell scripts that automate a series of commands.

* **The Mechanism:** A script might be programmed to read a password file and redirect that content into a temporary file.
* **Analysis:** By reading the contents of the script, the exact destination of the output can be identified. This allows for the retrieval of the credentials from a secondary location (such as `/tmp`) where the data has been temporarily stored by the automated process.

4. Summary of the Workflow

i. **Locate** = Inspect `/etc/cron.d/` - Find the scheduled task for the next user. 
ii. **Identify** = Read the cron configuration - Determine which script is being executed. 
iii. **Analyze** = Read the shell script - Find the output path where the password is saved. 
iv. **Retrieve** = Access the output file - Obtain the credentials for the next level. 


# Bandit Level 22 → Level 23

## Level Goal 
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

Commands you may need to solve this level: cron, crontab, crontab(5) (use “man 5 crontab” to access this)

## Solve
```
bandit22@bandit:~$ ls -la /etc/cron.d
total 36
drwxr-xr-x  2 root root 4096 Jul 11  2020 .
drwxr-xr-x 87 root root 4096 May 14  2020 ..
-rw-r--r--  1 root root   62 May 14  2020 cronjob_bandit15_root
-rw-r--r--  1 root root   62 Jul 11  2020 cronjob_bandit17_root
-rw-r--r--  1 root root  120 May  7  2020 cronjob_bandit22
-rw-r--r--  1 root root  122 May  7  2020 cronjob_bandit23
-rw-r--r--  1 root root  120 May 14  2020 cronjob_bandit24
-rw-r--r--  1 root root   62 May 14  2020 cronjob_bandit25_root
-rw-r--r--  1 root root  102 Oct  7  2017 .placeholder
bandit22@bandit:~$ cat /etc/cron.d/cronjob_bandit23
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
bandit22@bandit:~$ cat /usr/bin/cronjob_bandit23.sh
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget

bandit22@bandit:~$ echo I am user bandit23 | md5sum | cut -d ' ' -f 1
8ca319486bfbbc3663ea0fbe81326349
bandit22@bandit:~$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349
jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n
```

## Theory Concepts
This level centers on **Predictive Analysis** and the reverse-engineering of shell scripts that use **Deterministic Hashing**.

1. Script Logic Emulation: In this scenario, a scheduled task (cron job) executes a script that generates a password file in a hidden location. Unlike previous levels, where the path was static, this script generates the filename dynamically based on the current username. To find the password for the next level, the logic applied to the target username (`bandit23`) must be manually replicated.

2. Deterministic Hashing (MD5): The script utilises the **MD5 (Message Digest 5)** algorithm to transform a username into a unique string.

* **The Concept:** Hashing is a one-way mathematical function.
* **Determinism:** Because the process is deterministic, providing the same input string will always result in the same output hash.
* **The Vulnerability:** Since the hashing method is visible in the script, the "secret" filename is not actually secret; it is a predictable value that can be pre-calculated by anyone with access to the script's code.

3. Command Substitution and Variables: The script relies on shell variables and command substitution to function.

* **Variable Expansion:** The script uses `$myname` or `$USER` to capture the identity of the user running it.
* **Command Pipelines:** By piping the username through `echo`, `md5sum`, and `cut`, the script strips away unnecessary data to produce a clean, alphanumeric filename.
* **Replication:** By executing these exact commands in the terminal using "bandit23" as the input string, the resulting hash reveals the name of the file currently sitting in the `/tmp` directory.
