---
title: "Truyền Thông"
date: "2025-05-07"
updated: "2025-05-07"
categories:
  - "AnBach"
coverImage: "/images/jefferson-santos-fCEJGBzAkrU-unsplash.jpg"
coverWidth: 16
coverHeight: 9
excerpt: Ấn vào để xem thêm...
---

---

## **BÀI TẬP 1: Tìm hiểu cơ chế, chức năng và cài đặt RabbitMQ**

### 1. Giới thiệu

RabbitMQ là một hệ thống hàng đợi thông điệp mã nguồn mở, sử dụng giao thức AMQP (Advanced Message Queuing Protocol). Nó cho phép các tiến trình, ứng dụng và hệ thống khác nhau giao tiếp với nhau thông qua trao đổi thông điệp một cách bất đồng bộ.

### 2. Cơ chế hoạt động

RabbitMQ hoạt động dựa trên mô hình **producer - queue - consumer**. Các producer gửi thông điệp vào một **exchange**, nơi thông điệp được định tuyến tới một hoặc nhiều **queue**. Các consumer đăng ký nhận thông điệp từ các queue đó.

Cơ chế chính bao gồm:

* Producer gửi thông điệp đến Exchange.
* Exchange định tuyến thông điệp đến các Queue dựa trên cấu hình routing.
* Consumer nhận thông điệp từ Queue và xử lý.

### 3. Chức năng chính

* **Tách biệt các thành phần của hệ thống**: Producer và consumer không cần biết nhau, giúp hệ thống dễ mở rộng và bảo trì.
* **Hàng đợi thông điệp**: RabbitMQ lưu trữ tạm thời các thông điệp trong hàng đợi nếu consumer chưa sẵn sàng.
* **Phân phối tải**: RabbitMQ có thể gửi thông điệp đến nhiều consumer nhằm cân bằng tải.
* **Đảm bảo độ tin cậy**: Thông điệp có thể được lưu lại (durable queue) để tránh mất dữ liệu khi có lỗi.

### 4. Cài đặt

Sử dụng Docker để cài RabbitMQ:

```bash
docker run -d --hostname my-rabbit --name some-rabbit \
  -p 5672:5672 -p 15672:15672 rabbitmq:3-management
```

Sau khi chạy, truy cập giao diện web quản trị tại:

```
http://localhost:15672
```

Tài khoản mặc định: guest / guest


---

## **BÀI TẬP 2: Code một hệ thống đơn giản sử dụng RabbitMQ**

### 1. Mô hình hệ thống

* Producer gửi thông điệp (dữ liệu) đến một queue.
* Consumer nhận và xử lý thông điệp đó.
* Cả hai sử dụng RabbitMQ làm môi trường trung gian truyền tin.

### 2. Cài đặt thư viện

Ngôn ngữ sử dụng: Python
Cài thư viện `pika` để giao tiếp với RabbitMQ:

```bash
pip install pika
```

### 3. Mã nguồn

**Producer (send.py)**

```python
import pika

connection = pika.BlockingConnection(pika.ConnectionParameters('localhost'))
channel = connection.channel()

channel.queue_declare(queue='hello')

channel.basic_publish(exchange='',
                      routing_key='hello',
                      body='Hello RabbitMQ!')
print("Sent 'Hello RabbitMQ!'")

connection.close()
```

**Consumer (receive.py)**

```python
import pika

connection = pika.BlockingConnection(pika.ConnectionParameters('localhost'))
channel = connection.channel()

channel.queue_declare(queue='hello')

def callback(ch, method, properties, body):
    print("Received:", body.decode())

channel.basic_consume(queue='hello',
                      on_message_callback=callback,
                      auto_ack=True)

print("Waiting for messages. To exit press CTRL+C")
channel.start_consuming()
```

Chạy hai file trên hai terminal khác nhau để quan sát hoạt động gửi và nhận thông điệp.

---

## **BÀI TẬP 3: Tìm hiểu và demo thư viện RPC sử dụng định dạng JSON**

### 1. Tổng quan về RPC

RPC (Remote Procedure Call) là cơ chế cho phép gọi hàm từ xa, giống như gọi hàm cục bộ. Trong bài học trước đã sử dụng `xmlrpc`. Trong bài này sẽ sử dụng **JSON-RPC**, một giao thức RPC sử dụng định dạng dữ liệu JSON.

### 2. Các thư viện RPC phổ biến khác

Ngoài `xmlrpc`, có thể sử dụng các thư viện sau:

* `json-rpc`
* `gRPC`
* `msgpack-rpc`
* `zerorpc`
* `Thrift`

### 3. Lựa chọn thư viện: `json-rpc` với Flask

Cài đặt:

```bash
pip install Flask json-rpc
```

### 4. Mã nguồn demo

**Server: json\_server.py**

```python
from flask import Flask
from jsonrpcserver import method, serve

app = Flask(__name__)

@method
def add(a, b):
    return a + b

@app.route("/", methods=["POST"])
def handle():
    return serve()

if __name__ == "__main__":
    app.run(port=5000)
```

**Client: json\_client.py**

```python
import requests

payload = {
    "jsonrpc": "2.0",
    "method": "add",
    "params": [10, 5],
    "id": 1
}

response = requests.post("http://localhost:5000", json=payload)
print("Kết quả:", response.json()["result"])
```

Khi chạy server và client, đầu ra sẽ là:

```
Kết quả: 15
```


---

