# Giá vàng Việt Nam

Theo dõi và lưu trữ dữ liệu **giá vàng tại Việt Nam** từ nhiều thương hiệu/hệ thống phổ biến. Dữ liệu được cập nhật dưới dạng tệp JSON đơn lẻ cho từng nguồn (SJC, PNJ, DOJI, Phú Quý, Ngọc Thẩm) cùng với một tệp tổng hợp.

> Các tệp hiện có trong repo: `data.json`, `sjc.json`, `pnj.json`, `doji.json`, `phuquy.json`, `ngoctham.json`.

## Nội dung

- `data.json`: Tập dữ liệu tổng hợp (all-in-one) cho nhiều thương hiệu/điểm bán.
- `sjc.json`: Dữ liệu giá vàng SJC.
- `pnj.json`: Dữ liệu giá vàng PNJ.
- `doji.json`: Dữ liệu giá vàng DOJI.
- `phuquy.json`: Dữ liệu giá vàng Phú Quý.
- `ngoctham.json`: Dữ liệu giá vàng Ngọc Thẩm.

> Lưu ý: Cấu trúc JSON có thể thay đổi theo thời gian tùy theo logic thu thập dữ liệu. Hãy kiểm tra nhanh nội dung tệp trước khi tích hợp.

## Cách sử dụng

Bạn có thể truy cập trực tiếp các tệp JSON qua **Raw GitHub** để tích hợp vào ứng dụng/cronjob/dịch vụ của bạn.

### cURL

```bash
# Tổng hợp
curl -L https://raw.githubusercontent.com/availableservices/gia-vang/main/data.json

# Theo nguồn
curl -L https://raw.githubusercontent.com/availableservices/gia-vang/main/sjc.json
curl -L https://raw.githubusercontent.com/availableservices/gia-vang/main/pnj.json
curl -L https://raw.githubusercontent.com/availableservices/gia-vang/main/doji.json
curl -L https://raw.githubusercontent.com/availableservices/gia-vang/main/phuquy.json
curl -L https://raw.githubusercontent.com/availableservices/gia-vang/main/ngoctham.json
```

### JavaScript (Node.js / Browser)

```js
// Ví dụ: đọc tổng hợp
const url = 'https://raw.githubusercontent.com/availableservices/gia-vang/main/data.json';

async function loadGoldPrices() {
  const res = await fetch(url, { cache: 'no-store' }); // hạn chế cache nếu cần realtime
  if (!res.ok) throw new Error(`HTTP ${res.status}`);
  const data = await res.json();
  console.log(data);
}

loadGoldPrices();
```

### Python

```python
import requests

url = "https://raw.githubusercontent.com/availableservices/gia-vang/main/pnj.json"
r = requests.get(url, timeout=15)
r.raise_for_status()
data = r.json()
print(data)
```

## Gợi ý tích hợp

- **Bộ nhớ đệm (caching):** Nếu ứng dụng có nhiều lượt truy cập, hãy cache kết quả trong vài chục giây–vài phút để giảm tải.
- **Kiểm soát lỗi:** Luôn bao bọc `try/catch` (JS) hoặc `raise_for_status()` (Python) và xử lý khi JSON thay đổi hoặc tạm thời trống.
- **Múi giờ & thời gian:** Nếu dữ liệu chứa mốc thời gian, chuẩn hóa về **UTC** hoặc **Asia/Ho_Chi_Minh** để so sánh/truy vấn.
- **Làm sạch dữ liệu:** Tên nhẫn, tuổi vàng, loại vàng hay chi nhánh có thể khác nhau theo nguồn; cân nhắc chuẩn hóa schema (ví dụ: `brand`, `type`, `buy`, `sell`, `unit`, `updated_at`).

## Đóng góp

Đóng góp, issue, hoặc PR đều được chào mừng:

1. Fork repo
2. Tạo nhánh tính năng: `git checkout -b feature/ten-tinh-nang`
3. Commit: `git commit -m "Mo ta thay doi"`
4. Push: `git push origin feature/ten-tinh-nang`
5. Mở Pull Request

Khi gửi PR, vui lòng mô tả:
- Nguồn dữ liệu (nếu thêm mới)
- Thay đổi schema (nếu có)
- Ảnh hưởng tới các tệp JSON đang có

## Miễn trừ trách nhiệm

- Dữ liệu có thể **chậm trễ** hoặc **không chính xác** tại một số thời điểm do thay đổi từ nguồn gốc hoặc lỗi mạng/thu thập.  
- Không sử dụng dữ liệu làm **tư vấn đầu tư**. Hãy kiểm chứng bằng nguồn chính thức trước khi ra quyết định tài chính.

## Liên hệ

- Mở [Issue] để báo lỗi/đề xuất.  
- Nếu bạn muốn tích hợp API hoặc có nhu cầu doanh nghiệp, vui lòng mô tả yêu cầu trong Issue để thảo luận thêm.
