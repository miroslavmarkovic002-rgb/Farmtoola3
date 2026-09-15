# 🌾 Farm Tool A3 - Công Cụ Hỗ Trợ Canh Tác & Dự Báo Năng Suất Cây Củ

**Farm Tool A3** là ứng dụng web nhẹ giúp nông dân và người làm nông nghiệp lập kế hoạch canh tác hiệu quả. Công cụ hỗ trợ tính toán nhu cầu nước tưới, dự báo thời gian thu hoạch, ước tính năng suất và phân tích điều kiện môi trường (pH, nhiệt độ, độ ẩm) cho các loại cây củ phổ biến.

---

## 🌟 Tính Năng Chính

* 🥔 **Đa dạng cây trồng:** Hỗ trợ 5 loại cây củ chính bao gồm *Khoai tây, Khoai sắn (Sắn/Khoai mì), Khoai lang, Cà rốt* và *Củ dền*.
* 📐 **Chuyển đổi đơn vị linh hoạt:** Hỗ trợ tính toán theo mét vuông ($m^2$) và Hécta ($ha$).
* 💧 **Tính toán nước tưới thông minh:** Tự động điều chỉnh nhu cầu nước tưới hàng ngày và toàn vụ dựa trên nhiệt độ môi trường và độ ẩm không khí.
* 📅 **Dự báo thu hoạch:** Xác định chính xác khung thời gian thu hoạch dự kiến dựa trên ngày gieo trồng.
* 📊 **Ước tính năng suất:** Dự báo tổng sản lượng thu hoạch (kg hoặc Tấn) theo quy mô diện tích.
* 🧪 **Phân tích & Cảnh báo đất trồng:** Đánh giá độ pH, đưa ra lời khuyên xử lý đất (bón vôi/phân hữu cơ) và cảnh báo nguy cơ nấm bệnh khi độ ẩm cao.

---

## 🏗️ Cấu Trúc Dự Án & Luồng Hoạt Động

```text
┌─────────────────────────────────────────────────────────────────────────────────┐
│                                GIAO DIỆN (UI/UX)                                │
├─────────────────────────────────────────────────────────────────────────────────┤
│  [1. Chọn loại cây] ──► Khoai tây / Khoai sắn / Khoai lang / Cà rốt / Củ dền    │ 
│  [2. Ngày gieo trồng] ─► Chọn ngày (Mặc định: Ngày hiện tại)                    │
│  [3. Diện tích] ──────► [ Nhập số ] + [ Đơn vị: m² / ha ]                       │
│  [4. Môi trường] ─────► pH đất | Nhiệt độ (°C) | Độ ẩm (%)                      │
│                                                                                 │
│                              [ NÚT: TÍNH KẾT QUẢ ]                              │
└───────────────────────────────┬─────────────────────────────────────────────────┘
                                │ (Nhấp chuột)
                                ▼
┌─────────────────────────────────────────────────────────────────────────────────┐
│                            LUỒNG XỬ LÝ KỸ THUẬT (JS)                            │
├─────────────────────────────────────────────────────────────────────────────────┤
│  1. Kiểm tra dữ liệu đầu vào (Validation)                                       │
│  2. Quy đổi đơn vị chuẩn (1 ha = 10,000 m²)                                     │
│  3. Lấy dữ liệu nông nghiệp gốc từ cơ sở dữ liệu `cropData`                     │
│  4. Tính toán chu kỳ sinh trưởng & Tổng năng suất                               │
│  5. Thuật toán điều chỉnh lượng nước theo Nhiệt độ & Độ ẩm                      │
│  6. Phân tích & Đánh giá môi trường (pH, rủi ro sâu bệnh)                       │
└───────────────────────────────┬─────────────────────────────────────────────────┘
                                │ (Xuất kết quả)
                                ▼
┌─────────────────────────────────────────────────────────────────────────────────┐
│                                BẢNG KẾT QUẢ HIỂN THỊ                            │
├─────────────────────────────────────────────────────────────────────────────────┤
│  ✔ Khoảng thời gian thu hoạch dự kiến (Ngày/Tháng/Năm)                          │
│  ✔ Lượng nước tưới hằng ngày (Lít hoặc m³/ngày)                                 │
│  ✔ Tổng nhu cầu nước cả vụ canh tác (m³)                                        │
│  ✔ Ước tính tổng năng suất thu hoạch (kg / Tấn)                                 │
│  ⚠ Khuyến nghị xử lý đất & Cảnh báo thời tiết                                   │
└─────────────────────────────────────────────────────────────────────────────────┘
