# Docker Volumes 

*Docker Volumes* ensure data remains safe even if a container creashes / recreated 

1. Creating a volume : 
<code>
docker volume create <volume_name>
</code>

2. Inspecting a Volume : 
<code>
docker volume inspect <volume_name>
</code>

3. Attaching a Volume to a Container : 
<code>
docker run -v <volume_name>:<container_path> <image_name>
</code>

**can either use -v or --mount**

4. Read-Only Volumes : 
<code>
docker run -v <volume_name>:<container_path>:ro <image_name>
</code>

# Docker Networking

**IP Address**
- Unique identifier for a device/container in a network
- Each container gets an IP inside its Docker network

**Subnet & CIDR**

- Subnet = smaller network carved from a larger one
- CIDR format: IP/prefix

- Example:

`192.168.10.0/24
`

8 host bits → 2^8 = 256 IPs

**Network ID & Broadcast ID**

- Network ID → first IP (identifies network)
- Broadcast ID → last IP (send to all hosts)

### Docker Bridge Networking

**docker0 (Default Bridge)**
- Created automatically when Docker installs
- Acts like a virtual switch
- All containers connect via eth0

**veh Pair**

- Virtual Ethernet cable
- One end in container (eth0)
- Other end in docker0

### Commands 

- **`docker run -d nginx`** : Default Bridge , Runs inside docker0
- **`docker network create my_bridge`** : Creates custom bridge network
- **`docker network create \
  --subnet 192.168.10.0/24 \
  --gateway 192.168.10.1 \
  my_bridge`** : Create Bridge with Subnet & Gateway
- **`docker run -d --network my_bridge nginx`** : Run container on custom network 
- **`docker network inspect my_bridge`** : Check network details 