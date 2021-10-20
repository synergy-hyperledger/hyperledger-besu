## Developer Quickstart

## Install cURL
Command Line tool for transferring data using various network protocols. The name cURL stands for "Client URL".

`$ sudo apt update && sudo apt upgrade`

`$ sudo apt install curl`

Once the command line tool is installed, run the following command:
`$ curl --version`

## Install Docker
Docker is a set of platform as a service products that use OS-level virtualization to deliver software in packages called containers.

Use apt package manager to install Docker package.

`$ sudo apt update `

`$ sudo apt install docker.io`

Start and enable Docker service

`$ sudo systemctl start docker`

`$ sudo systemctl enable docker`

Check the status of Docker service and ensure that it is running. 
`$ sudo systemctl status docker`

### Configure user to work with Docker CLI

We need to add the user to docker group, so that the user can execute the docker commands.

`$ sudo usermod -aG docker synergy_hyperledger`

> **Note**: The changes will take effect in the new session. It is recommended that you logout and login to check if the user group 'docker' is added to user 'synergy_hyperledger'.

Let us verify the version of Docker installed.

`$ docker --version`

## Install Docker Compose

Docker Compose is a tool for running multi-container Docker applications.

`$ sudo apt update`

`$ sudo apt install docker-compose`

## Install Node.js

To install a different version of Node.js, we can use a PPA (Personal package archive) maintained by NodeSource. These PPAs have more versions of Node.js available than the official Ubuntu repositories. Node.js v12, v14, v16, v17 are available as of the time of writing. 
```
curl -fsSL https://deb.nodesource.com/setup_17.x | sudo -E bash -
sudo apt-get install -y nodejs
```
We may need to install development Tools to build native addons
```
sudo apt-get install gcc g++ make
```
To install Yarn package manager, 
```
curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | gpg --dearmor | sudo tee /usr/share/keyrings/yarnkey.gpg >/dev/null

echo "deb [signed-by=/usr/share/keyrings/yarnkey.gpg] https://dl.yarnpkg.com/debian stable main" | sudo tee /etc/apt/sources.list.d/yarn.list

sudo apt-get update && sudo apt-get install yarn
```
Verify the version of Node.js installed
```
node --version
```
## Quorum Developer Quickstart

Quorum Developer Quickstart tool can be used to rapidly generate local Quorum blockchain networks for development purposes using tools like GoQuorum, Besu, and Codefi Orchestrate.
```
npx quorum-dev-quickstart
```
Which Ethereum client would you like to run? 

 1. Hyperledger Besu
 2. GoQuorum

Do you want to try out Codefi Orchestrate? Note: choosing yes will direct you to a login/registration page. [Y/n] - n

Do you wish to enable support for private transactions? [Y/n] - Y

Do you wish to enable support for logging with Splunk or ELK (Elasticsearch, Logstash & Kibana)? Default: [1]

 1. None
 2. Splunk
 3. ELK

Where should we create the config files for this network? Please choose either an empty directory, or a path to a new directory that does not yet exist. Default: ./quorum-test-network

To start your test network, run 'run.sh' in the directory, './quorum-test-network'
For more information on the test network, see 'README.md' in the directory, './quorum-test-network'
