# Docker Hands-on Lab 1: Basic Commands & httpd Image

**Session focus:** Exploring fundamental Docker commands and running a simple hands-on example using the official `httpd:latest` image from Docker Hub.

---

## Objectives
- Pull an image from Docker Hub
- Create and run a container with port mapping and detached mode
- Understand the `-p` and `-d` flags
- Commit container changes into a new image with a tag
- Clean up unused images

---

## 1. Pull the latest `httpd` image

We start by downloading the official Apache HTTP Server image from Docker Hub.

**Link:** [httpd:latest tags on Docker Hub](https://hub.docker.com/_/httpd/tags?name=latest)

![Docker Hub httpd page](https://github.com/user-attachments/assets/c1b4a4fe-045c-4acf-9421-35130340c306)

**Command:**
```bash
docker pull httpd:latest
```

![Pulling the image](https://github.com/user-attachments/assets/afceac99-c5dd-4bf4-b3ac-e5c5d4b5332d)

---

## 2 & 3. Create a container and explore `-p` and `-d`

When we create a new container we use two important flags:

| Flag | Name              | What it does |
|------|-------------------|--------------|
| `-d` | Detached mode     | Runs the container in the background. Your terminal stays free so you can continue working. Without `-d`, the terminal is locked to the container’s live logs. |
| `-p` | Port mapping      | Maps a port on your host machine to a port inside the container. Format: `host_port:container_port` |

**Command:**
```bash
docker run -d -p 8080:80 --name my-Apache-server httpd
```

- `-d` → run in the background  
- `-p 8080:80` → access the container’s port 80 through `http://localhost:8080` on your machine  
- `--name my-Apache-server` → give the container a friendly name  

![Running the container](https://github.com/user-attachments/assets/014c2bef-780c-4b86-9b83-77a37bc80fcb)

![Container running](https://github.com/user-attachments/assets/57514945-5a3e-438b-b850-29b9b56e6428)

---

## 4. Commit changes and tag the new image

After making changes inside the running container, we can save those changes as a new image. Tagging helps with versioning.

**Command:**
```bash
docker commit my-Apache-server my-apache-image:v1
```

![Committing the container](https://github.com/user-attachments/assets/49e60dc2-6ad8-4245-89c7-90890c4dc045)

> **Note:** `docker commit` creates a new image from the current state of a container. This is useful for quick experiments, but for production work you should prefer writing a `Dockerfile`.

---

## Bonus: Delete an image

If you need to remove an image:

```bash
docker rmi <image-id>
```

![Deleting an image](https://github.com/user-attachments/assets/d82675c6-5f30-4d49-84d3-06f467a2e623)

---

## Quick command summary

| Action                          | Command                                                      |
|---------------------------------|--------------------------------------------------------------|
| Pull image                      | `docker pull httpd:latest`                                   |
| Run container (detached + port) | `docker run -d -p 8080:80 --name my-Apache-server httpd`     |
| Commit container to image       | `docker commit my-Apache-server my-apache-image:v1`          |
| Remove image                    | `docker rmi <image-id>`                                      |

---

*End of Lab 1*
