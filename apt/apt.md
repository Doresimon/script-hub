# apt

## basic commands

- `apt`
  - `apt install $PKG`
  - `apt update`
  - `apt autoremove`
  - `apt upgrade`
- `apt-key`

## keys

```bash
export KEY_SERVER=keyserver.ubuntu.com
# export PUB_KEY=xxx
export PUB_KEY=648ACFD622F3D138
# [sudo]
apt-key adv --keyserver $KEY_SERVER --recv-keys $PUBKEY
```
