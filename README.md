# Anonymity Sets Of Privacy Coins

This repo contains a whitepaper about the Anonymity Sets of Privacy coins, in particular of Zcash Protocol coins, where they are specifically called Shieled Pools.

# Definition of Anonymity Set (anonset)

The idea of anonymity set is actually something simple, with a complex name. If you are playing "Where's Waldo", the anonset is the number of people Waldo is hiding amongst. Mathematically, the larger the number of people, the less chance of picking at random and choosing correctly.

To be more precise, if there are `N` people that Waldo is hiding amongst, there is a `1/N` chance of randomly choosing him in the group of people. When `N=1` there is nobody to hide amongst and there is 100% chance. When `N=100`, there is a 1% chance, and as `N` increases, the chance of randomly choosing the correct person goes to zero.

# Different Kinds Of Anonsets

Privacy coins based on CryptoNote Protocol, such as Monero and related forks, have anonymity sets that are *per transaction*. One transaction from Alice to Bob has it's own, it is not network-wide, such as in Zcash Protocol coins.

Monero currently uses an anonset size of 11 for each transaction, known as *mixins*. Some Monero forks use larger values, but these are small numbers which are much smaller than Zcash Protocol coins. Currently as of June 2021, HUSH has an anonset of about 500,000, which protects every shielded transaction.

MimbleWimble Protocol coins have anonsets which are shared across an entire block, which can be considered strictly better than CryptoNote Protocol but not as beneficial as network-wide anonsets of Zcash Protocol. There is research that shows a malicious node can listen to network traffic and further degrate the anonset to individual transactions inside the block, but this data does not appear on a block explorer.

# Zcash Protocol Anonsets

Since Zcash Protocol has the largest anonsets which give the most privacy, and since Hush is based on Zcash Protocol, we will focus on this "flavor" of anonsets.