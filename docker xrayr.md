###  docker安装
在root目录下创建配置文件，并用下面的命令启动
```  
touch config.yml
```

```
docker pull ghcr.io/xrayr-project/xrayr:latest && docker run --restart=always --name xrayr -d -v /config.yml:/etc/XrayR/config.yml --network=host ghcr.io/xrayr-project/xrayr:latest
```



[配置文件教程地址](https://xrayr-project.github.io/XrayR-doc/xrayr-pei-zhi-wen-jian-shuo-ming/config.html)




###  脚本安装：
```
bash <(curl -Ls https://raw.githubusercontent.com/XrayR-project/XrayR-release/master/install.sh)
```

配置文件路径： `/etc/XrayR`



```
Log:
  Level: warning # Log level: none, error, warning, info, debug 
  AccessPath: # /etc/XrayR/access.Log
  ErrorPath: # /etc/XrayR/error.log
DnsConfigPath: # /etc/XrayR/dns.json # Path to dns config, check https://xtls.github.io/config/dns.html for help
RouteConfigPath: # /etc/XrayR/route.json # Path to route config, check https://xtls.github.io/config/routing.html for help
InboundConfigPath: # /etc/XrayR/custom_inbound.json # Path to custom inbound config, check https://xtls.github.io/config/inbound.html for help
OutboundConfigPath: # /etc/XrayR/custom_outbound.json # Path to custom outbound config, check https://xtls.github.io/config/outbound.html for help
ConnectionConfig:
  Handshake: 4 # Handshake time limit, Second
  ConnIdle: 30 # Connection idle time limit, Second
  UplinkOnly: 2 # Time limit when the connection downstream is closed, Second
  DownlinkOnly: 4 # Time limit when the connection is closed after the uplink is closed, Second
  BufferSize: 64 # The internal cache size of each connection, kB
Nodes:
  - PanelType: "NewV2board" # Panel type: SSpanel, NewV2board, PMpanel, Proxypanel, V2RaySocks, GoV2Panel
    ApiConfig:
      ApiHost: "https://wangdazhuang.top"
      ApiKey: "6xks9dmz5x11111"
      NodeID: 3
      NodeType: V2ray # Node type: V2ray, Shadowsocks, Trojan, Shadowsocks-Plugin
      Timeout: 30 # Timeout for the api request
      EnableVless: false # Enable Vless for V2ray Type
      VlessFlow: "" # Only support vless
      SpeedLimit: 0 # Mbps, Local settings will replace remote settings, 0 means disable
      DeviceLimit: 0 # Local settings will replace remote settings, 0 means disable
      RuleListPath: # /etc/XrayR/rulelist Path to local rulelist file
      DisableCustomConfig: false # disable custom config for sspanel
    ControllerConfig:
      ListenIP: 0.0.0.0 # IP address you want to listen
      SendIP: 0.0.0.0 # IP address you want to send pacakage
      UpdatePeriodic: 60 # Time to update the nodeinfo, how many sec.
      EnableDNS: false # Use custom DNS config, Please ensure that you set the dns.json well
      DNSType: AsIs # AsIs, UseIP, UseIPv4, UseIPv6, DNS strategy
      EnableProxyProtocol: false # Only works for WebSocket and TCP
      AutoSpeedLimitConfig:
        Limit: 0 # Warned speed. Set to 0 to disable AutoSpeedLimit (mbps)
        WarnTimes: 0 # After (WarnTimes) consecutive warnings, the user will be limited. Set to 0 to punish overspeed user immediately.
        LimitSpeed: 0 # The speedlimit of a limited user (unit: mbps)
        LimitDuration: 0 # How many minutes will the limiting last (unit: minute)
      GlobalDeviceLimitConfig:
        Enable: false # Enable the global device limit of a user
        RedisAddr: 127.0.0.1:6379 # The redis server address
        RedisPassword: YOUR PASSWORD # Redis password
        RedisDB: 0 # Redis DB
        Timeout: 5 # Timeout for redis request
        Expiry: 60 # Expiry time (second)
      EnableFallback: false # Only support for Trojan and Vless
      FallBackConfigs:  # Support multiple fallbacks
        - SNI: # TLS SNI(Server Name Indication), Empty for any
          Alpn: # Alpn, Empty for any
          Path: # HTTP PATH, Empty for any
          Dest: 80 # Required, Destination of fallback, check https://xtls.github.io/config/features/fallback.html for details.
          ProxyProtocolVer: 0 # Send PROXY protocol version, 0 for disable
      DisableLocalREALITYConfig: false  # disable local reality config
      EnableREALITY: true # Enable REALITY
      REALITYConfigs:
        Show: true # Show REALITY debug
        Dest: www.smzdm.com:443 # Required, Same as fallback
        ProxyProtocolVer: 0 # Send PROXY protocol version, 0 for disable
        ServerNames: # Required, list of available serverNames for the client, * wildcard is not supported at the moment.
          - wangdazhuang.top
        PrivateKey: 4BXPQHhbBiiTS21bGNb3o9Fujqbm4QVkrbCfTBmV6kE # Required, execute './xray x25519' to generate.
        MinClientVer: # Optional, minimum version of Xray client, format is x.y.z.
        MaxClientVer: # Optional, maximum version of Xray client, format is x.y.z.
        MaxTimeDiff: 0 # Optional, maximum allowed time difference, unit is in milliseconds.
        ShortIds: # Required, list of available shortIds for the client, can be used to differentiate between different clients.
          - ""
          - 0123456789abcdef
      CertConfig:
        CertMode: dns # Option about how to get certificate: none, file, http, tls, dns. Choose "none" will forcedly disable the tls config.
        CertDomain: "node1.test.com" # Domain to cert
        CertFile: /etc/XrayR/cert/node1.test.com.cert # Provided if the CertMode is file
        KeyFile: /etc/XrayR/cert/node1.test.com.key
        Provider: alidns # DNS cert provider, Get the full support list here: https://go-acme.github.io/lego/dns/
        Email: test@me.com
        DNSEnv: # DNS ENV option used by DNS provider
          ALICLOUD_ACCESS_KEY: aaa
          ALICLOUD_SECRET_KEY: bbb

#  - PanelType: "SSpanel" # Panel type: SSpanel, V2board, NewV2board, PMpanel, Proxypanel, V2RaySocks, GoV2Panel
#    ApiConfig:
#      ApiHost: "http://127.0.0.1:668"
#      ApiKey: "123"
#      NodeID: 41
#      NodeType: V2ray # Node type: V2ray, Shadowsocks, Trojan, Shadowsocks-Plugin
#      Timeout: 30 # Timeout for the api request
#      EnableVless: false # Enable Vless for V2ray Type
#      VlessFlow: "xtls-rprx-vision" # Only support vless
#      SpeedLimit: 0 # Mbps, Local settings will replace remote settings, 0 means disable
#      DeviceLimit: 0 # Local settings will replace remote settings, 0 means disable
#      RuleListPath: # /etc/XrayR/rulelist Path to local rulelist file
#    ControllerConfig:
#      ListenIP: 0.0.0.0 # IP address you want to listen
#      SendIP: 0.0.0.0 # IP address you want to send pacakage
#      UpdatePeriodic: 60 # Time to update the nodeinfo, how many sec.
#      EnableDNS: false # Use custom DNS config, Please ensure that you set the dns.json well
#      DNSType: AsIs # AsIs, UseIP, UseIPv4, UseIPv6, DNS strategy
#      EnableProxyProtocol: false # Only works for WebSocket and TCP
#      AutoSpeedLimitConfig:
#        Limit: 0 # Warned speed. Set to 0 to disable AutoSpeedLimit (mbps)
#        WarnTimes: 0 # After (WarnTimes) consecutive warnings, the user will be limited. Set to 0 to punish overspeed user immediately.
#        LimitSpeed: 0 # The speedlimit of a limited user (unit: mbps)
#        LimitDuration: 0 # How many minutes will the limiting last (unit: minute)
#      GlobalDeviceLimitConfig:
#        Enable: false # Enable the global device limit of a user
#        RedisAddr: 127.0.0.1:6379 # The redis server address
#        RedisPassword: YOUR PASSWORD # Redis password
#        RedisDB: 0 # Redis DB
#        Timeout: 5 # Timeout for redis request
#        Expiry: 60 # Expiry time (second)
#      EnableFallback: false # Only support for Trojan and Vless
#      FallBackConfigs:  # Support multiple fallbacks
#        - SNI: # TLS SNI(Server Name Indication), Empty for any
#          Alpn: # Alpn, Empty for any
#          Path: # HTTP PATH, Empty for any
#          Dest: 80 # Required, Destination of fallback, check https://xtls.github.io/config/features/fallback.html for details.
#          ProxyProtocolVer: 0 # Send PROXY protocol version, 0 for disable
#      EnableREALITY: true # Enable REALITY
#      REALITYConfigs:
#        Show: true # Show REALITY debug
#        Dest: www.smzdm.com:443 # Required, Same as fallback
#        ProxyProtocolVer: 0 # Send PROXY protocol version, 0 for disable
#        ServerNames: # Required, list of available serverNames for the client, * wildcard is not supported at the moment.
#          - www.smzdm.com
#        PrivateKey: YOUR_PRIVATE_KEY # Required, execute './xray x25519' to generate.
#        MinClientVer: # Optional, minimum version of Xray client, format is x.y.z.
#        MaxClientVer: # Optional, maximum version of Xray client, format is x.y.z.
#        MaxTimeDiff: 0 # Optional, maximum allowed time difference, unit is in milliseconds.
#        ShortIds: # Required, list of available shortIds for the client, can be used to differentiate between different clients.
#          - ""
#          - 0123456789abcdef
#      CertConfig:
#        CertMode: dns # Option about how to get certificate: none, file, http, tls, dns. Choose "none" will forcedly disable the tls config.
#        CertDomain: "node1.test.com" # Domain to cert
#        CertFile: /etc/XrayR/cert/node1.test.com.cert # Provided if the CertMode is file
#        KeyFile: /etc/XrayR/cert/node1.test.com.key
#        Provider: alidns # DNS cert provider, Get the full support list here: https://go-acme.github.io/lego/dns/
#        Email: test@me.com
#        DNSEnv: # DNS ENV option used by DNS provider
#          ALICLOUD_ACCESS_KEY: aaa
#          ALICLOUD_SECRET_KEY: bbb
```


---