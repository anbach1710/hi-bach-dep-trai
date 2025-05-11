---
title: "Tổng quan về ứng dụng phân tán"
date: "2025-04-29"
updated: "2025-04-2929"
categories:
  - "sveltekit"
  - "markdown"
coverImage: "/images/jefferson-santos-fCEJGBzAkrU-unsplash.jpg"
coverWidth: 16
coverHeight: 9
excerpt: Ấn vào, để xem thêmthêm
---

## 1. Hệ thống phân tán là gì?

Hệ thống phân tán (Distributed System) là một tập hợp các máy tính độc lập (node) được kết nối với nhau thông qua mạng truyền thông, hoạt động phối hợp để cung cấp dịch vụ như một hệ thống thống nhất đối với người dùng cuối.

---

## 2. Các ứng dụng của hệ thống phân tán

- Hệ thống tìm kiếm như Google.
- Mạng xã hội như Facebook, Zalo.
- Dịch vụ thương mại điện tử: Tiki, Shopee.
- Dịch vụ ngân hàng và ví điện tử: Momo, Internet Banking.
- Hệ thống chơi game trực tuyến: Liên Quân Mobile, PUBG.
- Hệ thống lưu trữ đám mây: Google Drive, Dropbox.
- Blockchain và tiền mã hóa: Bitcoin, Ethereum.

---

## 3. Các khái niệm chính của hệ thống phân tán

### Giải thích thuật ngữ

- **Scalability**: Khả năng mở rộng hệ thống khi số lượng người dùng tăng.
- **Fault Tolerance**: Khả năng tiếp tục hoạt động khi một thành phần gặp lỗi.
- **Availability**: Khả năng cung cấp dịch vụ liên tục không gián đoạn.
- **Transparency**: Tính trong suốt – người dùng không biết tài nguyên ở đâu, được xử lý như thế nào.
- **Concurrency**: Khả năng nhiều người dùng cùng truy cập và thao tác đồng thời.
- **Parallelism**: Khả năng thực thi nhiều tác vụ cùng lúc để tăng hiệu suất.
- **Openness**: Khả năng mở rộng và tích hợp với các hệ thống khác dễ dàng.
- **Vertical Scaling**: Nâng cấp phần cứng máy chủ hiện có.
- **Horizontal Scaling**: Thêm nhiều máy chủ để chia tải.
- **Load Balancer**: Cân bằng tải – phân phối yêu cầu người dùng đến các server khác nhau.
- **Replication**: Sao chép dữ liệu để tăng độ tin cậy và hiệu suất.

### Ví dụ: Hệ thống đặt vé máy bay trực tuyến

- Khi người dùng tìm kiếm chuyến bay, một server xử lý tìm kiếm được sử dụng.
- Khi người dùng đặt vé, một server khác xử lý đặt vé và thanh toán.
- Hệ thống có thể scale ngang để xử lý nhiều người đặt cùng lúc (**Scalability**).
- Nếu một server lỗi, server khác vẫn tiếp tục hoạt động (**Fault Tolerance**).
- Người dùng không biết hệ thống xử lý ở đâu (**Transparency**).
- Sử dụng **Load Balancer** để phân chia yêu cầu đến các node.
- Dữ liệu vé được sao lưu ở nhiều nơi (**Replication**).

---

## 4. Kiến trúc của hệ thống phân tán

### Một số kiến trúc phổ biến:

1. **Client–Server**: Máy khách gửi yêu cầu, máy chủ xử lý.
2. **Three-Tier Architecture**: Giao diện người dùng, xử lý logic, cơ sở dữ liệu.
3. **Microservices**: Chia nhỏ hệ thống thành các dịch vụ nhỏ, độc lập.