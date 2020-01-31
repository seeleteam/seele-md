FAQ
===

Q&A
---

genesis block hash mismatch
~~~~~~~~~~~~~~~~~~~~~~~~~~~

If the log looks like the following:

-  Windows:

::

   data folder: C:\Users\seele\.seele\node1
   INFO[0000] NewSeeleService BlockChain datadir is C:\Users\seele\.seele\node1\db\blockchain  caller="seeleservice.go:62" module=seele
   INFO[0000] NewSeeleService account state datadir is C:\Users\seele\.seele\node1\db\accountState  caller="seeleservice.go:72" module=seele
   ERRO[0000] NewSeeleService genesis.Initialize err. genesis block hash mismatch  caller="seeleservice.go:88" module=seele
   genesis block hash mismatch

-  Linux:

::

   log folder: /var/folders/dq/mcz24sr571g48wrbjvdbpndw0000gn/T/seeleTemp/log
   data folder: /Home/seele/.seele/node1
   INFO[0000] NewSeeleService BlockChain datadir is /Home/seele/.seele/node1/db/blockchain  caller="seeleservice.go:62" module=seele
   INFO[0000] NewSeeleService account state datadir is /Home/seele/.seele/node1/db/accountState  caller="seeleservice.go:72" module=seele
   ERRO[0000] NewSeeleService genesis.Initialize err. genesis block hash mismatch  caller="seeleservice.go:88" module=seele
   genesis block hash mismatch

You can just delete the .seele/node1 folder and restart. The absolute
path to the .seele folder is in the logs printed above.
