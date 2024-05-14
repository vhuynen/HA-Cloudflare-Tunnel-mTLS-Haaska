# HA-Cloudflare-Tunnel-mTLS-Haaska
This post explains why I gave up the Tailscale tunnel and opted for the mTLS Cloudflare tunnel to expose Home Assistant’s API to Haaska.

- [HA-Cloudflare-Tunnel-mTLS-Haaska](#ha-cloudflare-tunnel-mtls-haaska)
  - [Architecture](#architecture)


## Architecture

![architecture](./docs/Architecture-Cloudflared%20Tunnel.png)
```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```
