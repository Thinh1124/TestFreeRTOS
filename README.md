# 🌱 Smart Garden System using FreeRTOS (Arduino UNO)

## 📌 Giới thiệu

Dự án **Nghiên cứu phát triển hệ thống tưới cây tự động sử dụng hệ điều hành thời gian thực FREERTOS** là hệ thống tưới cây tự động sử dụng vi điều khiển Arduino UNO. Hệ thống được thiết kế theo kiến trúc **2 board** nhằm tối ưu tài nguyên phần cứng và tránh tràn bộ nhớ khi sử dụng FreeRTOS.

- 🔵 **Board Sensor**: Đọc cảm biến (DHT11, độ ẩm đất) và hiển thị OLED
- 🔴 **Board Main**: Xử lý logic điều khiển bằng FreeRTOS và điều khiển bơm nước

---

## 🧠 Kiến trúc hệ thống

```
[SENSOR BOARD]  ---> UART --->  [MAIN BOARD]
(DHT11, Soil, OLED)           (FreeRTOS + Relay)
```

### 🔵 Sensor Board

- Đọc:
  - Nhiệt độ (Temp)
  - Độ ẩm không khí (Hum)
  - Độ ẩm đất (Soil)

- Hiển thị lên OLED
- Gửi dữ liệu qua UART

### 🔴 Main Board

- Nhận dữ liệu từ Sensor Board
- Xử lý logic tưới cây (State Machine)
- Điều khiển Relay (bơm nước)
- Chạy FreeRTOS với 2 Task

---

## 🔌 Kết nối phần cứng

### 📡 UART giữa 2 Arduino

| Sensor Board | Main Board |
| ------------ | ---------- |
| TX (D1)      | RX (D0)    |
| GND          | GND        |

---

### 🌡️ Cảm biến DHT11

- DATA → D2
- VCC → 5V
- GND → GND

---

### 🌱 Cảm biến độ ẩm đất

- Analog → A0

---

### 💧 Relay (bơm nước)

- IN → D8
- VCC → 5V
- GND → GND

---

### 💡 LED báo lỗi nằm trên mạch uno

- D13 → điện trở 220Ω → LED → GND

---

### 📺 OLED (I2C)

| OLED | Arduino |
| ---- | ------- |
| SDA  | A4      |
| SCL  | A5      |
| VCC  | 5V      |
| GND  | GND     |

---

## 📡 Giao thức UART

Dữ liệu gửi từ Sensor Board:

```
T:30,H:65,S:450
```

| Ký hiệu | Ý nghĩa             |
| ------- | ------------------- |
| T       | Nhiệt độ (°C)       |
| H       | Độ ẩm không khí (%) |
| S       | Độ ẩm đất           |

---

## ⚙️ Logic hoạt động

### 🌿 State Machine

| State    | Mô tả                |
| -------- | -------------------- |
| IDLE     | Không tưới           |
| PUMPING  | Đang tưới            |
| OVERHEAT | Dừng do nhiệt độ cao |
| ERROR    | Lỗi hệ thống         |

---

### 🔥 Điều kiện hoạt động

- Bật bơm khi:

  ```
  Soil > DRY_THRESHOLD AND Temp < 32°C
  ```

- Tắt bơm khi:

  ```
  Soil < WET_THRESHOLD
  ```

---

### ⚠️ Safety Features

#### 🌡️ Chống sốc nhiệt

- Nếu `Temp > 32°C`
- Ngừng tưới ngay

#### ⏱️ Safety Timeout

- Nếu bơm chạy > 10 phút
- → Chuyển sang ERROR
- → LED nháy cảnh báo

---

## 🧵 FreeRTOS Design

### Task sử dụng

| Task         | Chức năng           | Priority |
| ------------ | ------------------- | -------- |
| Task_Control | Xử lý logic + Relay | 2        |
| Task_Monitor | Debug Serial        | 1        |

---

### ⚡ Tối ưu RAM

- Không dùng Queue
- Không dùng String
- Dùng `F()` cho Serial
- Dùng kiểu nhỏ:
  - `int8_t`, `uint8_t`

- Stack ~100 words/task

---

## 🚀 Ưu điểm hệ thống

- ✅ Tránh tràn RAM (UNO 2KB)
- ✅ Chạy ổn định với FreeRTOS
- ✅ Tách sensor giúp dễ mở rộng
- ✅ Giao tiếp UART đơn giản, hiệu quả

---

## ⚠️ Lưu ý khi sử dụng

- Rút dây UART khi upload code
- Kiểm tra đúng baud rate (9600)
- Đảm bảo nối chung GND
- Kiểm tra relay active HIGH/LOW

---

## 🔧 Hướng phát triển

- 📶 Thêm WiFi (ESP8266 / ESP32)
- 📱 Điều khiển qua app
- 🌦️ Thêm cảm biến mưa
- ☀️ Thêm cảm biến ánh sáng

## 📄 License

Dự án phục vụ mục đích học tập và nghiên cứu.
