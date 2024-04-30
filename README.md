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

   *after the installatio you will be able to see this interface---🥇*
