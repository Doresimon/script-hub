# v2ray

- [link](https://www.v2fly.org/)

## usage

```bash

```

## config

```json
{
  "inbounds": [
    {
      "port": 10086,
      "protocol": "vmess",
      "settings": {
        "clients": [
          {
            "id": "$uuid",
            "level": 1,
            "alterId": 64
          }
        ]
      }
    },
    {
      "port": 10087,
      "protocol": "vmess",
      "settings": {
        "clients": [
          {
            "id": "$uuid",
            "level": 1,
            "alterId": 64
          }
        ]
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "freedom",
      "settings": {}
    },
    {
      "protocol": "blackhole",
      "settings": {},
      "tag": "blocked"
    }
  ]
}
```
