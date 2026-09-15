┌─────────────────────────────────────────────────────────────────────────────────┐
│                                GIAO DIỆN (UI/UX)                                │
├─────────────────────────────────────────────────────────────────────────────────┤
│                                                                                 │
│  [1. Chọn loại cây] ──► Khoai tây / Khoai sắn / Khoai lang / Cà rốt / Củ dền   │
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
│                                                                                 │
│  1. Kiểm tra dữ liệu đầu vào (Validation)                                      │
│     └── Kiểm tra diện tích > 0 & ngày hợp lệ                                    │
│                                                                                 │
│  2. Quy đổi đơn vị chuẩn                                                       │
│     └── Nếu chọn Hécta (ha) ──► Quy đổi: 1 ha = 10,000 m²                       │
│                                                                                 │
│  3. Lấy dữ liệu nông nghiệp gốc (Từ cơ sở dữ liệu `cropData`)                   │
│     └── Ngày sinh trưởng, Nước cơ bản (lít/m²), Năng suất (kg/m²), pH chuẩn     │
│                                                                                 │
│  4. Tính toán Chu kỳ & Năng suất                                                │
│     ├── Ngày thu hoạch = Ngày trồng + Số ngày sinh trưởng (Min - Max)           │
│     └── Tổng năng suất  = Năng suất chuẩn × Diện tích (Quy đổi kg ──► Tấn)      │
│                                                                                 │
│  5. Thuật toán điều chỉnh Lượng nước (Theo Nhiệt độ & Độ ẩm)                     │
│     ├── Nhiệt độ > 32°C  ──► +20% nước  |  Nhiệt độ < 18°C ──► -15% nước         │
│     └── Độ ẩm < 40%      ──► +10% nước  |  Độ ẩm > 85%   ──► -10% nước         │
│                                                                                 │
│  6. Phân tích & Đánh giá Môi trường                                             │
│     ├── So sánh pH nhập vào vs pH tối ưu ──► Đưa cảnh báo Chua / Kiềm / Chuẩn   │
│     └── Cảnh báo rủi ro sâu bệnh nếu độ ẩm > 85%                                │
│                                                                                 │
└───────────────────────────────┬─────────────────────────────────────────────────┘
                                │ (Xuất kết quả)
                                ▼
┌─────────────────────────────────────────────────────────────────────────────────┐
│                                BẢNG KẾT QUẢ HIỂN THỊ                            │
├─────────────────────────────────────────────────────────────────────────────────┤
│                                                                                 │
│  ✔ Khoảng thời gian thu hoạch dự kiến (Ngày/Tháng/Năm)                           │
│  ✔ Lượng nước tưới hằng ngày (Lít hoặc m³/ngày)                                 │
│  ✔ Tổng nhu cầu nước cả vụ canh tác (m³)                                        │
│  ✔ Ước tính tổng năng suất thu hoạch (kg / Tấn)                                 │
│  ⚠ Khuyến nghị xử lý đất (Vôi/Phân hữu cơ) & Cảnh báo thời tiết                │
│                                                                                 │
└─────────────────────────────────────────────────────────────────────────────────┘
