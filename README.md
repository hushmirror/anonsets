# Anonymity Sets Of Privacy Coins

This repo contains a whitepaper about the Anonymity Sets of Privacy coins, in particular of Zcash Protocol coins, where they are specifically called Shieled Pools.

# Definition of Anonymity Set (anonset)

The idea of anonymity set is actually something simple, with a complex name. If you are playing "Where's Waldo", the anonset is the number of people Waldo is hiding amongst. Mathematically, the larger the number of people, the less chance of picking at random and choosing correctly.

To be more precise, if there are `N` people that Waldo is hiding amongst, there is a `1/N` chance of randomly choosing him in the group of people. When `N=1` there is nobody to hide amongst and there is 100% chance. When `N=100`, there is a 1% chance, and as `N` increases, the chance of randomly choosing the correct person goes to zero.

# Different Kinds Of Anonsets

Privacy coins based on CryptoNote Protocol, such as Monero and related forks, have anonymity sets that are *per transaction*. One transaction from Alice to Bob has it's own, it is not network-wide, such as in Zcash Protocol coins.

Monero currently uses an anonset size of 11 for each transaction, known as *mixins*. Some Monero forks use larger values, but these are small numbers which are much smaller than network-wide anonsets in Zcash Protocol coins. Currently as of June 2021, HUSH has an anonset of about 500,000, which protects every shielded transaction.

MimbleWimble Protocol coins have anonsets which are shared across an entire block, which can be considered strictly better than CryptoNote Protocol but not as beneficial as network-wide anonsets of Zcash Protocol. There is research that shows a malicious node can listen to network traffic and further degrate the anonset to individual transactions inside the block, but this data does not appear on a block explorer.

In Zcash Protocol, via Zero Knowledge mathematics knowns as zk-SNARKs, each "shielded transaction" is protected by the entire network-wide anonset.

# Zcash Protocol Anonsets

Since Zcash Protocol has the largest anonsets which give the most privacy, and since Hush is based on Zcash Protocol, we will focus on this "flavor" of anonsets.

## Definitions

We will need to define a few more terms to precisely talk about measuring and studying the anonset, AKA shielded pool size, in Zcash Protocol coins.

### Transaction (tx)

Alice sends Bob money via a transaction, which has one or more inputs and one or more outputs. If there is one Bob receiving funds, there is often at least two outputs, one for Bob and one where Alice receives her *change*.

### Input

Money about to be spent from an address. Value coming into a transaction. Can be *transparent* or *shielded*.

### Output

Value being received to an address, also called an Unspent Transaction Output (UTXO). Can be *transparent* or *shielded*.

### Coinbase

The shady company stole it's name from this, which means newly mined funds, the block reward for mining a block. They are a special kind of input, one which has no history.

### Shielded Input

Inputs being spent from a shieled address (zaddr) came into existence as the output of a shielded transaction, unspent, and then become *spent* by being used as the input of a future shielded transaction (ztx).

Because it is shielded, the amount and address it's coming from does not appear in public blockchain data.

### Shielded Output

Value being received to a shielded address (zaddr), where Alice spent her funds and Bob received newly *unspent* funds.

Because it is shielded, the amount and address it's going to does not appear in public blockchain data.

### Transparent Input

Inputs with no privacy, where both amount and addresses is public data that can be seen on an explorer.

### Transparent Output

Outputs with no privacy.


## Anonset Definition

The anonset size at block height `H` can be defined

```
anonset(H) = shielded_outputs(H) - shielded_inputs(H)
```

where

```
shielded_outputs(H) = number of shielded outputs at height H
shielded_inputs(H) = number of *spent* outputs, i.e. shielded transaction inputs at height H
```

### Does Coin X have a bigger anonset than Coin Y?

This question doesn't quite make sense, because anonset is a function of block height. It can go up and down at different block heights. Does coin X at height `H1` have a larger anonset than coin Y at height `H2`? That is a well-formed question with a yes/no answer.

Since anonset sizes can go up and down at every block, just because one coin has a larger anonset at a certain height, doesn't mean that will be true for the next block.

### How do anonsets go down?

Whenever there are more shielded inputs than shielded outputs, the anonset goes down in that transaction. One can add up all the transactions of a block and also determine if a certian block height *increases* or *decreases* the anonset size.

Let's say Alice wants to send Bob 1 HUSH and she has 11 shielded outputs of amount 0.01, which add up to 1.1 HUSH. That gives her enough to send 1 HUSH to Bob and to pay the transaction fee of 0.0001 HUSH.

Her shielded transaction will have 11 shielded inputs. On Zcash and Pirate coins, the transaction will have two outputs, and therefore *decrease* the anonset by 9. This can often happen when miners get many small regular payments from a mining pool, then they spend the funds.

If Alice used Hush, Sietch would increase the number of outputs to 8, and therefore the anonset would only *decrease* by 3. Sietch helps to keep the anonset larger. In general, when Alice only needs to spent 1 input, Sietch *increases* the anonset by 7 or 8, depending on if there is change.

### What makes anonsets go up? HushChat

Since HushChat memos are amount=0 by default, that means they have 1 shielded input and 8 shielded outputs on average, which means each HushChat memo increases the anonset size by 7. The use of HushChat directly increases the anonset of HUSH. Every HushChat memo helps create a larger anonset to protect all users.