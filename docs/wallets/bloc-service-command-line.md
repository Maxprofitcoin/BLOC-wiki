# What is BLOC-Service

This section describes **BLOC** integration process into your service with **BLOC e-commerce** solution called **bloc-service**.
bloc-service is the substitue of old **walletd** a HTTP server which provides JSON 2.0 RPC interface for [BLOC](https://bloc.money) payment operations and address management. **bloc-service** allows you to accept incoming payments, generate an address for each user via a robust API and much more features explained as follow.

## **Getting ready**

To start integration process you should follow this easy steps:

## **Downloading**

If you wish to compile **bloc-service** and **BLOCd** yourself you can download the [source Code](https://github.com/furiousteam/BLOC.git).

Binary distributions can be found: [here](https://github.com/furiousteam/BLOC/releases/latest).

Select the appropriate file for the target platform (Windows, Mac, Linux).

Binaries are provided in `.zip` format, while source code is provided in `.zip` and `.tar.gz` format.

## **Installing**

### Installing on Windows

Extract the *.zip* file (`BLOC-...-windows.zip`).

### Installing on Mac

Extract the *.zip* file:

```bash
unzip BLOC-...-mac.zip
```

### Installing on Linux

Extract the *.zip* file:

```bash
unzip BLOC-...-linux.zip
```

## **Synchronizing the Blockchain**

Here's a quick image of `BLOCd MAIN NET` in action:

![BLOCd MAIN NET](../wallets/images/BLOCd/BLOC-MAINNET-3.0.0.1.png)

Here's a quick image of `BLOCd TEST NET` in action:

![BLOCd TEST NET](../wallets/images/BLOCd/BLOC-TESTNET-3.0.0.1.jpg)


Running `BLOCd` will start the **BLOCd** network daemon, which will connect to the network and begin downloading and verifying the BLOC blockchain.  

Because the blockchain is constantly growing, the file size always increases (the blockchain is currently over 2 GB), and **BLOCd must verify every block**, which is both CPU and disk intensive. An SSD with at least this much free disk space is recommended, unless you plan to use [remote nodes](../BLOC-servic#remote-node-options). 

### Using Checkpoints

You can sync a fresh chain from block 0 much quicker by using checkpoints. Follow [this guide](../API/Using-checkpoints-for-BLOCd.md) to learn more.

## **Errors**

* Make sure you check the [RPC Errors conditions](../wallets/bloc-service-rpc-api-error-conditions.md).

## **bloc-service RPC Clients**

* [Javascript](https://github.com/furiousteam/bloc-rpc): A JavaScript wrapper for the bloc-service RPC interface.
* [NodeJS](https://www.npmjs.com/package/bloc-rpc): This project is designed to make it very easy to interact with various RPC APIs available within the BLOC Project. This entire project uses Javascript Promises to make things fast, easy, and safe.
* [Go](https://github.com/furiousteam/bloc-rpc-go): A Golang wrapper for the BLOC RPC API. This project makes it easy to send requests to particular RPC server and returns a clear response without any abrupt termination.
* [PHP](https://github.com/furiousteam/bloc-rpc-php): A PHP wrapper for BLOC's RPC interfaces.

See [bloc-service RPC API](wallet-rpc-api.md) for usage.


## **Ready to work with bloc-service**

Once **BLOCd** has been successfully synchronised we are ready to operate with **bloc-service**

The following examples are made using a Linux system but the concept is the same for all the OS supported by the **bloc-service**.

bloc-service screenshot:

![--help](images/bloc-service/help.png)


## **Command line options**

This is the command line options available since the bloc-service v3.0

```
  Common Options:
  -c [ --config ] arg                configuration file
  -h [ --help ]                      produce this help message and exit
  -v [ --version ]                   Output version information
  --bind-address arg (=127.0.0.1)    payment service bind address
  --bind-port arg (=8070)            payment service bind port
  --rpc-password arg                 Specify the password to access the rpc 
                                     server.
  --rpc-legacy-security              Enable legacy mode (no password for RPC). 
                                     WARNING: INSECURE. USE ONLY AS A LAST 
                                     RESORT.
  -w [ --container-file ] arg        container file
  -p [ --container-password ] arg    container password
  -g [ --generate-container ]        generate new container file with one 
                                     wallet and exit
  --view-key arg                     generate a container with this secret key 
                                     view
  --spend-key arg                    generate a container with this secret 
                                     spend key
  --mnemonic-seed arg                generate a container with this mnemonic 
                                     seed
  -d [ --daemon ]                    run as daemon in Unix or as service in 
                                     Windows
  -l [ --log-file ] arg              log file
  --server-root arg                  server root. The service will use it as 
                                     working directory. Don't set it if don't 
                                     want to change it
  --log-level arg                    log level
  --SYNC_FROM_ZERO                   sync from timestamp 0
  --address                          print wallet addresses and exit
  --enable-cors arg                  Adds header 'Access-Control-Allow-Origin' 
                                     to walletd's RPC responses. Uses the value
                                     as domain. Use * for all.
  --scan-height arg                  The height to begin scanning a wallet from
```

## **Remote Node options**

```
Remote Node Options:
  --daemon-address arg (=localhost)  daemon address
  --daemon-port arg (=2086)          daemon port
```

### --daemon-address arg (=127.0.0.1)
### --daemon-port arg (=2086)

Remote connection allows you to bind your **bloc-service** RPC Wallet to a remote BLOC daemon **BLOCd**. Such type of connection allows you to start **bloc-service** RPC Wallet without having to download the blockchain. Your wallet will be instantly synchronised. Always make sure that you trust the remote connection you are connecting to.

* For local daemons use localhost or 127.0.0.1 as an IP address.
* For remote daemons specify the remote daemon IP address.
* Default BLOC daemon port is 2086 (for rpc calls).

Use the following command to start **bloc-service** RPC Wallet with a remote connection: 

**Example**

```
./bloc-service --container-file=mycontainer --container-password=mypassword --daemon-address=IP.OF.YOUR.DAEMON --daemon-port=2086 --bind-address=0.0.0.0 --bind-port=8070 --rpc-password=RPCpassword
```

**Expected results**

```
You have connected to a node that charges a fee to send transactions.
The fee for sending transactions is: 0.0005 BLOC per transaction. 
If you don't want to pay the node fee, please relaunch BLOCWallet and specify a different node or run your own.
```

![--remote-node](images/bloc-service/remote-node.png)


## **Command line Options**

### --help

Display the help message and configuration settings.

#### Example

```
./bloc-service --help
```

**Expected results**

![--help](images/bloc-service/help.png)


### --config arg (=myconf.conf)

Specify a configuration file to start bloc-service. This is much more simple to use if you have a particular configuration and you do not want to type all the arguments while launching bloc-service.

#### Example

```
./bloc-service --config=myconf.conf
```

### --version

Display the current version of bloc-service

#### Example

```
./bloc-service --version
```

**Expected results**

![--help](images/bloc-service/--version.png)


## **Command line arguments**

All the following command line options and arguments must be used when start **bloc-service**

* You can use them directly in the command line and provided examples
* Or you can use them in the config file which is the best option

### --bind-address arg (=127.0.0.1)**

* Interface for bloc-service RPC
* Started by default on 127.0.0.1 when running either you specified it `./bloc-service --config=myconf.conf`
* If you want to use local only : 127.0.0.1
* if you want to open to public : 0.0.0.0d)
* More details about the [JSON bloc-service API](../wallet-rpc-api.md)

#### Example

```
./bloc-service --bind-address=127.0.0.1 --container-file=mycontainer --container-password=mypassword --rpc-password=RPCpassword
```

### --bind-port arg (=8070)

* Port for bloc-service RPC
* Started by default on 8070 when running either you specified it `./bloc-service --config=myconf.conf`
* You can change the port here for ex 8071
* More details about the [JSON bloc-service API](../wallet-rpc-api.md)

#### Example

```
./bloc-service --bind-port=8071 --container-file=mycontainer --container-password=mypassword --rpc-password=RPCpassword
```

### --rpc-password

Setup the rpc password to connect to bloc-service

#### Example

```
./bloc-service --container-file=mycontainer --container-password=mypassword --rpc-password=RPCpassword
```

### --rpc-legacy-security arg (=8070)

* Enable legacy mode (no password for RPC). 
* **WARNING: INSECURE. USE ONLY AS A LAST RESORT.**

#### Example

```
./bloc-service --container-file=mycontainer --container-password=mypassword --rpc-legacy-security
```

### --container-file=(arg)

* Container file is the only file that stores all data required to run your bloc-service. It contains user addresses and private keys required to operate them.
* This function works only coupled with `--container-password` and `--generate-container`

### --container-password=(arg)

* Container password file is the only file that stores all data required to run your bloc-service. It contains user addresses and private keys required to operate them.
* This function works only coupled with `--container-file` and `--generate-container`

### --generate-container

* Generate a new container file with one wallet and exit.
* This function works only coupled with `--container-file` and `--container-password`

#### Example

```
./bloc-service  --container-file=mycontainer --container-password=mypassword --generate-container 
```

**Expected results**

![generate-container](images/bloc-service/generate-container.png)

### --address

Start `bloc-service` to display the 1st wallet address in the container and exit

**Example**

```
./bloc-service --container-file=mycontainer --container-password=mypassword --rpc-password=RPCpassword --address
```

**Expected results**

![--address](images/bloc-service/load-wallet-and-exit.png)


### --log-level

* Specify another log file than the original one created by BLOCd with a level 2
* There is 5 different level. The higher you choose, the more details you get.
* Log level must be 0...5

**Example**

```
./bloc-service --container-file=mycontainer --container-password=mypassword --rpc-password=RPCpassword --log-level=5
```

**Expected results**

![--log-level](images/bloc-service/--log-level.png)


### --log-file

* Specify another log file than the original one created by BLOCd named (BLOCd.log)
* The specified log file will be created in the same folder where BLOCd was started

**Example**

```
./bloc-service --container-file=mycontainer --container-password=mypassword --rpc-password=RPCpassword --log-file=testme.log
```

**Expected results**

![--log-file](images/bloc-service/--log-file.png)


### --SYNC_FROM_ZERO

Re-synchronize the wallet from block 0.

**Example**

```
./bloc-service --container-file=mycontainer --container-password=mypassword --rpc-password=RPCpassword --SYNC_FROM_ZERO
```

**Expected results**

![--SYNC_FROM_ZERO](images/bloc-service/SYNC_FROM_ZERO.png)


### --enable-cors arg

* Adds header 'Access-Control-Allow-Origin' to the bloc-service's RPC responses.
* Uses the value as domain
* Use * for all

**Example**

```
./bloc-service --container-file=mycontainer --container-password=mypassword --rpc-password=RPCpassword --enable-cors=*
```

**Expected results**

![--enable-cors](images/bloc-service/--enable-cors.png)


### --scan-height arg

The height to begin scanning for transactions at. This can greatly speed up wallet syncing time.

**Example**

```
./bloc-service --container-file=mycontainer --container-password=mypassword --rpc-password=RPCpassword --scan-height=100000
```

**Expected results**

![--scan-height](images/bloc-service/--scan-height.png)


### --daemon

bloc-service RPC wallet can be started in both daemon and console modes. 

* Daemon mode - **bloc-service** RPC Wallet is launched in the background, while you can continue to work with a console window. 
* Console mode - **bloc-service** RPC Wallet is launched and prints log messages on the screen.
* BLOC RPC wallet starts in console mode by default.

**Example**

```
./bloc-service --container-file=mycontainer --container-password=mypassword --daemon --bind-address=0.0.0.0 --bind-port=2053 --rpc-password=RPCpassword
```

**Expected results**

![--daemon](images/bloc-service/--daemon.png)



## **Create .CONF file**

* Create a txt file with your favorite text editor and open it.
* Check all your required parameters and enter them like in this example
* You need to type the arguments without the '--'

**Expected results**

![conf](images/bloc-service/myconf.png)

#### Example

```
container-file = mycontainer
container-password = mypassword
daemon-address = 127.0.0.1
daemon-port = 2086
bind-port = 8070
bind-address = 127.0.0.1
rpc-password = RPCpassword
```

[Download Example](images/bloc-service/myconf.conf)

* Place this file next to bloc-service
* Save it under the name `myconf.conf`

**Expected results**

![conf](images/bloc-service/CONF2.png)

**Notes**

* Config file path is relative to current working directory, not server root.
* Options `container-file` and `container-password` should ALWAYS be set (in either command line or config file mode).
* Options `container-file` and `log-file` options are relative to `server-root`. `server-root` default is the current working directory.


## **Generate a new wallet**

To start using **bloc-service** you must first generate a container.
Container file is the only file that stores all data required to run your service. It contains user addresses and private keys required to operate them.
**Make sure to backup this file regularly**.

To generate a new container you should run the following command:

```
./bloc-service --container-file=mycontainer --container-password=mypassword --generate-container 
```

* `mycontainer` is the container file name and a path to it (relative or absolute); path is optional in this argument, specifying only a container name will result in new file located in the same folder as **bloc-service** 
* `mypassword` is a secret password for the new wallet & container file.
* `generate-container` option tells **bloc-service** to generate container file and exit.

**Expected results**

![generate-container](images/bloc-service/generate-container.png)

*Note: if `mycontainer` exists **bloc-service** will show you the notification and will ask you to provide a different name*

If the operation was successful you will get a corresponding message with your new **BLOC** address. At the same time **bloc-service** will save your container on the local disk (in the same folder where **bloc-service** is located and shut down.


## **Start bloc-service**

* To start **bloc-service** RPC wallet you can use both command line and config file. Config file allows you to configure your settings only once and use `--config` option further.
* The command below launches **bloc-service** RPC Wallet with a specific config file:

```
./bloc-service --config=myconf.conf
```

* You may specify BLOC config directly through console arguments. Here is the same config file as above in console: 

```
./bloc-service --container-file=mycontainer --container-password=mypassword --daemon-address=127.0.0.1 --daemon-port=2086 --bind-address=127.0.0.1 --bind-port=8070 --rpc-password=RPCpassword 
```

**Expected results**

Start with command line:

![start bloc-service](images/bloc-service/start.png)

Start with myconf.conf:

![start bloc-service](images/bloc-service/start-conf.png)

## **Restore a existing BLOC wallet with bloc-service**##

We have different option to recover a wallet using **bloc-service**

### Using a old Walletd container file

If you were using Walletd that come with the previous version of BLOC, the previous container file is compatible with the new version. This is the step to follow:

* Copy the your previous configuration file `yourfile.conf` and copy the acual container file `mycontainer`
* Paste this 2 files next to the new `bloc-service` and `BLOCd`
* Open `yourfile.conf` 
* Make sure you remove this line `testnet = no` we are not using this field anymore
* Edit like this:

```
container-file = mycontainer
container-password = mypassword
daemon-port = 2086
bind-port = 8070
bind-address = 127.0.0.1
rpc-password = RPCpassword
```
* Save the file
* Start `bloc-service` using this configuration file
* ```./bloc-service --config=myconf.conf```
* Please wait until the synchronisation is complete
* Your wallet is ready to be used with the **bloc-service** RPC API.

**Expected results**

![start bloc-service](images/bloc-service/restore-old-wallet-file.png)


### Using your private spend key and view key

If you already have a [BLOC Wallet](../wallet/Making-a-Wallet.md) you must know your **private spend key** and your **private view key** to restore your wallet using **bloc-service**. To find how to generate view your private key using your favorite BLOC Wallet software please refer to the . [Wallet manuals available](../wallet/Making-a-Wallet.md).

* Create a txt file with your favorite text editor and open it.
* Check all your required parameters and enter them like in this example
* You need to type the arguments without the '--'
* Place this file next to bloc-service
* Save it under the name `myconf.conf`

```
container-file = mycontainer
container-password = mypassword
daemon-port = 2086
bind-port = 8070
bind-address = 127.0.0.1
rpc-password = RPCpassword
```
* Save the file

#### Generate a new container file

Generate a new container file with the following `--view-key` and `--spend-key` commands:

```
Enter your details:
./bloc-service --container-file=mycontainer --container-password=mypassword --view-key=myviewkey --spend-key=myspendkey --generate-container

Example:
./bloc-service --container-file=mycontainer --container-password=mypassword --view-key=e82ebf49b74fccd754e39ac3ca6fabca35277b012dfce0cf8921c216396b3108 --spend-key=cda47a19e5d433060ab79c885817cd20fc394dc7043ac875678a3698804ede01 --generate-container
```

**Expected results**

![start bloc-service](images/bloc-service/restore-using-private-keys.png)


* Start `bloc-service` using your configuration file

```
./bloc-service --config=myconf.conf
```

* Your wallet is now loaded
* Please wait until the synchronisation is complete

**Expected results**

![wallet loading after restore private key](images/bloc-service/wallet-loading-after-restore-private-key.png)


* Your wallet is ready to be used with the **bloc-service** RPC API.

**Expected results**

![wallet ready after restore private key](images/bloc-service/wallet-ready-after-restore-prviate-keys.png)


### Using your mnemonic-seed

If you already have a [BLOC Wallet](../wallet/Making-a-Wallet.md) created after the launch of the **BLOC V3.0** then you you must know your **mnemonic-seed** to restore your wallet using **bloc-service**. To find how to generate view your mnemonic-seed using your favorite **BLOC** Wallet software please refer to the [Wallet manuals available](../wallet/Making-a-Wallet.md).

* Create a txt file with your favorite text editor and open it.
* Check all your required parameters and enter them like in this example
* You need to type the arguments without the '--'
* Place this file next to bloc-service
* Save it under the name `mycontainer.conf`

```
container-file = mycontainer
container-password = mypassword
daemon-port = 2086
bind-port = 8070
bind-address = 0.0.0.0
rpc-password = RPCpassword
```
* Save the file

#### Generate a new container file

Generate a new container file with the following `--mnemonic-seed` commands:

```
Enter your details:
./bloc-service --container-file=mycontainer --container-password=mypassword --mnemonic-seed="your-mnemonic-seed" --generate-container

Example:
./bloc-service --container-file=mycontainer --container-password=mypassword --mnemonic-seed="jazz border dude orphans worry absorb slackens public drinks bovine evenings hurried roped jaws drinks snug directed pirate behind zero null cuisine agreed alchemy directed" --generate-container
```

**Expected results**

![start bloc-service](images/bloc-service/restore-using-mnemonic-seed.png)


* Start `bloc-service` using your configuration file

```
./bloc-service --config=myconf.conf
```
* Your wallet is now loaded
* Please wait until the synchronisation is complete

**Expected results**

![wallet ready for bloc-service](images/bloc-service/restore-using-mnemonic-seed-loading.png)

* Your wallet is ready to be used with the **bloc-service** RPC API.

**Expected results**

![wallet ready for bloc-service](images/bloc-service/restore-using-mnemonic-seed-loaded-ok.png)







__________________________________________________________________________________________________


## BLOC-DEVELOPER

Make sure you visit the dedicated website [BLOC-DEVELOPER.com](https://bloc-developer.com) to find out more details and test your application.

If anything is missing or seems incorrect, please check the [GitHub issues](https://github.com/furiousteam/BLOC-wiki/issues) for existing known issues or [create a new one](https://github.com/furiousteam/BLOC-wiki/issues/new).