# Deploying a stack
```bash
# Create the virtual machines
docker-machine create --driver virtualbox myvm1
docker-machine create --driver virtualbox myvm1

# list machines
docker-machine ls

# initialize the swarm from a vm
docker-machine ssh myvm1 "docker swarm init --advertise-addr <myvm1 ip>

# Add a worker
docker-machine ssh myvm2 "docker swarm join --token <token> <myvm1 ip>:<port>

# Viewing nodes inside the swarm
docker-machine ssh myvm1 "docker node ls"

# Leaving a swarm
docker swarm leave

# To be able to run local files remotely on the vm
docker-machine env myvm1
eval $(docker-machine env myvm1)

# Verify myvm1 is the active machine
docker-machine ls

# Deploying
docker stack deploy -c docker-compose.yml getstartedlab

# Verify its working
docker stack ps getstartedlab
```

You can visit the stack by finding the ip address and going to:
<ip address> in your browser url bar

```bash
# Tearing down a stack
docker stack rm getstartedlab

# Leaving a swarm
docker-machine ssh myvm2 "docker swarm leave"

# --force required because it is the swarm leader
docker-machine ssh myvm1 "docker swarm leave --force"

# Unsetting the shell variable settings
eval $(docker-machine env -u)

# Restarting a machine
docker-machine start <vm name>
```
