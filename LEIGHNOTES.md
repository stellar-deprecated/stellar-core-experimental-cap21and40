# LEIGHNOTES

My notes of useful commands and other things while hacking on stellar-core.

## Standalone cfg

The stellar-core.cfg file contains a standalone network config.

NOTE: The account minimum reserve is 20XLM.

## Useful commands

### Configure

./autogen.sh
./configure --disable-tests --enable-next-protocol-version-unsafe-for-production

### Compile

time (make -j24)

### Setup DB

src/stellar-core new-db

### Run stellar-core

src/stellar-core run

### Upgrade to protocol 18

curl 'http://localhost:11626/upgrades?mode=set&upgradetime=1970-01-01T00:00:00Z&protocolversion=18'

### Submit tx

curl -G localhost:11626/tx --data-urlencode "blob=$(stc -c <stc-tx-file>)"

### Helpful queries for monitoring

select accountid,balance,seqnum,numsubentries from accounts order by lastmodified;

select txid,ledgerseq,txresult from txhistory;

select * from claimablebalance;
