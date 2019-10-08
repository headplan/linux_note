# v2ray

#### 搭建服务

```bash
#官方的一键安装脚本
bash <(curl -L -s https://install.direct/go.sh)
#第三方的傻瓜式一键安装配置脚本：
bash <(curl -s -L https://233yes.com/v2ray.sh)
```

#### 一键脚本

```
请选择 V2Ray 传输协议 [1-32]

  1. TCP
  2. TCP_HTTP
  3. WebSocket
  4. WebSocket + TLS
  5. HTTP/2
  6. mKCP
  7. mKCP_utp
  8. mKCP_srtp
  9. mKCP_wechat-video
 10. mKCP_dtls
 11. mKCP_wireguard
 12. QUIC
 13. QUIC_utp
 14. QUIC_srtp
 15. QUIC_wechat-video
 16. QUIC_dtls
 17. QUIC_wireguard
 18. TCP_dynamicPort
 19. TCP_HTTP_dynamicPort
 20. WebSocket_dynamicPort
 21. mKCP_dynamicPort
 22. mKCP_utp_dynamicPort
 23. mKCP_srtp_dynamicPort
 24. mKCP_wechat-video_dynamicPort
 25. mKCP_dtls_dynamicPort
 26. mKCP_wireguard_dynamicPort
 27. QUIC_dynamicPort
 28. QUIC_utp_dynamicPort
 29. QUIC_srtp_dynamicPort
 30. QUIC_wechat-video_dynamicPort
 31. QUIC_dtls_dynamicPort
 32. QUIC_wireguard_dynamicPort

备注1: 含有 [dynamicPort] 的即启用动态端口..
备注2: [utp | srtp | wechat-video | dtls | wireguard] 分别伪装成 [BT下载 | 视频通话 | 微信视频通话 | DTLS 1.2 数据包 | WireGuard 数据包]
```

#### v2ray客户端

[https://github.com/yanue/v2rayu](https://github.com/yanue/v2rayu)

[https://github.com/Cenmrev/V2RayX](https://github.com/Cenmrev/V2RayX)

