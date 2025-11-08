# Shell Scripting Basics

## 1. Hello World Script

**File:** `hello.sh`

```bash
#!/bin/bash
# This is a simple shell script that prints "Hello, World!" to the terminal

echo "Hello, World!"
```

## 2. Convert String to Uppercase

**File:** `uppercase.sh`
```bash
#!/bin/bash

read -p "Enter a string: " str
echo "Uppercase: ${str^^}"

```

## 3. Convert String to Lowercase
**File:** `lowercase.sh`
```bash
#!/bin/bash

read -p "Enter a string: " str
echo "Lowercase: ${str,,}"
```

## 4. User and group creation

```bash
  #!/bin/bash

  GROUP="devgroup"
  USER="devuser"

  # Create group
  groupadd $GROUP

  # Create user and add to group
  useradd -m -g $GROUP -s /bin/bash $USER

  # Add welcome message
  echo 'echo "Welcome to the system!"' >> /home/$USER/.bashrc

```

# Docker Basics & Containerization

**Docker** is a platform for building, shipping, and running applications using **containers**.

> **Philosophy:** *If it fits, it ships*  


### Container
- Lightweight, isolated runtime for an application  
- Includes code + runtime + dependencies  
- Shares the host OS kernel (unlike virtual machines)


### Image 
- Read-only template used to create containers
- Built from a Dockerfile
- Containers are running instances of images

## Docker Daemon
- Background service running on the host
- Manages containers, images, networks, and volumes
- Listens to Docker API requests

## Docker Client

- CLI tool used to interact with the Docker daemon
- Sends commands like run, build, pull
- **Command:**
  ```bash 
  docker <command>
  ```

## Common Docker Commands
- Run a Container
```bash 
docker run <image>
```
- Run Interactively
```bash
docker run -it <image> /bin/bash
```

` -i → interactive`

 `-t → terminal access`

- List Running Containers
```bash
docker ps
```
- List All Containers
```bash
docker ps -a
```
- Stop & Remove Containers
```bash
docker stop <container_id>
docker rm <container_id>
```