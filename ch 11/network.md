# Bridge network
**Create a new network named localnet with bridge**  
`$ docker network create -d bridge localnet`  

**Run 2 containers and ping 1 from another 1**  
`$ docker container run -d --name c1 --network localnet alpine sleep 1d`  
`$ docker container run -it --name c2 --network localnet alpine sh`  
`$ pint c1`  
  
**mapping docker port to host port**  
**run a new nginx web service container map docker 80 port to host 5000 port**  
`$ docker container run -d --name web --network localnet --publish 5000:80 nginx`  
**confirm the mapping, now run localhost:5000 should see ngix portal. But 5000 port cannot be used by other container**  
`$ docker port web`  

# Overlay network  
**idiealy communication method between containers, support containers communication on different docker host**  
`$ docker network create -d overlay --name <overlay network name>`    
  
# Macvlan in linux or Transparent in windows  
`$ docker network create -d macvlan \`  
` --subnet <sub vlan ip/port> \`  
` --ip-range=<the ip could assign to this macvlan> \`  
` --gateway=<gateway ip> \`  
` -o parent=eth0.<vlan id> \`  
` <macvlan name>`

