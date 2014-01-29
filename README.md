flow-pairs
===========

Flow-pairs:  A top 10 script gone crazy

Description:
The flow-pairs script gives a picture of large bandwidth consumers within
a given flow file.  It has two personalities, invoked by using -pairs or
-ports, which give a look at a host's peers and a detailed look at TCP/UDP
ports, respectively.  The key feature of the script is "aggregation", in
which ephemeral ports are collected into a single category, so that usage
patterns can emerge.

About:
Written by Mike Hunter (mhunter@ack.berkeley.edu)
Hacked by Max Baker (max@warped.org)

License:
See license.txt

Installation:
See INSTALL

Bugs:
On/off campus distinction is hard-coded
Memory hog; really needs to be rewritten in C[++]

Documentation:
Somewhat lacking.  Check out "pairs.html" and "ports.html" to get a feel
for the data format.  For usage examples, see the rest of this document.
Last but not least, check out the perl POD in "flow-pairs" itself.

-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|


% flow-cat /data3/netflow.inr-666/ft-v05.2003-08-07.081501-0700 
| flow-pairs -peers-display 10

(Show 10 peers for the top 10 (default) hosts by octets (default) )

Command: -peers-display 10 
(F Flows) (I- Incoming) (O- Outgoing) (T- Total) (-P Packets) (-O Octets)
"I-O" means Incoming Octets.  "*" means "not otherwise accounted for"

Processing big data
Finished reading data (39152/1283340)
Finished big sort
(Page    1)
Host                  Peer                    F  I-P   I-O  O-P   O-O  T-P   T-O
169.229.99.160:*      217.85.167.37:*       .4K  57K 2301K 113K  162M 170K  164M
169.229.99.160:*      204.65.25.17:2710      16  40K 1624K  81K  118M 121K  119M
169.229.99.160:*      62.161.190.11:23234     6  15K  603K  30K 44.1M  45K 44.7M
169.229.99.160:*      209.250.76.11:26788     2 7.1K  309K  10K 14.9M  17K 15.2M
169.229.99.160:*      212.17.117.162:*       24  153  7092    0     0  153  7092
169.229.99.160:*      217.232.31.142:2361    16   40  1808   24  2432   64  4240
169.229.99.160:*      217.232.31.142:2345     8   20   956   13  1308   33  2264
169.229.99.160:*      128.121.26.136:80       3   10   692    5   502   15  1194
169.229.99.160:*      217.232.31.142:2342     4   10   450    6   606   16  1056
169.229.99.160:*      *:*                    11   21  1439    6   240   27  1679
169.229.99.160        TOTAL:                .5K 120K 4850K 234K  338M 354K  343M


(Page    2)
Host                  Peer                    F  I-P   I-O  O-P   O-O  T-P   T-O
128.32.98.151:80      66.233.138.218:*      .2K 7.3K  361K  13K 17.2M  20K 17.5M
128.32.98.151:80      4.33.164.176:*        .2K 6.4K  302K  11K 13.7M  17K   14M
128.32.98.151:80      217.238.114.8:*        66 5.1K  234K 9.5K 12.7M  15K 12.9M
128.32.98.151:80      81.132.186.94:*        15 5.1K  223K 8.9K   12M  14K 12.3M
128.32.98.151:80      68.10.165.99:*        .2K 2.6K  130K 8.7K 11.3M  11K 11.5M
128.32.98.151:80      169.207.58.82:*       .2K 4.7K  217K 6.9K 9245K  12K 9462K
128.32.98.151:80      68.110.15.42:*         90 3.4K  156K 5.6K 7380K 9.1K 7536K
128.32.98.151:80      68.102.168.125:*       73 2.6K  116K 4.2K 5790K 6.8K 5907K
128.32.98.151:80      66.136.50.179:*       .1K 2.9K  136K 4.2K 5553K 7.1K 5689K
128.32.98.151:80      *:*                   31K 190K 14.6M 224K  223M 414K  238M
128.32.98.151         TOTAL:                32K 230K 16.4M 295K  317M 525K  334M

...


-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|


flow-cat ... | ./flow-pairs -peers-display 100 -persons 169.229.39.160 

(Show the top 100 peers for the host 169.229.99.160 (100 not shown because 100
fewer than 100 peers existed):

(Page    1)
Host                  Peer                    F  I-P   I-O  O-P   O-O  T-P   T-O
169.229.99.160:*      217.85.167.37:*       .4K  57K 2301K 113K  162M 170K  164M
169.229.99.160:*      204.65.25.17:2710      16  40K 1624K  81K  118M 121K  119M
169.229.99.160:*      62.161.190.11:23234     6  15K  603K  30K 44.1M  45K 44.7M
169.229.99.160:*      209.250.76.11:26788     2 7.1K  309K  10K 14.9M  17K 15.2M
169.229.99.160:*      212.17.117.162:*       24  153  7092    0     0  153  7092
169.229.99.160:*      217.232.31.142:2361    16   40  1808   24  2432   64  4240
169.229.99.160:*      217.232.31.142:2345     8   20   956   13  1308   33  2264
169.229.99.160:*      128.121.26.136:80       3   10   692    5   502   15  1194
169.229.99.160:*      217.232.31.142:2342     4   10   450    6   606   16  1056
169.229.99.160:*      63.175.146.25:80        3   10   903    0     0   10   903
169.229.99.160:*      220.166.100.236:3164    2    3   144    3   120    6   264
169.229.99.160:*      218.56.172.134:9051     2    2    96    2    80    4   176
169.229.99.160:*      203.75.172.100:3033     1    3   144    0     0    3   144
169.229.99.160:*      217.238.61.66:3152      1    2   104    0     0    2   104
169.229.99.160:*      218.56.172.134:27788    2    1    48    1    40    2    88
169.229.99.160:1430   209.211.56.201:23234    2   6K  259K  10K 15.3M  16K 15.6M
169.229.99.160:1413   209.211.56.201:23234    2 5.9K  255K  10K 15.2M  16K 15.5M
169.229.99.160:1418   209.250.76.11:26788     2 7.3K  319K  10K 14.9M  18K 15.3M
169.229.99.160        TOTAL:                .5K 139K 5683K 265K  384M 404K  389M


-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|


flow-cat ... | flow-pairs -ports -limit 5 -trash-off

(Show the port usage patterns, listing 3 (default) such patterns explicitly, 
for the top 5 hosts "on campus"):

(Page    1)
Host                         Known Port       F  I-P   I-O  O-P   O-O  T-P   T-O
doe-999-046.Lib               *->2710         9    0     0  81K  118M  81K  118M
doe-999-046.Lib               *->23234        5    0     0  51K 74.6M  51K 74.6M
doe-999-046.Lib             1418->26788       1    0     0  10K 14.9M  10K 14.9M
doe-999-046.Lib                Other:       .4K 139K 5683K 123K  177M 263K  182M

nor-90-493.Reshall            6881->*       .4K  111  5422 127K  148M 127K  148M
nor-90-493.Reshall            6882->*       .2K 6.9K  297K 112K  122M 119K  122M
nor-90-493.Reshall            6883->*       .3K    0     0  55K 64.8M  55K 64.8M
nor-90-493.Reshall             Other:       .7K 195K 26.3M  11K 12.6M 205K 38.9M

nntprelay                      *->119       .2K  13K 2662K 272K  330M 285K  333M
nntprelay                      119->*       .1K 306K 18.2M    0     0 306K 18.2M
nntprelay                    3011->1434       1    1   404    0     0    1   404
nntprelay                      Other:         9   15   768    6   240   21  1008

kosh.SSL                       80->*        16K    0     0 295K  317M 295K  317M
kosh.SSL                       *->80        16K 230K 16.4M    0     0 230K 16.4M
kosh.SSL                      *->2048        90  324 38.5K    0     0  324 38.5K
kosh.SSL                       Other:       .1K  165 17.1K  287 34.1K  452 51.1K

nor-91-333.Reshall          2140->58788       1    0     0  43K 58.2M  43K 58.2M
nor-91-333.Reshall           1750->4384       1    0     0  38K 52.4M  38K 52.4M
nor-91-333.Reshall            *->6881       .3K  20K  873K  39K 51.3M  59K 52.2M
nor-91-333.Reshall             Other:       .4K 255K 10.6M 127K  147M 383K  158M
