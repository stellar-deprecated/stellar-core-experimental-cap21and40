# LEIGHNOTES

My notes of useful commands and other things while hacking on stellar-core.

## Standalone cfg

The stellar-core.cfg file contains a standalone network config.

NOTE: The account minimum reserve is 20XLM.

## Useful commands

### First compile

./autogen.sh
./configure --enable-next-protocol-version-unsafe-for-production
time (make -j24)

### Run all the tests in parallel

rm -fr /tmp/pgtmp.* ; time (make check -j24 ALL_VERSIONS=1 NUM_PARTITIONS=24 BATCHSIZE=15)

### Run all the tests in parallel

rm -fr /tmp/pgtmp.* ; time (make check -j24 ALL_VERSIONS=1 NUM_PARTITIONS=24 BATCHSIZE=15 TEST_SPEC='txenvelope')

### Run a single test case or tests in serial

rm -fr /tmp/pgtmp.* ; time (make -j24) && time (src/stellar-core test 'txenvelope')

### Setup DB

src/stellar-core new-db

### Run stellar-core

src/stellar-core run

### Upgrade to protocol 18

curl 'http://localhost:11626/upgrades?mode=set&upgradetime=1970-01-01T00:00:00Z&protocolversion=18'

### Submit tx

curl -G localhost:11626/tx --data-urlencode "blob=$(stc -c <stc-tx-file>)"

### Helpful queries for monitoring

\watch 5 "select accountid,balance,seqnum,numsubentries from accounts order by lastmodified;"

\watch 5 "select txid,ledgerseq,txresult from txhistory;"

\watch 5 "select * from claimablebalance";
