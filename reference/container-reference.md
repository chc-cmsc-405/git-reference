# Container Reference Guide

A quick reference for understanding containers and Dockerfiles.

---

## What Are Containers?

A **container** packages an application with everything it needs to run: code, runtime, libraries, and configuration. Containers are isolated from each other and from the host system.

### Containers vs. Virtual Machines

| Aspect | Container | Virtual Machine |
|--------|-----------|-----------------|
| Size | Megabytes | Gigabytes |
| Startup | Seconds | Minutes |
| OS | Shares host kernel | Full guest OS |
| Isolation | Process-level | Hardware-level |

### Why Containers Matter

- **Consistency**: "Works on my machine" becomes "works everywhere"
- **Portability**: Run the same container on laptop, server, or cloud
- **Efficiency**: Lightweight, fast startup, minimal resource usage
- **Scalability**: Easy to run multiple instances

---

## Docker Basics

**Docker** is the most popular container platform. Key concepts:

| Term | Definition |
|------|------------|
| **Image** | A read-only template with instructions for creating a container (like a class) |
| **Container** | A running instance of an image (like an object) |
| **Dockerfile** | A text file with instructions to build an image |
| **Registry** | A repository for storing and sharing images (e.g., Docker Hub) |

### Common Docker Commands

```bash
# Build an image from a Dockerfile
docker build -t my-app .

# Run a container from an image
docker run my-app

# Run with environment variables
docker run -e APP_NAME=Test my-app

# List running containers
docker ps

# List all images
docker images

# Stop a container
docker stop <container-id>
```

---

## Dockerfile Syntax

A Dockerfile contains instructions to build an image. Each instruction creates a **layer**.

### Essential Instructions

| Instruction | Purpose | Example |
|-------------|---------|---------|
| `FROM` | Base image to start from | `FROM alpine:latest` |
| `WORKDIR` | Set working directory | `WORKDIR /app` |
| `COPY` | Copy files into image | `COPY main.go .` |
| `RUN` | Execute a command during build | `RUN go build -o main .` |
| `ENV` | Set environment variable | `ENV APP_NAME=MyApp` |
| `EXPOSE` | Document which port the app uses | `EXPOSE 8080` |
| `CMD` | Default command when container runs | `CMD ["./main"]` |

### Simple Dockerfile Example

```dockerfile
# Start from a base image
FROM python:3.11-slim

# Set the working directory
WORKDIR /app

# Copy application files
COPY app.py .

# Install dependencies
RUN pip install flask

# Expose the port
EXPOSE 5000

# Run the application
CMD ["python", "app.py"]
```

---

## Multi-Stage Builds

Multi-stage builds create smaller, more secure images by separating build-time dependencies from runtime.

### Why Multi-Stage?

| Stage | Contains | Needed at Runtime? |
|-------|----------|-------------------|
| Build | Compilers, SDKs, source code | No |
| Runtime | Application binary, minimal OS | Yes |

### Multi-Stage Example (Go)

```dockerfile
# Stage 1: Build
FROM golang:1.21-alpine AS build
WORKDIR /app
COPY . .
RUN go build -o main .

# Stage 2: Runtime
FROM alpine:latest
COPY --from=build /app/main /main
CMD ["/main"]
```

**Result**: Final image contains only the binary (~10-20 MB) instead of the full Go SDK (~300+ MB).

### The `--from` Flag

`COPY --from=build` copies files from a previous stage:
- `--from=build` references the stage named "build" (via `AS build`)
- `--from=0` references the first stage by index

---

## Common Base Images

| Image | Size | Use Case |
|-------|------|----------|
| `alpine` | ~5 MB | Minimal Linux, great for production |
| `ubuntu` | ~75 MB | Full Linux, familiar environment |
| `debian:slim` | ~50 MB | Balance of size and compatibility |
| `scratch` | 0 MB | Empty image, for static binaries only |

### Language-Specific Images

| Image | Purpose |
|-------|---------|
| `golang:1.21-alpine` | Build Go applications |
| `python:3.11-slim` | Run Python applications |
| `node:20-alpine` | Run Node.js applications |
| `openjdk:21-slim` | Run Java applications |

---

## Environment Variables

Containers commonly use environment variables for configuration:

```dockerfile
# Set default in Dockerfile
ENV DATABASE_URL=localhost:5432

# Override when running
docker run -e DATABASE_URL=prod-db:5432 my-app
```

**Why environment variables?**
- Keep configuration separate from code
- Different values for dev/staging/production
- No secrets in source code

---

## Best Practices

1. **Use specific image tags**: `alpine:3.18` not `alpine:latest`
2. **Minimize layers**: Combine related RUN commands
3. **Order by change frequency**: Put rarely-changing instructions first (better caching)
4. **Use .dockerignore**: Exclude unnecessary files from build context
5. **Don't run as root**: Use `USER` instruction for security
6. **Use multi-stage builds**: Keep production images small

### Example .dockerignore

```
.git
.github
*.md
tests/
```

---

## Containers in CI/CD

CI/CD pipelines (like GitHub Actions) commonly:
1. Build a Docker image from source
2. Run tests inside a container
3. Push the image to a registry
4. Deploy the container to production

### GitHub Actions Example

```yaml
- name: Build Docker image
  run: docker build -t my-app .

- name: Run container
  run: docker run my-app
```

---

## Quick Reference

```dockerfile
# Minimal Dockerfile template
FROM <base-image>
WORKDIR /app
COPY . .
RUN <build-command>
CMD ["<run-command>"]
```

```bash
# Build and run
docker build -t my-app .
docker run my-app
```

---

## Resources

- [Docker Overview](https://docs.docker.com/get-started/overview/)
- [Dockerfile Reference](https://docs.docker.com/engine/reference/builder/)
- [Best Practices for Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
