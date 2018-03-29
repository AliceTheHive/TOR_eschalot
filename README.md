# TOR_eschalot

Eschalot (Main)

(Main)    https://github.com/ReclaimYourPrivacy/eschalot/archive/master.zip <br>
(Others)  http://skunksworkedp2cg.onion/eschalot-1.2.0.tar.gz

The program:

Eschalot is a TOR hidden service name generator, it allows one to produce a (partially) customized vanity .onion address using a brute-force method.

Why eschalot? Well, eschalot is a different name for shallot and it is a fork of an older .onion names generator called shallot.

Eschalot is distributed in source form under BSD license. It should compile on any Unix or Linux system, but might need some minor modifications.

It was developed and most extensively tested on OpenBSD, but was also tested to compile and run on DragonFlyBSD, FreeBSD, CentOS Linux, and couple other mainstream Linux distributions whose names I do not recall at the moment. Various combinations of big/little endian platforms, 32bit/64bit platforms, and gcc/pcc/llvm/clang static analizer were tested. Many bugs were uncovered, some were fixed, some are still there - see TODO list if interested.

Bugs and ToDo list:
-------------------

0). Highest priority bug:
Every so often, while searching in a wordlist mode, eschalot finds the right prefix, but then, after finalizing the key and regenerating the .onion name, the result is garbage. I suspected my CPU or RAM overheating at first, but now I tend to think it's a bug in the program (or OpenSSL) somewhere. It gets detected and rejected and a message is printed on STDERR, but it's a big waste of hash cycles. Have to track it down.

-------------------

All the above is taken from the README file for eschalot. Eschalot runs somewhat faster than shallot, but has an even worse problem with bogus keys. Fortunately, this problem can be ameliorated by changing just a single bit in the source.

This program offers so much more than just a way to get a specific domain. It allows to search wordlists for matches. Pronouncable names of ten to twelve characters are commonly produced in wordlist mode. To match any one of them would require years with any other generator. The larger the list, the more frequently matches come out. Eschalot includes a second program, worgen, to produce compound search lists from some included simple word lists. Or you can make up your own lists.

Matches generated are sometimes laughable and one needs to mine the better keys from the larger list.
Sample run:

C:\eschalot-1.2.0>eschalot -cvt4 -l8-16 -f wordlist.txt > results.txt <br>
Verbose, continuous, no digits, 4 threads, prefixes 8-16 characters long. <br>
Reading words from wordlist.txt, please wait... <br>
Loaded 1300814 words. <br>
Sorting the word hashes and removing duplicates. <br>
Final word count: 1280298. <br>
Thread #1 started. <br>
Thread #2 started. <br>
Thread #3 started. <br>
Thread #4 started. <br>
Running, collecting performance data... <br>
Found a key for sorehead (8) - soreheadpraggzkd.onion <br>
Found a key for dampbeam (8) - dampbeam4jmamrku.onion <br>
Found a key for nineowls (8) - nineowlsxdoz6bo5.onion <br>
Found a key for highsoap (8) - highsoapwgkdn5uk.onion <br>
Total hashes: 112207616, running time: 10 seconds, hashes per second: 11220761 <br>
Found a key for poorcork (8) - poorcorkujm7zwdj.onion <br>
Found a key for neattest (8) - neattestx54ejtwz.onion <br>
Found a key for goodbuns (8) - goodbunsuqv5mxpx.onion <br>
Found a key for leanslip (8) - leanslipunvw7xkw.onion <br>
Found a key for ovalbomb (8) - ovalbombwrlnmyjo.onion <br>
Found a key for glibteam (8) - glibteamadzo63x3.onion <br>
Found a key for tidycars (8) - tidycars6oage64o.onion <br>

Eschalot may be freed of its bogus key bug by changing one bit in the source. This simultaneously doubles the efficiency of the word list search.

Old code:
#define RSA_E_LIMIT 0xFFFFFFFFu /* Max e */

New code:
#define RSA_E_LIMIT 0x7FFFFFFFu /* Max e */

Please note: The first F becomes a 7, a change of a single bit.

A precompiled windows executable with the above bogus key patch in the /files/ section.
