# New Network

## Introduction

The purpose of this document is to describe in some detail the process of building a brand new Indy Network (Network) using 4 Stewards on their own separate nodes.
It goes more into details than [Starting a Network](../start-nodes.md).
These instructions are intended to be used for a distributed or “production” level environment, but can be adapted to be used to build a private network.

It is heavily based on [Create New Indy Network](https://docs.google.com/document/d/1XE2QOiGWuRzWdlxiI9LrG9Am9dCfPXBXnv52wGHorNE) and the [Steward Validator Preparation Guide v3](https://docs.google.com/document/d/18MNB7nEKerlcyZKof5AvGMy0GP9T82c4SWaxZkPzya4).

## Steps

### Create Network Governance documents (Optional)

   Network Governance describes the policies and procedures by which your new network will run and be maintained. Here’s an example: [Sovrin Governance Framework](https://docs.google.com/document/d/1K8l5MfXQWQtpT49-FHuYn_ZnRC5m0Nwk)


### Assign Network Trustees
   
   Trustee’s are the people who manage the network and protect the integrity of the Network Governance.  This includes managing the auth_rules.

   Generally speaking, for a production Network, at least 3 Trustees representing three different persons are required and more are preferred.  
   For a test Network one Trustee is required and 3 or more are preferred (all Trustee DID’s may belong to the same user on a test network if needed). 

   Initial Trustees (3 preferred) must create and submit a Trustee DID and Verkey so that the domain genesis file can be built.

   Each trustee has to [install the cli](./CLIInstall.md) and [create a Trustee DID](./CreateDID.md).


### Genesis Stewards

   A Steward is an organization responsible for running a Node on the Network

   Exactly 4 “Genesis” Stewards are needed, more Stewards can be added later.

   Each Genesis Steward’s node information will be included in the Genesis Pool file, so they should be willing to install and maintain a Node on the new Network for an extended period of time.

   Generate Stewards DIDs as described in [Creating DID](./CreateDID.md).
   
   To create the Validator Node keys you have to have indy-node installed.
   An installation process is described [here](../installation-and-configuration.md)
   Just run `init_indy_node <ALIAS> <node ip> <node port> <client ip> <client port>`.
   
   > WARNING!!! The seed that will be printed can be used to recreate the keys, so you have to store it safely!

   Create and give Genesis Stewards access to a spreadsheet like [this one](https://docs.google.com/spreadsheets/d/1LDduIeZp7pansd9deXeVSqGgdf0VdAHNMc7xYli3QAY/edit#gid=0) and have them fill out their own row with the DID and Validator Node information. Note the 2 sheets in the linked spreadsheet. Both will be used in the next step. 

### Create and Distribute genesis transaction file
   Use the following [script](https://github.com/sovrin-foundation/steward-tools/tree/master/create_genesis) with the 2 spreadsheets as input to create the genesis transaction file.
   If no spreadsheats are provided and the script is executed with the `-h` parameter, it will print out what csv files are needed.

### Schedule a meeting to instantiate the new network

   Invite all Genesis Stewards to a meeting where they are able to execute commands and share their screens for both an indy-cli and for their Validator Nodes being added to the Network.
    
   NOTE: It is very useful to go through some checks for each node to verify their setup before continuing. Some large amounts of debug and recovery work can be avoided by 5-10 minutes of checking configs of each node at the beginning of the meeting.
   + /etc/indy/indy_config.py - all nodes need to have the same network name (and that name should be a directory on each node and the  genesis files should be in those directories and have the correct permissions.)
   + /etc/indy/indy.env - all nodes should have local ip addresses in this file and be pointing at the correct ports.
   + Check network communication from one node to each other node on the client IP and port, and also check from a client on the internet to see that all Client IPs and ports are accessible. Node ports can be checked after the Network is up and running.  (e.g. nc -vz <IP> <port> can be used to check connectivity)

   1. Start all the nodes as described in [Start Nodes](../start-nodes.md) or [Steward Validator Preparation Guide v3](https://docs.google.com/document/d/18MNB7nEKerlcyZKof5AvGMy0GP9T82c4SWaxZkPzya4).
   Normally this involves starting the indy-node-service with `sudo systemctl start indy-node`.
   For testing on one machine we will use the `start_indy_node` command.
     > The method of starting nodes with the `start_indy_node` is for provisional (test) networks. The preferred method for production level networks is documented in the [Steward Validator Preparation Guide v3](https://docs.google.com/document/d/18MNB7nEKerlcyZKof5AvGMy0GP9T82c4SWaxZkPzya4).
     However, since, for the purposes of the demo, the nodes are all running on the same machine you sort of have to do it this way.
    
   2. Validate the Nodes with the `validator-info` script.

## Where to go from here?
The network can be hardened by configuring [AUTH-RULES](https://docs.google.com/document/d/1xk0A5FljKOZ2Fazri6J5mAfnYWXdOMl2LwrFK16MJIY/edit) and [TransactionAuthorAgreements](https://github.com/hyperledger/indy-plenum/blob/master/docs/source/transaction_author_agreement.md)

## Hands On Walkthrough

An example Walkthrough of the above mentioned steps can be found in the `sample/Network` [folder](../../../sample/Network/README.md).