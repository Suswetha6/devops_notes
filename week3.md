# Docker – Command & Dockerfile Notes

## 1. Docker CLI Commands

### Container Lifecycle

- **`docker run`** - Creates and starts a new container from an image.

```bash
docker run -it ubuntu 
```

- **`docker stop`** - Gracefully stops a running container.
- **`docker exec`** - Executes a command inside a running container.

```bash
docker exec -it <container_id> 
```

### Cleanup & Maintenance

- **`docker container prune`** - Deletes all stopped containers to free space.

### Authentication

- **`docker login`** - Authenticates to Docker Hub or another registry.

## 2. Dockerfile Instructions

### Core Instructions

- **`FROM`** - Specifies the base image for the Dockerfile.
- **`RUN`** - Executes commands at build time, creating a new image layer.
- **`CMD`** - Defines the default command when a container starts (can be overridden at runtime).
- **`ENTRYPOINT`** - Makes the container behave like an executable (harder to override than `CMD`).

### File & Environment Handling

- **`COPY`** - Copies files from the host into the image.
- **`ADD`** - Like `COPY`, but also supports URLs and auto-extracts archives (use sparingly).
- **`ENV`** - Sets environment variables inside the image.

### Networking

- **`EXPOSE`** - Documents which ports the container listens on (does not publish the port).
- **Port Mapping (`-p`)** - Forwards host ports to container ports.

```bash
docker run -p 8080:80 nginx
```

## 3. Image Internals & Optimization Concepts

### Docker Image Layers

- Each Dockerfile instruction creates a new immutable layer.
- More layers = larger images & slower builds.

### Copy-on-Write (COW)

- Docker uses COW filesystem:
  - Image layers are read-only
  - Container layer is writable
- Saves disk space and improves efficiency.

### Multi-Stage Builds

- Use multiple `FROM` statements in one Dockerfile.
- Keeps only required artifacts in the final image.
- Reduces image size significantly.

### Dockerfile Best Practices

- Combine commands to reduce layers.
- Place frequently changing commands at the bottom.
- Use multi-stage builds for production images.
- Prefer `COPY` over `ADD` unless extra features are needed.
- Use lightweight base images (e.g., `alpine`).

## 4. Inspection & Debugging

- **Image Inspection**

```bash
docker image inspect <image_id>
```

- Useful for checking:
  - Layers
  - Environment variables
  - Entrypoint / CMD
  - Exposed ports

## 5. How Containers Work (Kernel Concepts)

### Linux Namespaces (Isolation)

Each container gets isolated views of:
- **PID namespace** – process IDs  
- **UTS namespace** – hostname  
- **NET namespace** – network stack  
- **USER namespace** – user IDs  
- **IPC namespace** – inter-process communication  
- **MNT namespace** – filesystem mounts  


### Control Groups (cgroups)

- Limit and manage:
  - CPU usage
  - Memory usage
  - Disk I/O
- Prevent one container from starving others.



## 6. Docker and the OS Kernel

- **Linux**
  - Docker runs natively.
  - Uses host Linux kernel directly.

- **Windows / macOS**
  - Docker runs inside a lightweight Linux VM.
  - Required because Docker depends on Linux kernel features.



## 7. Running Containers on Different Systems

- **Linux**  
  Native container execution (best performance).

- **Windows / macOS**  
  Containers run via a Linux VM abstraction.



## 8. Need for Volumes 

- **Ephemeral Containers**
  - Can be created, stopped, and destroyed easily.
  - Container filesystem is temporary.

- **Implication**
  - Applications should be **stateless**.
  - Persistent data should be stored using **volumes** or external services.
