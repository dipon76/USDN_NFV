# USDN_NFV

This is the implementation of SDN/NFV framework based on microSDN protocol. The support environment is Contiki OS. 

Getting Started
---

**IMPORTANT** You'll also need to install the 20-bit mspgcc compiler.

For instructions on how to compile this please click [here](https://github.com/contiki-os/contiki/wiki/MSP430X)

For a pre-compiled version for Ubuntu-64 please click [here](https://github.com/pksec/msp430-gcc-4.7.3)

Some people have had issues trying to install this compiler, so if you're new to Contiki or Linux in general then I'd recommend doing the following:

- Use a clean Ubuntu64 installation, don't use Instant Contiki. Contiki is included as part of uSDN and it's not necessary to have a separate Contiki repo.
- Use the precompiled msp430-gcc version above. You literally just need to extract it to a folder of your choice and then add it to your path `export PATH=$PATH:<uri-to-your-mspgcc>`. Once you have done this your path should look something like this:

```
echo $PATH
/home/mike/Compilers/mspgcc-.7.3/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/usr/lib/jvm/java-8-oracle/bin:/usr/lib/jvm/java-8-oracle/db/bin:/usr/lib/jvm/java-8-oracle/jre/bin
```

- NB There is only *ONE* msp430-gcc compiler in the path. If there are two you need to remove the old one.
- Check the mspgcc version (`msp430-gcc --version`) it should be 4.7.3.

```
msp430-gcc (GCC) 4.7.3 20130411 (mspgcc dev 20120911)
Copyright (C) 2012 Free Software Foundation, Inc.
This is free software; see the source for copying conditions. There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```
You are now ready move on to the next stage! If you haven't properly set it up to use the 20-bit mspgcc then it will not compile!!!

Because of the size of the stack, if you're testing in Cooja you'll need to compile for exp5438 motes (*there is a Makefile.target which should handle this for you*). Please note that you'll need to run make in *both* sdn/controller and sdn/node as I haven't set it up to do both in the higher level directory.

```
  cd usdn/examples/sdn/controller/
  make clean & make
  cd ..
  cd node/
  make clean & make
```

To get you going you can find some Cooja examples in:

 **usdn/examples/sdn/..**

There is a handy compile script in there that can be used to compile both the controller and node:
```
./compile.sh MULTIFLOW=1 NUM_APPS=1 FLOWIDS=1 TXNODES=8 RXNODES=6 DELAY=0 BRMIN=5 BRMAX=5 NSUFREQ=600 FTLIFETIME=300 FTREFRESH=1 FORCENSU=1 LOG_LEVEL_SDN=LOG_LEVEL_DBG LOG_LEVEL_ATOM=LOG_LEVEL_DBG SDN=1 RPL=1
```


How to run. 
---

Right now the SDN/NFV implementation is compiled in the project. Just follow the process: 
1. go to usdn/tools/cooja
2. execute "ant run" ( make sure you have 'ant' install in your machine)
3. go to open simulation and open usdn/examples/usdn-redirect.csc
4. start the simulation, you will find the transmission log in the mote output. 
