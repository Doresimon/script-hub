# v2ray

- [link](https://www.v2fly.org/)

## usage

```bash
# install
curl -O https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh && sudo bash install-release.sh

# config path
cat /usr/local/etc/v2ray/config.json

# copy config
sudo cp ./config.json /usr/local/etc/v2ray/config.json 

# restart
sudo systemctl restart v2ray 
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
