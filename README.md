# etlfunnel-execution

ETLFunnel execution engine. The Docker image runs `dfshell`, a server that takes JSON requests and sends JSON events over a WebSocket.

**Latest release: [v1.2.2](../../releases/tag/v1.2.2)** — the packages for both architectures (images, docs, examples, checksums, install guides) are attached to that one release.

## Download

- **One zip per architecture:** `etlfunnel-execution-linux-amd64.zip` (Intel/AMD) or `etlfunnel-execution-linux-arm64.zip` (Apple silicon, Graviton).
- `SHA256SUMS.txt` has the checksum of both zips.

Each architecture package contains the image, the documentation bundle (protocol, connectors, hooks, runnable `examples/`), a checksum file and `INSTALL-<arch>.md`. The docs are also inside the image at `/opt/execution/docs`.

## Quick start (linux/amd64; use `arm64` on ARM hosts)

```bash
grep amd64 SHA256SUMS.txt | shasum -a 256 -c                      # use sha256sum -c on Linux
unzip etlfunnel-execution-linux-amd64.zip
shasum -a 256 -c etlfunnel-execution-1.2.2-linux-amd64.sha256   # use sha256sum -c on Linux
gunzip -c etlfunnel-execution-1.2.2-linux-amd64.image.tar.gz | docker load
docker run -d --name etlfunnel-execution -p 8080:8080 \
  etlfunnel-execution:1.2.2-amd64 -listen 0.0.0.0:8080
curl http://localhost:8080/healthz
```

Full instructions are in `INSTALL-<arch>.md` inside each package.

## Security

The server has **no authentication**. Publish the port to a private network only.
