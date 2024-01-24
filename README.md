Implimenting a Customizable Load Balancer

   ![image](https://github.com/Tirthankar-Halder/dsAssignment/assets/64760892/f8df9a7b-1fe3-4dcf-8dfb-45c7c33e1a71)

# Design

This repository implements a loadbalancer system which uses Consistent Hashmaping technnique for the the allocation of servers and client requests simulteniously further it uses the concept of virtual server of better performence. 

We use Python as a programming language and<strong> Flask </strong>module for http endpoints for the interaction over the network.For the generation of asynchronous requests <strong>asyncio aiohttp </strong> libraries are used.


<ol type="1">
 <li><strong>Load-balancer</strong> is mainly responsible for accepting asynchronous http requests from client and distributes among the servers.</li>
 <li><strong>Consistent Hashmap </strong> Consistent hashing has a unique hashing structure that is circular instead of linear to avoid many shifts of data in
the event of the addition of resources to the system. Load Balancer uses consistent hashing to distribute client requests
evenly among the server instances (i.e., balancing the system load). Moreover, consistent hashing technique is also used in
distributed caching systems for better utilization of resources.</li><li><strong>Server</strong> has two endpoints "/home" endpoint returns a unique identifier to distinguish among the replicas and "/heartbeat" this endpoint sends heartbeat responses upon request. The load balancer further
uses the heartbeat endpoint to identify failures in the set of containers maintained by it.
</ol>

# Assumptions
+ For the server ids we have use six digit random numbers which servers the purpose of non cluster allocation of virtual servers.
+ For removing servers, if the no.of servers are more than the length of Hostname then random servers are chosen and removed.
+ For analisys part when servers are increasing, we put a 10 second halt.
+ Statistically, K = log (M) (K = no. of virtual server, M = no. of slots.) virtual servers work best to distribute the load across the
physical server instances equally.
+ In case of faliure of server, we have manually down the server.



# Challenges

+ Sending the request to the load-balancer and tracking the server load was quite challenging.
+ However we have noticed that a large number of server container allocation might affect the performence of the system.
+ In real case scenario servers may get down for various reasons but in our case servers are running on docker container it is challenging to down them automatically. 





# Prerequisites

### 1. Docker: latest [version 20.10.23, build 7155243]

    sudo apt-get update

    sudo apt-get install \
        ca-certificates \
        curl \
        gnupg \
        lsb-release

    sudo mkdir -p /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

    echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

    sudo apt-get update

    sudo apt-get install docker-ce docker-ce-cli containerd.io

### 2. Docker-compose standalone [version v2.15.1]
    sudo curl -SL https://github.com/docker/compose/releases/download/v2.15.1/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
    
    sudo chmod +x /usr/local/bin/docker-compose
    
    sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose


 # Testing
 
Test results are as follows:
 
<p align="center">
      <img src="AnalysisServerRemove.jpg" width="70%"/>
</p>
