# 📊 EMG / ADC Signal Analysis & Labeling Tool (Dash)

## 🇻🇳 Giới thiệu

Ứng dụng này là một **công cụ web xây dựng bằng Dash (Python)** dùng để:

* Tải và hiển thị **tín hiệu ADC/EMG** từ file `.txt`
* Tính và hiển thị **đường bao (Envelope)** của tín hiệu EMG
* **Chọn vùng thời gian** trên tín hiệu
* **Gắn nhãn (Labeling)** cho từng đoạn tín hiệu (Flexion, Extension, Rest)
* **Cập nhật / xóa / xuất** dữ liệu đã gắn nhãn

Ứng dụng phù hợp cho:

* Thí nghiệm EMG
* Tiền xử lý dữ liệu cho Machine Learning
* Gán nhãn thủ công tín hiệu y sinh

---

## 🇬🇧 Overview

This is a **Dash-based web application** for:

* Loading ADC/EMG signals from `.txt` files
* Computing and visualizing EMG envelopes
* Selecting time ranges interactively
* Labeling signal segments
* Exporting labeled datasets

---

## 🧠 Chức năng chính

### 1. 📂 Tải dữ liệu TXT

* Hỗ trợ file TXT dạng **Viking Natus / ADC log**
* Tự động **loại bỏ metadata** (`;`, `[ ]`, `key=value`)
* Trích xuất dữ liệu số ADC

### 2. 📈 Hiển thị tín hiệu

* Tín hiệu thô (đã giảm mẫu để tối ưu hiệu năng)
* Đường bao EMG (Rectification + Moving Average)
* Zoom, pan, chọn vùng bằng chuột

### 3. ✂️ Chọn vùng & gắn nhãn

* Kéo chọn vùng thời gian trực tiếp trên đồ thị
* Gắn nhãn cố định:

  * **Flexion** (đỏ)
  * **Extension** (cam)
  * **Rest** (xanh lá)
* Mỗi nhãn gồm:

  ```json
  {
    "channel": "ch0",
    "start": 1.234,
    "end": 2.345,
    "label": "Flexion",
    "color": "#d62728"
  }
  ```

### 4. 📝 Quản lý nhãn

* Danh sách nhãn hiển thị bên dưới
* Click để chọn / bỏ chọn nhãn
* Cập nhật hoặc xóa nhãn đã chọn

### 5. 📤 Xuất dữ liệu

* Xuất ra file `emg_project_labeled.txt`
* Bao gồm:

  * Metadata (FS, số mẫu)
  * Dữ liệu ADC gốc
  * Danh sách nhãn (JSON)

---

## ⚙️ Cấu hình quan trọng

```python
FS = 19200.0          # Tần số lấy mẫu (Hz)
DOWNSAMPLE_FACTOR = 10
```

### Nhãn & màu sắc

```python
LABEL_OPTIONS = {
    "Flexion": "#d62728",
    "Rest": "#2ca02c",
    "Extension": "#ff7f0e"
}
```

---

## 🧮 Xử lý tín hiệu

### Envelope EMG

* Rectification: `abs(signal)`
* Làm trơn: Moving Average

```python
def emg_envelope(x, win=100):
    x = np.abs(x)
    kernel = np.ones(win) / win
    return np.convolve(x, kernel, mode="same")
```

---

## 🖥️ Giao diện người dùng

* Upload file TXT
* Dropdown chọn kênh
* Đồ thị tương tác (Plotly)
* Nút chức năng: Save / Update / Delete / Export

---

## ▶️ Cách chạy chương trình

### 1. Cài thư viện

```bash
pip install dash plotly numpy
```

### 2. Chạy ứng dụng

```bash
python app.py
```

### 3. Mở trình duyệt

```
http://127.0.0.1:8050
```

---

## 📁 Cấu trúc file gợi ý

```
project/
│── app.py
│── README.md
│── data/
│   └── sample_emg.txt
```

---

## 🚀 Hướng phát triển

* [ ] Hỗ trợ nhiều kênh EMG
* [ ] Xuất CSV / MAT
* [ ] Tự động gợi ý nhãn
* [ ] Kết nối model ML

---

## 👤 Tác giả

* Nguyễn Giang
* Mục đích: học tập, nghiên cứu EMG & xử lý tín hiệu y sinh

---

## 📜 License

Sử dụng cho mục đích **học tập và nghiên cứu**.
# EMG-label
