# How-To-Install-Hyperledger-Fabric-v2.4-on-liinux
 -  Hyperledger_fabric installation -----------------
  - first understan that what is the fabric is :-⏬

 *Step 1: Install curl and git*

curl: A command-line tool for transferring data with URL syntax. It is used here to download files and scripts from the internet.
git: A version control system used for tracking changes in files and coordinating work among multiple developers. It is commonly used for managing source code during software development.
```
sudo apt update
sudo apt-get install git
sudo apt-get install curl
```


 *Step 2: Install Docker*

 
Docker: A platform for developing, shipping, and running applications in containers. Containers allow developers to package an application with all of its dependencies into a standardized unit for software 
        development.
       docker-compose: A tool for defining and running multi-container Docker applications. It allows you to use a YAML file to configure your application's services and then create and start all the services 
       from your configuration with a single command.

```
sudo apt-get -y install docker-compose
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -a -G docker <username>

```

*Step 3: Install Golang*

Go (Golang): A programming language developed by Google. It is known for its simplicity, efficiency, and concurrency features. Hyperledger Fabric is built using Go, so installing Go is necessary to compile and 
             run Fabric.

```
curl -O https://dl.google.com/go/go1.18.3.linux-amd64.tar.gz
tar xvf go1.18.3.linux-amd64.tar.gz
export GOPATH=$HOME/go
export PATH=$PATH:$GOPATH/bin
nano ~/.bashrc

```
- Add these lines at the end of the file:
```
export GOPATH=$HOME/go
export PATH=$PATH:$GOPATH/bin
```
*Then run:*
 ```
source ~/.bashrc
 ```

*Step 4: Install Hyperledger Fabric☑️*

- Hyperledger Fabric: One of the blockchain frameworks hosted by the Linux Foundation under the Hyperledger umbrella. It is a permissioned blockchain infrastructure, providing modular architecture and components 
  for building enterprise-grade Alternatively, to download the latest releases:blockchain solutions.
  Fabric version: Specifies the version of Hyperledger Fabric to install.
  Fabric CA version: Specifies the version of Fabric Certificate Authority (CA) to install. The CA provides services for issuing and managing digital certificates used by clients and peers in the network.

   *Now you' have to creat a diretory where u will install the fabric:--*
    - mkdir fabric-network
    - put verion as :=(Fabric v2.4.4 and Fabric CA v1.5.3)
    ```
   curl -sSL https://bit.ly/2ysbOFE | bash -s -- <fabric_version> <fabric-ca_version>
    ```
  - *or you can also use this commands to install the fabric::☑️*
   ```
   curl -sSL https://bit.ly/2ysbOFE | bash -s -- 2.4.4 1.5.3
   ```
  - *Alternatively, to download the latest releases*
   ````
    curl -sSL https://bit.ly/2ysbOFE | bash -s
   ````

   *after the installation ---To test the our installation, we will run test network that comes with fabric-samples:*
 ```
 cd fabric-samples/test-network
 ./network.sh up createChannel -ca -c mychannel -s couchdb
 ```
```
docker -ps 
```
*you will see some container's are running *
 *after running this command u will be able to see 🥸this insterface:-*
 - ![image](https://github.com/Rjesh2006/How-To-Install-Hyperledger-Fabric-v2.4-on-liinux/assets/143868643/5c8d980c-444d-4215-8fbb-4063a8cc32d8)

    **- if there is any error 😰then you have to follow this GIVEN  commands :---*

 ***update to be continued.......**
 ```
    curl -sSL https://bit.ly/2ysbOFE | bash -s -- 2.2.2 1.4.9
```
 - it will install the latest fabric ledger
   -then u will seee this interface:-⏬
   545454
   

## Setting up the configtxgen tool-

- Channels are created by building a channel creation transaction and submitting the transaction to the ordering service. The channel        creation transaction specifies the initial configuration of the channel and is used by the ordering service to write the channel genesis   block.
-  While it is possible to build the channel creation transaction file manually, it is easier to use the configtxgen tool. The tool works     by reading a configtx.yaml file that defines the configuration of your channel, and then writing the relevant information into the         channel creation transaction. The configtxgen tool was installed when you ran the curl command in the previous step.

 For the purposes of this tutorial, we will want to operate from the test-network directory inside fabric-samples. Navigate to that         directory using the   following command:
 ```
 cd fabric-samples/test-network
 ```
We will operate from the test-network directory for the remainder of the tutorial. Use the following command to add the configtxgen tool to your CLI path:
 ```
 export PATH=${PWD}/../bin:$PATH
 ```

In order to use configtxgen, you need to the set the FABRIC_CFG_PATH environment variable to the path of the directory that contains your local copy of the configtx.yaml file. For this tutorial, we will reference the configtx.yaml used to setup the Fabric test network in the configtx folder:

```
export FABRIC_CFG_PATH=${PWD}/configtx
```

you can check that you can are able to use the tool by printing the configtxgen help text:
 
```
configtxgen --help
```
## The configtx.yaml file:⬇️

  - The configtx.yaml file specifies the channel configuration of new channels. The information that is required to build the channel          configuration is specified in a readable and editable form in the configtx.yaml file. The configtxgen tool uses the channel profiles       defined in the configtx.yaml file to create the channel configuration and write it to the protobuf format that can be read by Fabric.
 
 -  You can find the configtx.yaml file that is used to deploy the test network in the configtx folder in the test-network directory. The      file contains the following information that we will use to create our new channel:
 
 -  Organizations: The organizations that can become members of your channel. Each organization has a reference to the cryptographic           material that is used to build the channel MSP.
 
 - Ordering service: Which ordering nodes will form the ordering service of the network, and consensus method they will use to agree to       a common order of transactions. The file also contains the organizations that will become the ordering service administrators.
 
 - Channel policies Different sections of the file work together to define the policies that will govern how organizations interact           with
   
 - the channel and which organizations need to approve channel updates. For the purposes of this tutorial, we will use the default            policies used by Fabric.
 
     Channel profiles Each channel profile references information from other sections of the configtx.yaml file to build a channel              configuration. The profiles are used the create the genesis block of the orderer system channel and the channels that will be used by      peer organizations. To distinguish them from the system channel, the channels used by peer organizations are often referred to as          application channels.
 
     The configtxgen tool uses configtx.yaml file to create a complete genesis block for the system channel. As a result, the system            channel profile needs to specify the full system channel configuration. The channel profile used to create the channel creation            transaction only needs to contain the additional configuration information required to create an application channel.
 
- *You can visit the Using configtx.yaml to build a channel configuration tutorial to learn more about this file. For now, we will return     to the operational aspects of creating the channel, though we will reference parts of this file in future steps.*
 
 
## Start the network:____
  We will use a running instance of the Fabric test network to create the new channel. For the sake of this tutorial, we want to operate     from a known initial state. The following command will kill any active containers and remove any previously generated artifacts. Make      sure that you are still operating from the test-network directory of your local clone of fabric-samples.

```
./network.sh down
```
- interface::--
- 4545

*You can then use the following command to start the test network:*
```
./network.sh up
- interface:--
  4545
```
 This command will create a Fabric network with the two peer organizations and the single ordering organization defined in the  configtx.yaml file. The peer organizations will operate one peer each, while the ordering service administrator will operate a single      ordering node. When you run the command, the script will print out logs of the nodes being created:
 - interfacce:----
 - 4545
  *Our instance of the test network was deployed without creating an application channel. However, the test network script creates the system channel when you issue the ./network.sh up command. Under the covers, the script uses the configtxgen tool and the configtx.yaml file to build the genesis block of the system channel. Because the system channel is used to create other channels, we need to take some time to understand the orderer system channel before we can create an application channel.*

## The orderer system channel:____
  The first channel that is created in a Fabric network is the system channel. The system channel defines the set of ordering nodes that     form the ordering service and the set of organizations that serve as ordering service administrators.
  
  The system channel also includes the organizations that are members of blockchain consortium. The consortium is a set of peer              organizations that belong to the system channel, but are not administrators of the ordering service. Consortium members have the ability   to create new channels and include other consortium organizations as channel members.
  
  The genesis block of the system channel is required to deploy a new ordering service. The test network script already created the system   channel genesis block when you issued the ./network.sh up command. The genesis block was used to deploy the single ordering node, which    used the block to create the system channel and form the ordering service of the network. If you examine the output of the ./network.sh    script, you can find the command that created the genesis block in your logs:
   
 - *You can now create the channel by using the following command:*🥇
 - 
   ```
   peer channel create -o localhost:7050  --ordererTLSHostnameOverride orderer.example.com -c channel1 -f ./channel-artifacts/channel1.tx --outputBlock ./channel-artifacts/channel1.block --tls --cafile "${PWD}/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem"
   ```
 The command above provides the path to the channel creation transaction file using the -f flag and uses the -c flag to specify the         channel name. The -o flag is used to select the ordering node that will be used to create the channel. The --cafile is the path to the     TLS certificate of the ordering node. When you run the peer channel create command, the peer CLI will generate the following response:
 
 - interface:----
    - 
  
 - *Because we are using a Raft ordering service, you may get some status unavailable messages that you can safely ignore. The command         will return the genesis block of the new channel to the location specified by the --outputBlock flag.*
   
   - interface:--
     45454


 **update to be continued later:_▶️ :---**
