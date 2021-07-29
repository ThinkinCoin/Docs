# Run a Read-only node

## Read-only node parameters <a id="read-only-node-parameters"></a>

* Minimum hardware requirements: AWS EC2 m5.xlarge with 4 vCPUs \(3.1 GHz\) and at least 1TB of Amazon EBS General Purpose SSD \(gp2\) storage \(or equivalent\).

## What are we going to do? <a id="what-are-we-going-to-do"></a>

1. 1. 1. **Launch Cloud Instance**

You can either run a node on your own hardware or use a cloud provider. We would recommend choosing one of the big cloud providers, e.g. Amazon AWS.

### Node Specifications <a id="node-specifications"></a>

We recommend the following or better: m5.xlarge **General Purpose Instance** with 4 vCPUs \(3.1 GHz\), 16GB of memory, up to 10 Gbps network bandwidth, and at least **1TB** of disk space.

We would recommend going with Ubuntu Server 20.04 LTS \(64-bit\).

### Network Settings <a id="network-settings"></a>

Open up port 22 for SSH, as well as port 5050 for both TCP and UDP traffic.

### Set up Non-Root User <a id="setup-non-root-user"></a>

If there is already a non-root user available, you can skip this step.

```text
# SSH into your machine# Update the system$ sudo apt-get update && sudo apt-get upgrade -y# Create a non-root user$ USER={USERNAME}$ sudo mkdir -p /home/$USER/.ssh$ sudo touch /home/$USER/.ssh/authorized_keys$ sudo useradd -d /home/$USER $USER$ sudo usermod -aG sudo $USER$ sudo chown -R $USER:$USER /home/$USER/$ sudo chmod 700 /home/$USER/.ssh$ sudo chmod 644 /home/$USER/.ssh/authorized_keys
```

Make sure to paste your public SSH key into the **authorized\_keys** file of the newly created user in order to be able to log in via SSH.

```text
# Enable sudo without password for the user$ sudo vi /etc/sudoers
```

Add the following line to the end of the file:

```text
{USERNAME} ALL=NOPASSWD: ALL
```

Now close the root SSH connection to the machine and log in as your newly created user:

```text
# Close the root SSH connection$ exit# Log in as new user(local)$ ssh {USERNAME}@{IP_ADDRESS}
```

You are still logged in as the new user via SSH. Now we are going to install **Go** and **Opera**.

First, install the required build tools:

```text
# Install build-essential$ sudo apt-get install -y build-essential
```

### Install Go <a id="install-go"></a>

```text
# Install go$ wget https://dl.google.com/go/go1.15.10.linux-amd64.tar.gz$ sudo tar -xvf go1.15.10.linux-amd64.tar.gz$ sudo mv go /usr/local
```

Export the required Go paths:

```text
# Export go paths$ vi ~/.bash_aliases# Append the following linesexport GOROOT=/usr/local/goexport GOPATH=$HOME/goexport PATH=$GOPATH/bin:$GOROOT/bin:$PATH
```

### Validate your Go installation <a id="validate-your-go-installation"></a>

### Install Opera <a id="install-opera"></a>

```text
# Install Opera$ git clone https://github.com/Fantom-foundation/go-opera.git$ cd go-opera/$ git checkout release/1.0.1-rc.1$ make
```

Validate your **Opera** installation:

```text
$./build/opera help​VERSION:1.0.1-rc.1
```

\*For latest update, please check [https://github.com/Fantom-foundation/lachesis\_launch](https://github.com/Fantom-foundation/lachesis_launch).

