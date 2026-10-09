# CareLoop AI — Operating Dashboard (Lab Day 23)

- **Họ và tên:** Mai Tiến Huy  
- **Mã học viên:** 2A202602914  
- **Lớp / Nhóm:** AI-IN-ACTION Track 1 · Nhóm DBH  
- **Tên sản phẩm:** CareLoop AI — AI Agent Hỗ trợ Chăm sóc Sau Xuất viện & Phòng Tái Nhập viện  
- **Loại mô hình:** **B2B** (Bán cho Bệnh viện tư nhân & Phòng khám đa khoa qua kênh Partner-Led VNPT HIS)  
- **Ngày thực hiện:** 09/10/2026  

---

## 1. Câu chốt loại mô hình

> **Chúng tôi là B2B** vì tiền đến từ ngân sách vận hành CSKH & Điều dưỡng của các Bệnh viện tư nhân & Phòng khám đa khoa ($700/tháng ARPU, tính theo $1,75/bệnh nhân hoàn tất), người dùng trực tiếp vận hành quy trình và xử lý cảnh báo là Điều dưỡng trưởng & Nhân viên CSKH bệnh viện, còn kênh VNPT HIS là kênh phân phối kỹ thuật (Partner-Led channel) chứ không phải end-user tiêu dùng.

---

## 2. Danh mục Hồ sơ Nộp bài (Deliverables)

| Tệp tin | Vai trò & Mô tả | Trạng thái |
|---|---|:---:|
| [**`dashboard.md`**](dashboard.md) | Bản Operating Dashboard 1 trang hoàn chỉnh (Trạm 5) với 7 thẻ đèn, 5 luật quyết định, 3 cổng gác 90 ngày. | ✅ Hoàn thành |
| [**`worksheet.md`**](worksheet.md) | Bằng chứng chi tiết Trạm 1–4: rà soát bảng đèn B2B, thẻ đèn 3 tầng, bảng ngưỡng có nguồn, 3 phép tính [MH], 5 luật quyết định. | ✅ Hoàn thành |
| [**`dashboard.pdf`**](dashboard.pdf) | Bản in PDF chuẩn 2 trang: Trang 1 là Operating Dashboard, Trang 2 là Phụ lục phép tính [MH]. | ✅ Hoàn thành |
| [**`README.md`**](README.md) | Giới thiệu dự án, thông tin tác giả, câu chốt loại và chỉ số vàng. | ✅ Hoàn thành |

---

## 3. Bản đồ Số liệu Cốt lõi (Golden Metrics)

```
[ Cost/Job: $0,3859 ] ─── (3× Giá sàn: $1,1578) ─── [ Giá bán: $1,7500 ] ─── [ Giá trần: $3,0000 ]
         │                                                      │
   Chia cho 820 completed                                Gross Margin: 77,95%
 (v = $0,1395, HITL = $177/tháng)                      (Vùng an toàn: 60% ≤ GM ≤ 85%)
         │                                                      │
Breakeven Containment: 65,90% ◄──────────────────────── Eval hiện tại: 82,00% (+16,10%)
```

- **North Star Metric:** Time-to-first-value (TTFV) — Hiện tại: **21 ngày** — Mục tiêu: **< 14 ngày**.
- **Đèn chi phí AI:** Containment Rate (Tỷ lệ AI tự giải quyết an toàn, ngưỡng đỏ sống còn: < 65,9%).
- **Ngân sách CAC cho phép:** $6.547,80 (Payback mục tiêu 12 tháng theo chuẩn SaaS SMB Bessemer).
- **Runway:** 9 tháng ($45.000 vốn khởi điểm, burn rate ~$5.000/tháng).
