# RTSP Feed Setup

### 1. Build RTSP Feed Container

```bash
./build.sh
```

---

### 2. Run the RTSP feed container in the background

```bash
./run-feed.sh <STREAM_ENDPOINT> <SOURCE_PATH>
```

**Examples:**

* Using a Google Storage URL:

```bash
./run-feed.sh BAI_STREAM_02 gs://path-to-google-storage-url
```

* Using a local file:

```bash
./run-feed.sh BAI_STREAM_02 /path/to/local/file
```

* Using a local directory:

```bash
./run-feed.sh BAI_STREAM_02 /path/to/local/dir
```

* After running, the RTSP stream will be available at:

```
rtsp://<HOST_IP>:<RTSP_PORT>/<STREAM_ENDPOINT>
```

You can check your host IP in the script output or run:

```bash
ip route get 8.8.8.8 | tr -s ' ' | cut -d' ' -f7
```

> **Note:** The RTSP server currently supports both **TCP and UDP** connections.

---

### 3. Debug / Check if the stream is running

Use `ffplay` to play the stream:

```bash
ffplay rtsp://<HOST_IP>:<RTSP_PORT>/<STREAM_ENDPOINT>
```

This will open a window and play the live RTSP stream.

---

### 4. Stop the containers

```bash
docker compose down
```

Run this from the same directory as `docker-compose.yml`.

---

### 5. Reuse on another system

* Copy the `docker-compose.yml` and `run-feed.sh` script to another machine.
* Set the `.env` variables or use the script arguments.
* You can run the stream **without rebuilding the container**.

---

### 6. Notes

* **RTSP Server Image:** Switched from `aler9/rtsp-simple-server` to `bluenviron/mediamtx`.
* **Docker Command:** We now use `docker compose` instead of `docker-compose`.

  * It is part of the modern Docker CLI, no separate installation required.
  * Fully supported and maintained, avoiding deprecation warnings.
  * Behaves the same as the old command but integrates better with Docker CLI commands.

---
