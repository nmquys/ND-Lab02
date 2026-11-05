# ND-Lab02 – Advanced OSPF Area 0 • Redundant WAN

Bài thực hành môn **Network Design**: mạng 4 router – 4 switch – 10 PC, 4 LAN và 5 liên kết WAN dạng lưới (có đường dự phòng), chạy **OSPF process 1, Area 0** trong Cisco Packet Tracer.

## Nội dung repository

| File | Mô tả |
| --- | --- |
| `MSSV_HoTenSinhVien_ND-Lab02.pdf` | Báo cáo (Predict → Build → Configure → Verify → Simulate → Explain) |
| `MSSV_HoTenSinhVien_ND-Lab02.pkt` | File Packet Tracer chạy được |
| `NDLab02_Configs.txt` | Cấu hình đầy đủ R1–R4, SW1–SW4 và thông số PC |

## Tóm tắt thiết kế

- 9 subnet /24: LAN1–LAN4 (`192.168.1–4.0/24`) và WAN1–WAN5 (`10.0.1–5.0/24`).
- Router-ID: R1 `1.1.1.1`, R2 `2.2.2.2`, R3 `3.3.3.3`, R4 `4.4.4.4`.
- Đầu DCE (có `clock rate 64000`): R1 (S0/0/0, S0/0/1, S0/1/0), R2 S0/0/1, R4 S0/0/1.
- Cost OSPF: serial = 64, FastEthernet = 1 → đường PC0 ↔ PC9 đi qua WAN2 (R1–R4), cost 65, đối xứng.

## Kết quả kiểm thử chính

- Neighbor FULL trên cả 5 WAN; mọi LAN liên lạc hai chiều.
- Ngắt WAN5 (R1–R3): R1 → LAN2 chuyển sang 2 đường ECMP cost 129 qua R2 và R4; khôi phục trả về cost 65.
- Ngắt WAN2 (làm thêm): PC0 ↔ PC9 chuyển sang đường R1 → R3 → R4 (cost 129).
- Đã phân tích 15 tình huống Problem Solving và 25 câu Interview trong báo cáo.

## Cách chạy lại

1. Mở file `.pkt` trong Cisco Packet Tracer.
2. Hoặc dựng lại topology theo báo cáo (mục 1) và dán cấu hình trong `NDLab02_Configs.txt` vào từng thiết bị.
3. Kiểm tra: `show ip ospf neighbor`, `show ip route ospf`, `ping`/`tracert` từ PC0 tới PC9.
