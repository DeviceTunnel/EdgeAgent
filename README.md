
# EdgeAgent

[![build](https://github.com/DeviceTunnel/EdgeAgent/actions/workflows/build.yml/badge.svg)](https://github.com/DeviceTunnel/EdgeAgent/actions/workflows/build.yml)

EdgeAgent là thành phần chạy trên từng máy (edge) của hệ thống DeviceTunnel. Agent được cài như một service trên máy Windows hoặc Linux, thu thập tình trạng của máy và giữ một kết nối gRPC liên tục về server trung tâm để báo cáo.

Repo này chỉ chứa agent và hợp đồng gRPC giữa agent với server. Server là một dự án riêng.

## Vai trò trong hệ thống

```
  máy Windows ─┐
  máy Linux  ──┼── EdgeAgent ══ gRPC stream (mTLS) ══▶  DeviceTunnel server
  máy Linux  ──┘        ▲                                      │
                        └──────── cấu hình (chu kỳ, top N) ────┘
```

Mỗi máy chạy một agent. Agent chủ động kết nối ra server, nên máy không cần mở cổng vào và vẫn hoạt động sau NAT hoặc firewall. Trên cùng kết nối đó, agent đẩy số liệu theo chu kỳ, còn server có thể gửi ngược cấu hình xuống mà không cần đăng nhập vào từng máy.
