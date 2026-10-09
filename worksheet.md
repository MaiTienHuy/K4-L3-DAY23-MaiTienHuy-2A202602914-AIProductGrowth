# Worksheet — CareLoop AI

**Họ tên:** Mai Tiến Huy · **MSSV:** 2A202602914 · **Ngày làm:** 09/10/2026  
**Lớp / Nhóm:** AI-IN-ACTION Track 1 · Nhóm DBH  
**Dự án:** CareLoop AI — AI Agent Hỗ trợ Chăm sóc Sau Xuất viện & Phòng Tái Nhập viện  

---

## Số liệu đầu vào từ Mô hình Tài chính & Cost/Job (Day 22 / 24 / 25)

| Chỉ số | Giá trị | Đơn vị / Ghi chú | Nguồn gốc |
|---|---|---|---|
| **ARPU / tháng** | **$700,00** | ~18.200.000 ₫ / tháng / bệnh viện (tính trên ~400 ca hoàn tất @ $1,75) | Day 22 Tab 4_Channel_Fit!B5 |
| **Gross Margin (GM)** | **77,95%** | Lãi gộp $1,3641 / ca hoàn tất (vùng an toàn 60%–85%) | Day 22 Tab 2_Pricing!B21 |
| **Cost/Job** | **$0,3859** | ~10.034 ₫ / bệnh nhân hoàn tất chu kỳ 30 ngày (v=$0,1395, HITL=$0,2158) | Day 22 Tab 1_Cost_Job!B66 |
| **Giá bán đề xuất (P)** | **$1,7500** | ~45.500 ₫ / completed care episode 30 ngày | Day 22 Tab 2_Pricing!B19 |
| **Breakeven Containment** | **65,90%** | Ngưỡng AI tự giải quyết tối thiểu để giữ GM ≥ 60% | Day 22 Tab 2_Pricing!B33 |
| **Containment hiện tại** | **82,00%** | Eval trên 200 ca bệnh án mẫu (biên an toàn +16,10%) | Day 22 Tab 1_Cost_Job!B10 |
| **Ngân sách CAC cho phép** | **$6.547,80** | ARPU $700 × GM 77,95% × 12 tháng payback | Day 22 Tab 4_Channel_Fit!B9 |
| **CAC Payback mục tiêu** | **12 tháng** | Chuẩn B2B SaaS SMB (Bessemer, Scaling to $100M) | Day 22 Tab 4_Channel_Fit!B8 |
| **CAC thực tế Sales-Led** | **$32.000,00** | Cost/opp $8.000 ÷ Win rate 25% (Lệch 4,89 lần → Bất khả thi) | Day 22 Tab 4_Channel_Fit!B22 |
| **CAC Partner-Led ước tính** | **$1.200,00** | Chi phí tích hợp kỹ thuật ban đầu + rev-share 25% | Day 22 GTM Strategy |
| **Runway hiện tại** | **9 tháng** | $45.000 vốn khởi điểm, burn-rate ban đầu ~$5.000/tháng | Day 22 Financial Assumptions |

---

## Trạm 1 — Loại mô hình & Bảng đèn gốc

### 1.1 Ba câu hỏi xác định mô hình theo thực tế hôm nay
1. **Ai trả tiền cho bạn?**  
   $\rightarrow$ Doanh nghiệp: Ban Giám đốc và Phòng Điều dưỡng / Vận hành CSKH của các Bệnh viện tư nhân & Phòng khám đa khoa trả tiền theo ngân sách vận hành CSKH ($700/tháng theo gói usage).
2. **Ai dùng sản phẩm?**  
   $\rightarrow$ Người dùng trực tiếp thụ hưởng giá trị vận hành là Điều dưỡng trưởng khoa ngoại/sản và nhân viên tổng đài bệnh viện (quản lý dashboard, nhận ca escalation cảnh báo nguy cơ). Bệnh nhân là người nhận tương tác thoại/tin nhắn dưới danh nghĩa bệnh viện ủy quyền.
3. **Nếu có bên trung gian (VNPT HIS), bạn có chạm được người dùng cuối không?**  
   $\rightarrow$ Kênh VNPT HIS chỉ là đối tác cung cấp nền tảng phần mềm bệnh viện và kênh phân phối kỹ thuật (Partner-Led channel), không phải người trả tiền cũng không phải end-user tiêu dùng.

**Câu chốt loại:**  
> **Chúng tôi là B2B** vì tiền đến từ ngân sách vận hành của các Bệnh viện tư nhân & Phòng khám đa khoa ($700/tháng ARPU, tính theo $1,75/bệnh nhân hoàn tất), người dùng trực tiếp vận hành quy trình và xử lý cảnh báo là Điều dưỡng trưởng & Nhân viên CSKH bệnh viện, còn kênh VNPT HIS là kênh phân phối kỹ thuật (Partner-Led channel) chứ không phải end-user tiêu dùng.

---

### 1.2 Rà soát toàn bộ bảng đèn B2B (HANDBOOK §3.2)

| # | Đèn trong B2B (§3.2) | Tầng | Đánh dấu | Số nằm ở đâu / Cần gì để đo |
|---|---|---|:---:|---|
| 1 | **Time-to-first-value (TTFV)** | Leading | ✅ | Đo được ngay: Timestamp từ lúc ký thỏa thuận pilot đến ca xuất viện đầu tiên hoàn tất tương tác D1 và xuất báo cáo lâm sàng cho Điều dưỡng trưởng (Database log). |
| 2 | **Pipeline coverage** | Leading | 🔧 | Đo được trong 2 tuần: Cần thiết lập CRM theo dõi danh sách 15 bệnh viện đang trao đổi qua giới thiệu của đội ngũ VNPT Y tế khu vực. |
| 3 | **% deal chết ở security/procurement** | Leading | 🔧 | Đo được trong 2 tuần: Cần bảng theo dõi lý do từ chối khi trình bộ hồ sơ pháp lý / bảo mật Nghị định 13/2023/NĐ-CP cho Hội đồng bệnh viện. |
| 4 | **POC → paid rate** | Operating | ✅ | Đo được ngay: Tỷ lệ chuyển đổi từ 2 bệnh viện pilot hiện tại sang hợp đồng thương mại năm (Theo dõi qua biên bản nghiệm thu pilot). |
| 5 | **Sales cycle (tuần)** | Operating | 🔧 | Đo được trong 2 tuần: Ghi nhận số tuần từ lúc demo giải pháp với Giám đốc bệnh viện đến khi ký hợp đồng chính thức (CRM tracking). |
| 6 | **Usage depth trong tài khoản** | Operating | ✅ | Đo được ngay: Số ca xuất viện thực tế được điều dưỡng bấm duyệt CareLoop AI chia cho tổng số ca xuất viện nội trú của khoa Ngoại (Log Webhook từ VNPT HIS). |
| 7 | **Chi phí triển khai ÷ ACV** | Operating | ✅ | Đo được ngay: Giờ công kỹ thuật tích hợp Webhook + đào tạo điều dưỡng tại chỗ chia cho ACV ($8.400) (Bảng chấm công Jira / Timesheet). |
| 8 | **Tập trung doanh thu** | Operating | ✅ | Đo được ngay: Doanh thu bệnh viện lớn nhất ÷ Tổng doanh thu MRR (Báo cáo tài chính nội bộ). |
| 9 | **Net Revenue Retention (NRR)** | Lagging | ❌ | Chưa đo được hôm nay: Cần bệnh viện vận hành tối thiểu 6–12 tháng để đo tỷ lệ mở rộng thêm khoa phòng (Sản, Tim mạch, Nhi) hoặc mở rộng sang cơ sở 2. |
| 10 | **Gross Margin** | Lagging | ✅ | Đo được ngay: (Doanh thu − chi phí API LLM Haiku/Voice − Telephony SIP Trunk − HITL ca trực) ÷ Doanh thu (Báo cáo P&L hàng tháng). |
| 11 | **CAC Payback** | Lagging | ❌ | Chưa đo được hôm nay: Cần tối thiểu 6–12 tháng theo dõi dòng tiền thực thu từ bệnh viện sau khi trừ chi phí hoa hồng kênh đối tác 25%. |

---

## Trạm 2 — Cây 3 tầng & Thẻ đèn

**NORTH STAR METRIC:**  
> **Time-to-first-value (TTFV)** — Hiện tại: **21 ngày** — Mục tiêu: **< 14 ngày**  
> *(Lý do: Trong B2B y tế, deal pilot không chết vì giá mà chết ở khoảng trống tích hợp Webhook HIS và sự e ngại của điều dưỡng. TTFV < 14 ngày là tín hiệu quyết định tỷ lệ POC → Paid và ngăn ngừa hủy bỏ hợp đồng).*

### Bảng 7 thẻ đèn phân tầng chặt chẽ

| # | Tầng | Đèn | Định nghĩa (Đếm gì · **KHÔNG** đếm gì) | Công thức | Nhịp · Ai lấy số | Báo trước cho |
|---|:---:|---|---|---|---|---|
| **1** | **L** | **Time-to-first-value (TTFV)** ⭐ *(North Star)* | Số ngày từ khi Bệnh viện ký thỏa thuận pilot/hợp đồng đến ngày ca bệnh nhân đầu tiên xuất viện hoàn tất tương tác D1 qua AI và tạo ra báo cáo lâm sàng tự động cho điều dưỡng. **Không** đếm các ngày chờ thủ tục hành chính nội bộ của bệnh viện trước khi ký hoặc các ca test giả lập của kỹ sư IT. | $Ngày_{FirstReport} - Ngày_{Signed}$ | Mỗi khách mới · Mai Tiến Huy (Product Lead) | Tỷ lệ chuyển đổi POC → Paid (Tầng 2 - Operating) |
| **2** | **L** | **Tỷ lệ phản hồi tương tác D1–D3 (Patient Engagement)** | % bệnh nhân xuất viện trả lời ít nhất 1 câu hỏi kiểm tra triệu chứng qua Zalo/Voicebot trong vòng 72 giờ đầu. **Không** đếm các cuộc gọi máy bận, số điện thoại sai hoặc bệnh nhân từ chối ngay khi bắt máy. | $\frac{\text{Số BN phản hồi check-in D1-D3}}{\text{Tổng số ca kích hoạt hợp lệ}} \times 100\%$ | Hằng ngày · Log tự động hệ thống | Containment Rate & Hoàn tất chu kỳ 30 ngày (Tầng 2 - Operating) |
| **3** | **O** | **Containment Rate (AI tự giải quyết an toàn)** ⚡ *(Đèn chi phí AI)* | % ca bệnh nhân được AI theo dõi, phân tầng nguy cơ an toàn suốt chu kỳ 30 ngày mà không cần chuyển điều dưỡng trực escalation can thiệp. **Không** đếm các ca bệnh nhân từ chối tham gia ngay từ mốc D1 hoặc các cuộc gọi test nội bộ. | $\frac{\text{Số ca AI tự giải quyết an toàn}}{\text{Tổng số ca theo dõi hoàn tất}} \times 100\%$ | Hằng tuần · AI Triage Engine Log | Chi phí can thiệp HITL & Gross Margin (Tầng 3 - Lagging) |
| **4** | **O** | **Tỷ lệ chuyển đổi Pilot → Paid (POC → Paid Rate)** | % bệnh viện tham gia pilot 30 ngày chuyển sang ký hợp đồng thương mại trả phí chính thức (hoặc gia hạn). **Không** đếm các thỏa thuận MOU hợp tác nghiên cứu phi thương mại. | $\frac{\text{Số BV ký hợp đồng chính thức}}{\text{Tổng số BV hoàn thành pilot}} \times 100\%$ | Hằng tháng / sau mỗi pilot · Báo cáo thương mại | Doanh thu MRR và Runway (Tầng 3 - Lagging) |
| **5** | **O** | **Mức độ thâm nhập khoa phòng (Usage Depth)** | % số ca bệnh nhân xuất viện tại các khoa mục tiêu (Ngoại, Sản) thực sự được điều dưỡng kích hoạt CareLoop AI qua VNPT HIS so với tổng số ca xuất viện thực tế của các khoa đó. **Không** đếm bệnh nhân chuyển viện hoặc tử vong nội viện. | $\frac{\text{Số ca kích hoạt CareLoop AI}}{\text{Tổng số ca ra viện đủ điều kiện}} \times 100\%$ | Hằng tuần · Log Webhook VNPT HIS | ARPU / bệnh viện & NRR (Tầng 3 - Lagging) |
| **6** | **O** | **Chi phí triển khai ÷ ACV** | Tổng chi phí nhân sự kỹ thuật cấu hình Webhook và đào tạo điều dưỡng cho 1 bệnh viện chia cho Giá trị hợp đồng năm đầu tiên (ACV = $8.400). **Không** tính chi phí phát triển tính năng R&D dùng chung cho toàn bộ sản phẩm. | $\frac{\text{Giờ công onboarding} \times \$15 + \text{Chi phí tích hợp}}{\text{ACV (\$8.400)}} \times 100\%$ | Mỗi khách mới · Tech Lead | Thời gian hoàn vốn CAC Payback (Tầng 3 - Lagging) |
| **7** | **G** | **Gross Margin (Tỷ suất lợi nhuận gộp)** | Tỷ suất lợi nhuận gộp sau khi trừ toàn bộ chi phí API LLM/Voice, cước viễn thông SIP, hạ tầng cloud và chi phí điều dưỡng trực ca đêm/escalation (HITL). **Không** trừ chi phí bán hàng, chi phí R&D và chi phí quản lý doanh nghiệp. | $\frac{\text{Doanh thu} - \text{COGS trực tiếp}}{\text{Doanh thu}} \times 100\%$ | Hằng tháng / Hằng quý · Kế toán quản trị | Bảng điểm tài chính cuối cùng (Bảo vệ Runway) |

> **Đèn chi phí AI là đèn số 3 (Containment Rate):** Đo lường tỷ lệ ca AI tự giải quyết an toàn. Trong kiến trúc Biến thể B (CareLoop AI gánh chi phí điều dưỡng trực escalation $9/giờ), mỗi ca escalate tốn 6 phút điều dưỡng = $0,90. Nếu Containment tụt, chi phí HITL sẽ tăng vọt và ăn sạch Gross Margin trước khi xuất hiện trên báo cáo tài chính cuối tháng.

---

## Trạm 3 — Ngưỡng có nguồn & Phụ lục [MH]

### 3.1 Bảng ngưỡng vận hành 🟢 🟡 🔴

| # | Đèn | 🟢 Xanh | 🟡 Vàng | 🔴 Đỏ | Nguồn | Lý do thiết lập ngưỡng · Ngày kiểm tra nếu [BM] |
|---|---|:---:|:---:|:---:|:---:|---|
| **1** | **Time-to-first-value (TTFV)** ⭐ | < 14 ngày | 14 – 28 ngày | > 28 ngày | **[MH]** | Suy từ chu kỳ pilot 30 ngày của bệnh viện: nếu sau 28 ngày chưa có ca đầu tiên thấy giá trị, bệnh viện sẽ không nghiệm thu gia hạn (xem Phụ lục [MH] 2). |
| **2** | **Tỷ lệ phản hồi D1–D3 (Engagement)** | ≥ 80% | 65% – 79% | < 65% | **[TB]** | Baseline đo thử trên 200 bệnh nhân mẫu đạt 78,5%; nếu < 65% bệnh nhân không tham gia thì dữ liệu sàng lọc biến chứng bị gãy chuỗi (đo tiếp chu kỳ 2 vào 30/10/2026). |
| **3** | **Containment Rate** ⚡ *(Chi phí AI)* | ≥ 80% | 66% – 79% | < 65,9% | **[MH]** | Suy ngược từ công thức Breakeven Containment: tại mức < 65,9%, chi phí escalation HITL sẽ kéo Gross Margin xuống dưới 60% (xem Phụ lục [MH] 1). |
| **4** | **Tỷ lệ chuyển đổi POC → Paid** | ≥ 50% | 35% – 49% | < 35% | **[BM]** | Benchmark phần mềm B2B AI đạt trung bình ~50% (tăng từ ~36% năm 2025). *(Nguồn: ICONIQ State of Go-to-Market 2026, kiểm tra ngày 2026-10-09).* |
| **5** | **Mức độ thâm nhập (Usage Depth)** | ≥ 60% | 30% – 59% | < 30% | **[BM]** | Quy ước chuẩn ngành SaaS B2B về mức độ thâm nhập workflow trong tài khoản; <30% là tín hiệu báo trước nguy cơ churn hợp đồng. *(Nguồn: HANDBOOK §3.2, kiểm tra ngày 2026-10-09).* |
| **6** | **Chi phí triển khai ÷ ACV** | < 15% | 15% – 25% | > 25% | **[MH]** | Suy từ mô hình tài chính: với ACV $8.400 và CAC ngân sách $6.548, chi phí triển khai kỹ thuật vượt quá 25% ($2.100) sẽ làm thời gian hoàn vốn vượt 12 tháng (xem Phụ lục [MH] 3). |
| **7** | **Gross Margin** | ≥ 70% | 55% – 69% | < 53% | **[BM]** | Benchmark trung vị Gross Margin của các công ty AI-native năm 2026E đạt 53%; dưới 53% là nguy cơ cạn kiệt dòng tiền. *(Nguồn: ICONIQ State of AI 2026, kiểm tra ngày 2026-10-09).* |

---

### 3.2 Phụ lục [MH] — Các phép tính suy ngược từ mô hình tài chính

#### [MH] 1 — Ngưỡng đỏ Containment Rate (Đèn chi phí AI sống còn)
```
Đầu vào từ Mô hình Kinh tế CareLoop AI (Day 22 Tab 1_Cost_Job & 2_Pricing):
- Giá bán P = $1,75 / bệnh nhân hoàn tất chu kỳ 30 ngày
- Biến phí công nghệ / ca thử nghiệm v = $0,1395 (LLM Haiku cached, Deepgram STT, ElevenLabs TTS, SIP trunk, retry)
- Chi phí kiểm định QA nội bộ q = $0,0150 / ca thử nghiệm (5% mẫu × 2 phút × $9/giờ)
- Chi phí can thiệp điều dưỡng escalation e = $0,9000 / ca bất thường (6 phút trực × $9/giờ điều dưỡng)
- Gross Margin tối thiểu mục tiêu GM_target = 60,0% (biên an toàn sống còn)

Phép tính Breakeven Containment (R):
Điều kiện để Gross Margin ≥ 60%:
  Cost/Job = [v + q + e × (1 − R)] / R ≤ P × (1 − GM_target)
  v + q + e − e × R ≤ R × P × (1 − GM_target)
  R × [P × (1 − GM_target) + e] ≥ v + q + e
  R ≥ (v + q + e) / [P × (1 − GM_target) + e]

Thay số:
  Tử số = 0,1395 + 0,0150 + 0,9000 = $1,0545
  Mẫu số = 1,75 × (1 − 0,60) + 0,9000 = 0,7000 + 0,9000 = $1,6000
  R_breakeven = 1,0545 / 1,6000 = 0,6590625 ≈ 65,90%

Kết quả:
→ 🟢 Xanh: Containment ≥ 80,0% (Gross Margin đạt ~77,95%)
→ 🟡 Vàng: Containment từ 66,0% đến 79,9% (Gross Margin dao động 60%–77%)
→ 🔴 Đỏ: Containment < 65,9% (Gross Margin tụt dưới 60%, mô hình bắt đầu gãy tài chính)
```

#### [MH] 2 — Ngưỡng đỏ Time-to-first-value (TTFV)
```
Đầu vào từ Hợp đồng Pilot B2B & Quy trình Bệnh viện:
- Thời hạn hợp đồng pilot tiêu chuẩn: 30 ngày (1 tháng)
- Chu kỳ đánh giá lâm sàng tối thiểu của Hội đồng khoa: 14 ngày (2 tuần) để xem đủ dữ liệu 1 cohort bệnh nhân xuất viện
- Thời gian trễ để ca bệnh nhân đầu tiên hoàn thành check-in D1: 2 ngày sau xuất viện

Phép tính:
- Thời gian tối đa cho phép triển khai kỹ thuật và chạy ca đầu tiên:
  TTFV_max = Thời hạn pilot (30 ngày) − Thời gian thu thập đủ báo cáo lâm sàng (2 ngày kiểm tra D1) = 28 ngày.
- Nếu TTFV > 28 ngày, bệnh viện kết thúc thời gian pilot 30 ngày mà chưa nhìn thấy bất kỳ kết quả lâm sàng nào trên thực tế → Chắc chắn từ chối ký hợp đồng chính thức.

Kết quả:
→ 🟢 Xanh: TTFV < 14 ngày (kịp hoàn tất cấu hình trong 2 tuần đầu, còn trọn vẹn 2 tuần đánh giá lâm sàng)
→ 🟡 Vàng: TTFV từ 14 đến 28 ngày (nguy cơ chậm tiến độ, cần họp khẩn với IT bệnh viện)
→ 🔴 Đỏ: TTFV > 28 ngày (thất bại pilot, vi phạm mốc thời gian nghiệm thu)
```

#### [MH] 3 — Ngưỡng đỏ Chi phí triển khai ÷ ACV
```
Đầu vào từ Mô hình Kênh Partner-Led (Day 22 Tab 4_Channel_Fit):
- ACV (Giá trị hợp đồng hàng năm của 1 bệnh viện) = ARPU $700 × 12 tháng = $8.400
- Gross Margin mục tiêu = 77,95% → Lãi gộp hàng năm = $8.400 × 77,95% = $6.547,80
- Thời gian hoàn vốn CAC Payback tối đa cho phép = 12 tháng
- Chi phí hoa hồng chia sẻ kênh Partner VNPT HIS = 25% doanh thu = $2.100 / năm
- Ngân sách tối đa còn lại cho chi phí triển khai kỹ thuật Onboarding tại chỗ:
  Ngân sách = Lãi gộp hàng năm ($6.547,80) − Chi phí hoa hồng kênh ($2.100) = $4.447,80 / năm.
  Tuy nhiên, để bảo đảm tỷ lệ LTV/CAC ≥ 3, tổng chi phí CAC (gồm cả Onboarding) không được vượt quá $2.100 / khách hàng.

Phép tính tỷ lệ chi phí triển khai tối đa:
  Tỷ lệ tối đa = $2.100 ÷ $8.400 = 25,0% ACV
  (Tương đương tối đa 140 giờ công kỹ sư @ $15/giờ)

Kết quả:
→ 🟢 Xanh: Chi phí triển khai < 15% ACV (< $1.260 / bệnh viện, tương đương < 84 giờ công)
→ 🟡 Vàng: Chi phí triển khai từ 15% đến 25% ACV ($1.260 – $2.100)
→ 🔴 Đỏ: Chi phí triển khai > 25% ACV (> $2.100, mô hình dịch vụ ăn mòn biên lợi nhuận phần mềm)
```

---

## Trạm 4 — 5 Luật Quyết định Vận hành

*(Ký hiệu ⏹ = Luật dừng hành động đang làm để bảo vệ nguồn lực)*

### Luật 1 · ⏹ Luật dừng mở rộng pilot khi triển khai tắc nghẽn
> **NẾU** Time-to-first-value (TTFV) > 28 ngày  
> **TRÊN** 2 bệnh viện pilot liên tiếp  
> **THÌ** đóng băng toàn bộ hoạt động tiếp cận bệnh viện mới trong 3 tuần, cử Tech Lead cắm chốt tại bệnh viện để đóng gói module Webhook một chạm chuẩn hóa trên VNPT HIS  
> **KHÔNG THÌ** không được ký thêm biên bản ghi nhớ pilot mới để làm đẹp báo cáo phễu bán hàng.

### Luật 2 · ⏹ Luật dừng tính năng khi tỷ lệ AI tự động tụt dốc (Bảo vệ chi phí AI)
> **NẾU** Containment Rate < 65,9%  
> **TRONG** 2 tuần liên tiếp  
> **VÀ** tổng số ca theo dõi trong kỳ ≥ 150 bệnh nhân  
> **THÌ** dừng toàn bộ việc phát triển tính năng mới trên roadmap, chuyển toàn bộ nguồn lực engineering rà soát lại prompt triage phân tầng và kịch bản hội thoại để đưa containment trở lại ≥ 80%  
> **KHÔNG THÌ** không được tăng số giờ điều dưỡng trực ca ngoài giờ để gánh ca lỗi mà không sửa tận gốc thuật toán.

### Luật 3 · Luật xử lý khi bệnh nhân không tương tác (Patient Engagement)
> **NẾU** Tỷ lệ phản hồi tương tác D1–D3 < 65%  
> **TRONG** 1 cohort xuất viện (tối thiểu 50 bệnh nhân)  
> **THÌ** chuyển ngay kênh liên lạc mặc định từ tin nhắn Zalo sang cuộc gọi thoại Voicebot tự động trong khung giờ vàng 19:30 – 20:30, đồng thời phối hợp Điều dưỡng trưởng dán poster hướng dẫn quét mã Zalo ngay tại bàn nhận thuốc ra viện  
> **KHÔNG THÌ** không được đổ lỗi cho bệnh nhân lớn tuổi khó tiếp cận công nghệ rồi bỏ qua mốc kiểm tra triệu chứng.

### Luật 4 · ⏹ Luật dừng giảm giá khi tỷ lệ chuyển đổi pilot thấp
> **NẾU** Tỷ lệ chuyển đổi POC → Paid < 35%  
> **TRÊN** 3 đợt pilot gần nhất  
> **THÌ** dừng toàn bộ hoạt động chào bán 2 tuần để hoàn thiện lại bộ Evidence Pack (cập nhật Báo cáo Pilot lâm sàng chứng minh số giờ điều dưỡng tiết kiệm và rà soát lại tiêu chí chọn bệnh viện mục tiêu)  
> **KHÔNG THÌ** không được giảm giá bán xuống dưới mức giá sàn $1,1578 hoặc miễn phí dùng thử kéo dài để cố giữ chân khách hàng.

### Luật 5 · Luật chuẩn hóa khi chi phí triển khai phình to
> **NẾU** Chi phí triển khai ÷ ACV > 25%  
> **TRÊN** 2 hợp đồng bệnh viện liên tiếp  
> **THÌ** chuyển đổi toàn bộ quy trình tích hợp sang cổng Self-serve API Connector có tài liệu mẫu và từ chối các yêu cầu tùy biến giao diện riêng biệt của bệnh viện  
> **KHÔNG THÌ** không được nhận thêm các yêu cầu chỉnh sửa phần mềm theo đặc thù từng khoa phòng mà không tính thêm phí dịch vụ tích hợp (Professional Services Fee).

---
