# Quick start - Getting started with your first Distrobox container on Linux

This guide helps you get started with Distrobox - a powerful tool that creates containerized sandboxes tightly integrated with your host system. Think of it as a lightweight, disposable development environment that feels native on your Linux machine.

> **Audience:** Linux users who want lightweight, disposable development environments without virtual machines.
> **Use Case:** create and manage containerized sandboxes that integrate seamlessly with your host system.
> **Prerequisites:** Linux (Ubuntu, Fedora, Arch, or similar), Podman or Docker installed, and `sudo` access.
> **Last Updated:** this guide was verified in August 2026 with Distrobox 1.8.1.2 and Podman 5.4.2.

---

## Overview

In this guide, you'll learn to:
- Install Distrobox and its dependencies
- Create your first container
- Enter and use the container
- Exit and manage containers

Time to complete: ~10 minutes (plus initial setup time)

---

## Prerequisites

Before you begin, make sure you have:

- Linux (any distribution—Ubuntu, Fedora, Arch, etc.)
- Podman or Docker installed on your system
- A user account with sudo privileges

> **Tip:** Distrobox works with both Podman and Docker. If you don't have either, install Podman first. Podman is preferred for rootless containers on Linux.

---

## Install Distrobox

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

## Create your first container

Next, create a container using a common base image, such as Ubuntu:

```bash
distrobox-create --name my-devbox --image ubuntu:latest
```

This command:
- Creates a container named `my-devbox`
- Uses the latest Ubuntu image as the base
- This first download **can take several minutes** depending on your internet speed

> **Tip:** if you prefer Fedora or Arch Linux, replace `ubuntu:latest` with `fedora:latest` or `archlinux:latest`. Check the [official Distrobox docs](https://github.com/89luca89/distrobox) for the full list of supported base images.

---

## Enter your container

Once the image is downloaded and the container is created, enter it:

> **Note:** the first time you enter a newly created container, Distrobox runs a one-time setup script that may take a few minutes. Subsequent entries still show progress output but complete in seconds.

```bash
distrobox-enter my-devbox
```

Your terminal prompt may change, indicating you're now inside the container. You may also see the container name in your prompt, like `user@my-devbox:/$`. If not, you can check in the next step.

> **Important:** inside the container, your home directory is automatically mounted and shared with your host system. Files you create here appear on your host, and vice versa.

---

## Verify everything works

Inside the container, check that it's working properly:

```bash
# Check the container's distribution
cat /etc/os-release

# Check that your home directory is synced
ls ~
```

`ls ~` shows your host’s home directory contents because Distrobox shares it by default. If you see your usual files, the mount is working.

Now open a new terminal on your host machine and list out your containers:

```bash
# Verify the container is running and visible from the host
distrobox list
```

---

## Exit and manage your container

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

## Next steps

Now that you have a working container, you can:

- Install development tools inside the container (Node.js, Python, Go, etc.)
- Create multiple containers for different projects or distributions
- Export apps so they appear in your system app menu

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
