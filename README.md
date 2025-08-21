Perfect 🎯 — I get it now.
You want a **ready-to-use README.md** that your students can just follow step by step without guessing anything.
I’ll write it as if it’s **your project documentation** — clean, beginner-friendly, but still professional.

Here’s the **full guide**:

---

# 🚀 Running Phi-4 Mini Reasoning Model in Docker with Ollama

This guide will help you **set up, run, and test** the `phi4-mini-reasoning:3.8b-q8_0` model using **Docker + Ollama**.
No prior Docker knowledge is required — just follow the steps below. ✅

---

## 📦 Prerequisites

1. **Install Docker**

   * [Download Docker Desktop](https://www.docker.com/products/docker-desktop/) (Windows/macOS)
   * On Linux:

     ```bash
     sudo apt update
     sudo apt install docker.io -y
     ```

2. **Install Docker Compose**

   * Already included with Docker Desktop.
   * On Linux:

     ```bash
     sudo apt install docker-compose -y
     ```

3. **Check installation:**

   ```bash
   docker --version
   docker compose version
   ```

---

## 📁 Step 1: Project Setup

Create a folder for the project:

```bash
mkdir ollama-docker
cd ollama-docker
```

---

## 📝 Step 2: Create `Dockerfile`

Inside the folder, create a file called **`Dockerfile`**:

```dockerfile
# Use official Ollama base image
FROM ollama/ollama:latest

# Expose the Ollama API port
EXPOSE 11434

# Start Ollama server when the container runs
CMD ["serve"]
```

---

## 📝 Step 3: Create `docker-compose.yml`

In the same folder, create **`docker-compose.yml`**:

```yaml
version: "3.8"

services:
  ollama:
    image: ollama/ollama:latest
    container_name: ollama-phi4-mini
    ports:
      - "11434:11434"
    volumes:
      - ollama_models:/root/.ollama
    command: serve

volumes:
  ollama_models:
```

---

## ▶️ Step 4: Start the Container

From inside the project folder:

```bash
docker compose up -d
```

This will:

* Pull the Ollama Docker image
* Create a container named **`ollama-phi4-mini`**
* Run it in the background

Check if it’s running:

```bash
docker ps
```

You should see:

```
CONTAINER ID   NAME               PORTS
xxxxxxx        ollama-phi4-mini   0.0.0.0:11434->11434/tcp
```

---

## 📥 Step 5: Install the Phi-4 Mini Reasoning Model

Open a shell inside the container:

```bash
docker exec -it ollama-phi4-mini bash
```

Pull the model:

```bash
ollama pull phi4-mini-reasoning:3.8b-q8_0
```

Confirm it’s installed:

```bash
ollama list
```

You should see:

```
phi4-mini-reasoning:3.8b-q8_0
```

Exit the container:

```bash
exit
```

---

## 🧪 Step 6: Test the Model

Run this command **from your host machine**:

```bash
curl http://localhost:11434/api/generate -d '{
  "model": "phi4-mini-reasoning:3.8b-q8_0",
  "prompt": "Explain why the sun sets in the west."
}'
```

✅ You’ll get a JSON response with the model’s generated text.

---

## 📚 Summary

1. Install Docker + Docker Compose
2. Create `Dockerfile` and `docker-compose.yml`
3. Run container: `docker compose up -d`
4. Enter container and pull the model
5. Test with `curl`

---

## 🛑 Stopping the Container

To stop and remove the container:

```bash
docker compose down
```

---

## ⚡️ Advanced (Optional)

You can **limit CPU and RAM usage** by editing `docker-compose.yml`:

```yaml
deploy:
  resources:
    limits:
      cpus: "2.5"
      memory: 8g
    reservations:
      cpus: "1.0"
      memory: 4g
```

You can also enable **GPU support** (if you have NVIDIA):

```yaml
runtime: nvidia
environment:
  - NVIDIA_VISIBLE_DEVICES=0
```

---

# 🎯 That’s it!

You now have a **working Dockerized Ollama setup** with the **Phi-4 Mini Reasoning model** running locally and accessible via API.

---

👉 Do you want me to make this README file **ready-to-download** (`README.md`) so your students can just clone the repo and follow along?
