# HA-Cloudflare-Tunnel-mTLS-Haaska
This post explains why I gave up the Tailscale tunnel and opted for the mTLS Cloudflare tunnel to expose Home Assistant’s API to Haaska.

## Table of Contents
- [HA-Cloudflare-Tunnel-mTLS-Haaska](#ha-cloudflare-tunnel-mtls-haaska)
  - [Table of Contents](#table-of-contents)
  - [Architecture](#architecture)
  - [Settings](#settings)
    - [Domain Name](#domain-name)
    - [Cloudflare](#cloudflare)
    - [Home Assistant](#home-assistant)


## Architecture

![architecture](./docs/Architecture-Cloudflared%20Tunnel.png)

Instead of opening my router to the Internet to allow my Haaska Lambda to reach my Home Assistant, I have protected my Home Assistant over the Internet with a third-party service, Cloudflare.
Cloudflare provides an excellent tool that initiates a secure connection from your Home Assistant instance to Cloudflare’s global network. A daemon agent named cloudflared, installed and running from Home Assistant, establishes an authenticated secure communication with your Cloudflare tenant.
On the Cloudflare side, we use the WAF (Web Application Firewall) to protect your endpoint from unexpected Internet traffic.
Two rules have been implemented to reduce the attack surface:
- First, a rule that accepts only requests from AWS’s Data Centers. In Europe, the Alexa Voice Service is hosted in Ireland.
- Second, a rule that accepts only mTLS requests from a well-know client. In our case, the WAF accepts only TLS connections established with a trusted client certificate provided by the Lambda function.
- On the Haaska side, the Lambda is set to establish an mTLS two-way communication with a trusted client certificate provided and accepted by Cloudflare.
  
Right now, we have a nice explanation of what this architecture does. We are going to describe in detail all the steps we need to take to protect your Home Assistant from the Internet.

## Settings

### Domain Name

First, if you don’t have your own domain name, you will need to buy one from your preferred registrar. In my case, I opted to buy a cheaper domain with the .ovh extension from ovh.com. The domain name doesn’t matter; my goal is to reach my Home Assistant instance from my Lambda Haaska over the Internet without opening my router to the Internet.

### Cloudflare 

### Home Assistant

