{
  "dns": {
    "hosts": {
      "geosite:category-ads-all": "127.0.0.1",
      "domain:googleapis.cn": "googleapis.com",
      "dns.pub": [
        "1.12.12.12",
        "120.53.53.53"
      ],
      "dns.alidns.com": [
        "223.5.5.5",
        "223.6.6.6",
        "2400:3200::1",
        "2400:3200:baba::1"
      ],
      "one.one.one.one": [
        "1.1.1.1",
        "1.0.0.1",
        "2606:4700:4700::1111",
        "2606:4700:4700::1001"
      ],
      "dns.google": [
        "8.8.8.8",
        "8.8.4.4",
        "2001:4860:4860::8888",
        "2001:4860:4860::8844"
      ]
    },
    "servers": [
      "1.1.1.1",
      {
        "address": "1.1.1.1",
        "domains": [
          "domain:googleapis.cn",
          "domain:gstatic.com"
        ],
        "port": 53
      },
      {
        "address": "223.5.5.5",
        "domains": [
          "domain:dns.alidns.com",
          "domain:doh.pub",
          "domain:dot.pub",
          "domain:doh.360.cn",
          "domain:dot.360.cn",
          "geosite:cn",
          "geosite:geolocation-cn"
        ],
        "expectIPs": [
          "geoip:cn"
        ],
        "port": 53
      }
    ]
  },
  "inbounds": [
    {
      "listen": "127.0.0.1",
      "port": 10808,
      "protocol": "socks",
      "settings": {
        "auth": "noauth",
        "udp": true,
        "userLevel": 8
      },
      "sniffing": {
        "destOverride": [
          "http",
          "tls"
        ],
        "enabled": true,
        "routeOnly": false
      },
      "tag": "socks"
    },
    {
      "listen": "127.0.0.1",
      "port": 10809,
      "protocol": "http",
      "settings": {
        "userLevel": 8
      },
      "tag": "http"
    }
  ],
  "log": {
    "loglevel": "warning"
  },
  "outbounds": [
    {
      "mux": {
        "concurrency": -1,
        "enabled": false,
        "xudpConcurrency": 8,
        "xudpProxyUDP443": ""
      },
      "protocol": "vmess",
      "settings": {
        "vnext": [
          {
            "address": "quiz.vidio.com",
            "port": 443,
            "users": [
              {
                "alterId": 0,
                "encryption": "",
                "flow": "",
                "id": "53f64488-9aa0-4125-bc74-2c3d439e0c31",
                "level": 8,
                "security": "auto"
              }
            ]
          }
        ]
      },
      "streamSettings": {
        "network": "ws",
        "security": "tls",
        "tlsSettings": {
          "allowInsecure": true,
          "fingerprint": "",
          "publicKey": "",
          "serverName": "sgo-viprext.my.id",
          "shortId": "",
          "show": false,
          "spiderX": ""
        },
        "wsSettings": {
          "headers": {
            "Host": "sgo-viprext.my.id"
          },
          "path": "/vmess"
        }
      },
      "tag": "proxy"
    },
    {
      "protocol": "freedom",
      "settings": {
        "domainStrategy": "UseIP"
      },
      "tag": "direct"
    },
    {
      "protocol": "blackhole",
      "settings": {
        "response": {
          "type": "http"
        }
      },
      "tag": "block"
    }
  ],
  "remarks": "ajat_17988_hidessh",
  "routing": {
    "domainStrategy": "IPIfNonMatch",
    "rules": [
      {
        "ip": [
          "1.1.1.1"
        ],
        "outboundTag": "proxy",
        "port": "53",
        "type": "field"
      },
      {
        "ip": [
          "223.5.5.5"
        ],
        "outboundTag": "direct",
        "port": "53",
        "type": "field"
      },
      {
        "domain": [
          "domain:googleapis.cn",
          "domain:gstatic.com"
        ],
        "outboundTag": "proxy",
        "type": "field"
      },
      {
        "network": "udp",
        "outboundTag": "block",
        "port": "443",
        "type": "field"
      },
      {
        "domain": [
          "geosite:category-ads-all"
        ],
        "outboundTag": "block",
        "type": "field"
      },
      {
        "ip": [
          "geoip:private"
        ],
        "outboundTag": "direct",
        "type": "field"
      },
      {
        "domain": [
          "geosite:private"
        ],
        "outboundTag": "direct",
        "type": "field"
      },
      {
        "ip": [
          "223.5.5.5/32",
          "223.6.6.6/32",
          "2400:3200::1/128",
          "2400:3200:baba::1/128",
          "119.29.29.29/32",
          "1.12.12.12/32",
          "120.53.53.53/32",
          "2402:4e00::/128",
          "2402:4e00:1::/128",
          "180.76.76.76/32",
          "2400:da00::6666/128",
          "114.114.114.114/32",
          "114.114.115.115/32",
          "180.184.1.1/32",
          "180.184.2.2/32",
          "101.226.4.6/32",
          "218.30.118.6/32",
          "123.125.81.6/32",
          "140.207.198.6/32",
          "geoip:cn"
        ],
        "outboundTag": "direct",
        "type": "field"
      },
      {
        "domain": [
          "domain:dns.alidns.com",
          "domain:doh.pub",
          "domain:dot.pub",
          "domain:doh.360.cn",
          "domain:dot.360.cn",
          "geosite:cn",
          "geosite:geolocation-cn"
        ],
        "outboundTag": "direct",
        "type": "field"
      },
      {
        "outboundTag": "proxy",
        "port": "0-65535",
        "type": "field"
      }
    ]
  }
}
