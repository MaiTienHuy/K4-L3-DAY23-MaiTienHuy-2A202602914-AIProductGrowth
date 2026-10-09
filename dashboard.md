# OPERATING DASHBOARD — CareLoop AI

**Loại mô hình:** B2B · **Cập nhật:** 09/10/2026 · **Mai Tiến Huy – MSSV: 2A202602914**  
**NORTH STAR:** Time-to-first-value (TTFV) — Hiện tại: **21 ngày** — Mục tiêu: **< 14 ngày**

---

### Đèn báo sớm (Leading — theo dõi hằng ngày / hằng tuần)

| Đèn | Hiện tại | Ngưỡng 🟢 / 🟡 / 🔴 | Nguồn | Báo trước cho |
|---|:---:|:---:|:---:|---|
| **Time-to-first-value (TTFV)** ⭐ | 21 ngày | 🟢 <14 ngày · 🟡 14–28 ngày · 🔴 >28 ngày | [MH] | Tỷ lệ chuyển đổi POC → Paid |
| **Phản hồi tương tác D1–D3** | 78,5% | 🟢 ≥80% · 🟡 65–79% · 🔴 <65% | [TB] | Containment Rate & Hoàn tất chu kỳ |

---

### Đèn vận hành (Operating — theo dõi hằng tuần / hằng tháng)

| Đèn | Hiện tại | Ngưỡng 🟢 / 🟡 / 🔴 | Nguồn | Báo trước cho |
|---|:---:|:---:|:---:|---|
| **Containment Rate** ⚡ *(Chi phí AI)* | 82,0% | 🟢 ≥80% · 🟡 66–79% · 🔴 <65,9% | [MH] | Chi phí HITL escalation & Gross Margin |
| **Tỷ lệ chuyển đổi POC → Paid** | 50,0% | 🟢 ≥50% · 🟡 35–49% · 🔴 <35% | [BM] | Doanh thu MRR & Thời gian Runway |
| **Usage Depth (Thâm nhập khoa)** | 62,5% | 🟢 ≥60% · 🟡 30–59% · 🔴 <30% | [BM] | ARPU / Bệnh viện & Tỷ lệ gia hạn |
| **Chi phí triển khai ÷ ACV** | 16,7% | 🟢 <15% · 🟡 15–25% · 🔴 >25% | [MH] | Thời gian hoàn vốn CAC Payback |

---

### Đèn kết quả (Lagging — theo dõi hằng quý)

| Đèn | Hiện tại | Ngưỡng 🟢 / 🟡 / 🔴 | Nguồn | Ý nghĩa kiểm soát |
|---|:---:|:---:|:---:|---|
| **Gross Margin** | 77,9% | 🟢 ≥70% · 🟡 55–69% · 🔴 <53% | [BM] | Bảng điểm kinh tế đơn vị & An toàn tài chính |

---

### 5 luật quyết định (⏹ = luật dừng)

1. ⏹ **NẾU** TTFV > 28 ngày **TRÊN** 2 bệnh viện pilot liên tiếp **THÌ** đóng băng toàn bộ tiếp cận khách hàng mới 3 tuần để chuẩn hóa module Webhook một chạm trên VNPT HIS **KHÔNG THÌ** không được ký thêm pilot mới để làm đẹp pipeline.
2. ⏹ **NẾU** Containment Rate < 65,9% **TRONG** 2 tuần liên tiếp **VÀ** cỡ mẫu ≥150 bệnh nhân **THÌ** dừng toàn bộ roadmap tính năng mới để tập trung rà soát prompt triage phân tầng đưa containment về ≥80% **KHÔNG THÌ** không được tăng giờ điều dưỡng trực để gánh lỗi AI.
3. **NẾU** Phản hồi D1–D3 < 65% **TRONG** 1 cohort xuất viện (≥50 ca) **THÌ** chuyển kênh liên lạc mặc định sang Voicebot tự động khung giờ 19:30–20:30 và dán poster QR Zalo tại quầy phát thuốc **KHÔNG THÌ** không được đổ lỗi bệnh nhân cao tuổi rồi bỏ qua ca theo dõi.
4. ⏹ **NẾU** POC → Paid < 35% **TRÊN** 3 đợt pilot gần nhất **THÌ** dừng chào bán 2 tuần để hoàn thiện Evidence Pack chứng minh số giờ điều dưỡng tiết kiệm **KHÔNG THÌ** không được giảm giá dưới giá sàn $1,1578 hoặc kéo dài dùng thử miễn phí.
5. **NẾU** Chi phí triển khai ÷ ACV > 25% **TRÊN** 2 hợp đồng liên tiếp **THÌ** chuyển quy trình tích hợp sang cổng Self-serve API Connector có tài liệu chuẩn **KHÔNG THÌ** không nhận tùy biến tính năng riêng mà không thu phí Professional Services.

---

### Cổng gác 90 ngày

| Ngày | Metric gác cổng duy nhất | Ngưỡng qua cổng | Bằng chứng vật lý bắt buộc | Quyết định nếu trượt |
|:---:|---|:---:|---|:---:|
| **30** | **Time-to-first-value (TTFV)** | ≤ 14 ngày | Log hệ thống xác nhận 1 ca xuất viện hoàn tất D1 và xuất báo cáo lâm sàng cho BV pilot | **FIX** *(Chuẩn hóa Webhook HIS 1 lần)* |
| **60** | **Containment Rate** ⚡ | ≥ 80% | Báo cáo kiểm định AI Triage trên ≥ 300 ca xuất viện thật có xác nhận của Điều dưỡng trưởng | **PIVOT** *(Đổi sang model phân tầng triệu chứng mới)* |
| **90** | **Tỷ lệ chuyển đổi POC → Paid** | ≥ 50% | Hợp đồng thương mại trả tiền chính thức đã ký từ tối thiểu 1/2 bệnh viện pilot | **KILL** *(Dừng dự án, thanh lý nguồn lực)* |

**KILL CRITERIA:** Sau 90 ngày (đến ngày 10/01/2027), nếu không có ít nhất 1 bệnh viện pilot ký hợp đồng thương mại trả phí chính thức với mức giá ≥ $1,50/bệnh nhân, hoặc Containment Rate sau 1 lần FIX vẫn < 65,9%, CareLoop AI sẽ dừng hoạt động dự án để bảo toàn vốn.

**CHƯA ĐO ĐƯỢC:** 
- **Net Revenue Retention (NRR):** Cần bệnh viện vận hành thực tế tối thiểu 6 tháng để đo tỷ lệ mở rộng thêm khoa phòng; dự kiến có số liệu baseline đầu tiên vào tháng 04/2027.
- **CAC Payback:** Cần theo dõi dòng tiền thanh toán thực tế sau khi trừ 25% hoa hồng đối tác kênh trong 2 quý; dự kiến có số liệu chốt vào ngày 31/03/2027.
