# Quick Start: Getting Started With Your First Distrobox Container on Linux

This guide will help you get started with Distrobox - a powerful tool that creates containerized sandboxes tightly integrated with your host system. Think of it as a lightweight, disposable development environment that feels native on your Linux machine.

---

## Overview

In this guide, you'll learn to:
- Install Distrobox and its dependencies
- Create your first container
- Enter and use the container
- Exit and manage containers

**Time to complete:** ~10 minutes (plus initial setup time)

---

## Prerequisites

Before you begin, make sure you have:

- **Linux** (any distribution—Ubuntu, Fedora, Arch, etc.)
- **Podman or Docker** installed on your system
- A user account with **sudo** privileges

> **Tip:** Distrobox works with both Podman and Docker. If you don't have either, install Podman first. Podman is preferred for rootless containers on Linux.

---

## Step 1: Install Distrobox

Open your terminal and run the following command depending on your distribution:

```bash
# For Ubuntu/Debian users:
sudo apt update && sudo apt install podman distrobox -y

# For Fedora users:
sudo dnf install podman distrobox

# For Arch Linux users:
sudo pacman -S podman distrobox
```

---

## Step 2: Create Your First Container

Now it's time to create a container. We'll use a common base image, such as Ubuntu:

```bash
distrobox-create --name my-devbox --image ubuntu:latest
```

This command:
- Creates a container named `my-devbox`
- Uses the latest Ubuntu image as the base
- This first download **will take several minutes** depending on your internet speed

> **Tip:** Prefer Fedora or Arch Linux? Replace `ubuntu:latest` with `fedora:latest` or `archlinux:latest`. Check the [official Distrobox docs](https://github.com/89luca89/distrobox) for the full list of supported base images.

---

## Step 3: Enter Your Container

Once the image is downloaded and the container is created, enter it:

> **Note:** The first time you enter a newly created container, Distrobox runs a one-time setup script that may take a few minutes. Subsequent entries will still show progress output but complete in seconds.

```bash
distrobox-enter my-devbox
```

Your terminal prompt may change, indicating you're now inside the container. You'll may also see the container name in your prompt, like `user@my-devbox:/$`. If not, you can check in the next step.

> **Important:** Inside the container, your home directory is automatically mounted and shared with your host system. Files you create here appear on your host, and vice versa.

---

## Step 4: Verify Everything Works

Inside the container, check that it's working properly:

```bash
# Check the container's distribution
cat /etc/os-release

# Check that your home directory is synced
ls ~
```
> **Note:** `ls ~` will show your host’s home directory contents because Distrobox shares it by default. If you see your usual files, the mount is working.

Now open a new terminal on your host machine and list out your containers:

```bash
# Verify the container is running and visible from the host
distrobox list
```

---

## Step 5: Exit and Manage Your Container

To exit the container and return to your host, go back to the terminal with your container running and enter:

```bash
exit
```

You're now back on your host system.

### Useful management commands:

| Command | What it does |
|---------|--------------|
| `distrobox list` | List all your containers |
| `distrobox stop my-devbox` | Stop the container |
| `distrobox rm my-devbox` | Remove the container completely |

---

## Next Steps

Now that you have a working container, you can:

- **Install development tools** inside the container (Node.js, Python, Go, etc.)
- **Create multiple containers** for different projects or distributions
- **Export applications** so they appear in your system application menu
- **Learn about `distrobox-init`** to customize your container environment

---

## Troubleshooting

| Issue | Possible solution |
|-------|-------------------|
| Container creation fails | Check that Docker or Podman is running (`systemctl status podman`) |
| Can't install packages | Ensure you have network connectivity inside the container |
| Performance is slow | Consider using a lighter base image like `alpine:latest` |

---

## Summary

You've successfully:
- Installed Distrobox on your Linux system
- Created your first container
- Entered and explored the container environment
- Learned basic container management commands

Your new container is ready for development, testing, or exploring different Linux distributions without affecting your host system.
