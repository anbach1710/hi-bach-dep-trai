---
title: "Tiến trình và Luồng"
date: "2025-05-06"
updated: "2025-05-0606"
categories:
  - "sveltekit"
  - "markdown"
  - "svelte"
coverImage: "/images/jerry-zhang-ePpaQC2c1xA-unsplash.jpg"
coverWidth: 16
coverHeight: 9
excerpt: ấn vào để xem thêm...
---

---

## 🔧 **BÀI TẬP 1: Phân tích hiệu năng máy ASUS TUF GAMING F15**

**Cấu hình phổ biến của ASUS TUF GAMING F15:**

* **CPU**: Intel Core i5-10300H (14 nhân: 6 hiệu năng + 8 tiết kiệm điện, 20 threads)
* **GPU**: NVIDIA GeForce RTX 3050/3060/3070 tùy phiên bản
* **RAM**: 8GB DDR4 hoặc DDR5
* **Ổ cứng**: SSD NVMe tốc độ cao

**Hiệu năng:**

* Với 20 threads, máy có thể xử lý tốt đa luồng (multithreading), đặc biệt hữu ích cho lập trình song song, chơi game, hoặc xử lý dữ liệu lớn.
* GPU RTX hỗ trợ tính toán song song thông qua CUDA, rất phù hợp cho AI, machine learning.
* RAM 8GB đủ cho chạy nhiều tiến trình cùng lúc mà không gây chậm trễ lớn.

**→ Nhận định**: Máy có cấu hình mạnh mẽ, phù hợp cho cả đa luồng (nhiều luồng chạy song song trong một tiến trình) lẫn đa tiến trình (nhiều chương trình chạy độc lập).
![hihi](../../../images/hihi.jpg)
---

## 📝 **BÀI TẬP 2: 12 bài toán CNTT phổ biến sử dụng đa luồng / đa tiến trình**

| STT | Bài toán                                 | Đa tiến trình | Đa luồng |
| --- | ---------------------------------------- | ------------- | -------- |
| 1   | Trình duyệt web (Chrome, Firefox)        | ✓             | ✓        |
| 2   | Xử lý ảnh/video (Photoshop, Premiere)    | ✓             | ✓        |
| 3   | Web server (Apache, Nginx)               | ✓             | ✓        |
| 4   | Trò chơi (Game Engine)                   | ✓             | ✓        |
| 5   | AI/ML training                           | ✓             | ✓        |
| 6   | Database server (MySQL, PostgreSQL)      | ✓             | ✓        |
| 7   | Chương trình IDE như VSCode, IntelliJ    | ✓             | ✓        |
| 8   | Trình phát nhạc/video                    | ✓             | ✓        |
| 9   | App mobile có nhiều dịch vụ nền          | ✓             | ✓        |
| 10  | Công cụ crawl dữ liệu (Scrapy, Selenium) | ✓             | ✓        |
| 11  | MapReduce (Hadoop)                       | ✓             | ✗        |
| 12  | Quản lý hệ điều hành                     | ✓             | ✓        |

---

## 📸 **BÀI TẬP 3: So sánh khi nào dùng Thread, Process (viết ra giấy + ví dụ)**

![hi](../../../images/hi.jpg)
---

 **BÀI TẬP 4: Report – ChatGPT training sử dụng hệ thống phân tán như thế nào?**

**Tóm tắt:**

* ChatGPT được huấn luyện bởi OpenAI trên **siêu máy tính** do Microsoft Azure cung cấp.
* Mô hình dùng **distributed training** với hàng ngàn GPU nối mạng.
* Dữ liệu huấn luyện được chia nhỏ, mỗi GPU xử lý một phần => đồng bộ hoá qua **NCCL + AllReduce**.
* Dùng kỹ thuật như **pipeline parallelism**, **tensor parallelism** để tối ưu hiệu năng.

