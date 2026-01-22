# Mô Phỏng Hệ Thống Mạng Campus Trường Học

## 1. Giới thiệu

Dự án này mô phỏng một hệ thống mạng campus cho trường học nhiều tòa nhà, được thiết kế theo mô hình phân tầng, có phân đoạn mạng rõ ràng, định tuyến linh hoạt, dự phòng gateway và tích hợp mạng không dây. Toàn bộ hệ thống được triển khai và kiểm thử trên Cisco Packet Tracer nhằm phục vụ mục đích học tập và thực hành các công nghệ mạng cốt lõi.

## 2. Mục tiêu dự án

- Thiết kế mạng cho môi trường trường học với nhiều phòng ban và tòa nhà
- Phân đoạn mạng bằng VLAN để tăng khả năng quản lý và an toàn
- Triển khai định tuyến liên VLAN trên switch Layer 3
- Đảm bảo tính sẵn sàng cao cho gateway bằng HSRP
- Tự động cấp phát địa chỉ IP bằng DHCP tập trung
- Cung cấp dịch vụ phân giải tên miền (DNS) nội bộ
- Tích hợp mạng không dây với VLAN thông qua SSID

## 3. Kiến trúc tổng thể

- **Hệ thống gồm 4 tòa nhà**: A1, B1, A2, B2
- **Switch Layer 2** dùng để kết nối máy trạm tại các phòng/ban
- **Switch Layer 3 (Core / Distribution)** đảm nhiệm:
  - Định tuyến liên VLAN (Inter-VLAN Routing)
  - HSRP cho gateway dự phòng
  - Chạy giao thức định tuyến OSPF
- **Máy chủ DHCP, DNS** đặt tập trung trong VLAN Server
- **Các Access Point** hỗ trợ nhiều SSID và gán VLAN tương ứng

## 4. Công nghệ & Kỹ thuật sử dụng

### 4.1 Switching & VLAN
- VLAN (Virtual LAN)
- Access Port & Trunk Port
- IEEE 802.1Q Trunking
- Native VLAN
- VTP (VLAN Trunking Protocol)
- STP (Spanning Tree Protocol)

### 4.2 Routing & High Availability
- Inter-VLAN Routing bằng SVI trên Switch Layer 3
- HSRP (Hot Standby Router Protocol)
- OSPF (Open Shortest Path First)

### 4.3 Dịch vụ mạng
- DHCP Server tập trung
- DHCP Relay (ip helper-address)
- DNS Server nội bộ

### 4.4 Wireless Networking
- WLAN (Wireless LAN)
- Multiple SSID
- SSID gắn VLAN (WLAN–VLAN Mapping)

### 4.5 Công cụ
- Cisco Packet Tracer
- Cisco IOS CLI

## 5. Tổng quan VLAN

| VLAN ID | Chức năng      |
|---------|----------------|
| 10      | Công nghệ      |
| 20      | Cầu đường      |
| 30      | Tài vụ         |
| 40      | Phòng máy      |
| 50      | Server         |
| 60      | Kinh tế        |
| 70      | Hành chính     |
| 80      | Phòng máy      |
| 1001    | Native VLAN    |

## 6. Mạng không dây (Wireless)

- Các Access Point được cấu hình nhiều SSID
- Mỗi SSID được ánh xạ (mapping) vào một VLAN cụ thể
- Thiết bị không dây khi kết nối sẽ thuộc VLAN tương ứng với SSID

**Ví dụ:**
- SSID it → VLAN 10
- SSID tv → VLAN 30
- SSID cd → VLAN 20
- SSID admin → VLAN 1001

## 7. Định tuyến & dự phòng

- Các VLAN được định tuyến thông qua SVI trên switch Layer 3
- Gateway mặc định của mỗi VLAN sử dụng HSRP virtual IP

**HSRP đảm bảo:**
- Gateway luôn sẵn sàng khi có sự cố
- Có thể chia tải gateway theo nhóm VLAN

- OSPF được sử dụng để trao đổi thông tin định tuyến giữa các thiết bị Layer 3

## 8. Dịch vụ DHCP & DNS

- DHCP Server cấp phát IP tự động cho các VLAN
- Các VLAN khác VLAN Server sử dụng DHCP Relay
- DNS Server nội bộ cho phép truy cập dịch vụ bằng tên miền thay vì địa chỉ IP

## 9. Kịch bản kiểm thử

- Máy trạm nhận đúng địa chỉ IP theo VLAN
- Các VLAN giao tiếp được với nhau
- Gateway vẫn hoạt động khi thiết bị Layer 3 chính gặp sự cố
- Thiết bị Wi-Fi vào đúng VLAN theo SSID
- Truy cập được dịch vụ nội bộ thông qua DNS

## 10. Cách chạy mô phỏng

1. Mở file .pkt bằng Cisco Packet Tracer
2. Bật nguồn các thiết bị mạng
3. Chờ DHCP, HSRP và OSPF hội tụ
4. Kiểm tra kết nối bằng lệnh ping và trình duyệt web

