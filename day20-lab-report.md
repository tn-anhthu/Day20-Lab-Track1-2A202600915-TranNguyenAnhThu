# Day 20 Lab — Retention, Engagement & Habit Loop

**Sản phẩm:** Academic Research Assistant / Literature Review AI

**Tính năng kế thừa từ Day 18:** Claim Verification & Routing (Step ⑧⑨)

**Persona:** Sinh viên/học viên đang viết literature review, dùng AI sinh content theo từng theme và cần verify trước khi nộp/bảo vệ.

> Lưu ý: Ngày 20 không chọn lại đề bài, không tạo sản phẩm mới. Toàn bộ phần dưới đây tiếp tục trực tiếp trên sản phẩm, scenario và prototype đã hoàn thiện ở Day 18.

---

## Bài 1 — Hành vi tự nhiên và Use Case: Customer Retention Canvas

| Thành phần | Nội dung |
|---|---|
| **The Problem** | "Tôi để AI viết content cho từng theme trong bài literature review, nhưng tôi không biết câu nào trong đó thực sự có nguồn đủ tin cậy — nếu tự dò lại từng câu thì rất mất thời gian, mà nộp bài có claim sai nguồn thì rủi ro academic integrity." |
| **The Persona** | Sinh viên/học viên đang viết literature review cho một đề tài cụ thể (khoá luận, báo cáo nghiên cứu, bài tổng quan), dùng AI Research Assistant để sinh content theo từng theme và cần verify trước khi nộp/bảo vệ. Đã có kinh nghiệm dùng AI viết nhưng chưa quen tự tra cứu học thuật sâu (Semantic Scholar, arXiv). |
| **Anti-persona** | (1) Người dùng AI chỉ để đọc/tóm tắt nhanh, không tự viết bài. (2) Researcher/giáo sư đã có quy trình peer review hoặc trợ lý riêng. |
| **The Why** | Muốn nộp/bảo vệ bài viết mà tự tin từng claim có nguồn xác thực, tránh rủi ro academic integrity, không phải tự dò nguồn tay từng câu. |
| **The Alternative** | Tự đọc lại + Ctrl+F tra chéo; search tay trên Google Scholar/Semantic Scholar; hỏi giảng viên/bạn học; hoặc bỏ qua, nộp không kiểm tra kỹ. |
| **The Frequency** | Project-based — nhiều lần/ngày trong giai đoạn tích cực viết một đề tài (mỗi khi AI sinh xong một theme mới); giảm mạnh gần về 0 khi đề tài hoàn thành/nộp, cho tới đề tài tiếp theo (vài tuần–vài tháng sau). Khớp với ví dụ "lập kế hoạch dự án" trong đề bài: tần suất cao trong một cửa sổ thời gian active, gần như biến mất ngoài cửa sổ đó. |

---

## Bài 2 — Từ Use Case tới Retention Metric

**Core Action:** User resolve một claim được AI flag cần xem lại — sau khi xem evidence/nguồn, chọn một hành động có cơ sở (Giữ nguyên / Sửa / Xóa / Khôi phục / Đồng ý / Không đồng ý). Chỉ xem hoặc mở rộng nguồn (expand evidence) **không** tính là core action — vì đó là hành vi quan sát thuần, chưa tạo ra quyết định có giá trị.

**Active User:** "Một user được tính là active trong một buổi viết (session) khi họ resolve được ít nhất 1 claim được flag, trong cùng phiên mở ClaimVerifier cho một theme."

**Retention Metric — Project Return Rate:** % user quay lại dùng ClaimVerifier khi bắt đầu đề tài/bài viết tiếp theo, sau khi đã tạm dừng hoạt động ≥ vài tuần. Không dùng D1/D7/D30 vì hành vi không có tần suất daily/weekly tự nhiên — nó vận hành theo "đề tài", nên metric retention phải khớp với chu kỳ đó.

---

## Bài 3 — Onboarding tới First Core Action

### Current-State Journey (trước khi sửa)
Entry point (vào màn ClaimVerifier sau Step ⑦) → Onboarding step 1 (click "Bắt đầu verify") → Onboarding step 2 (progress bar ~1.5s) → Result screen (header dài + legend 5 màu + claim list xen lẫn auto-kept trước actionable) → First core action (resolve claim Partially Supported) → (chưa có Aha moment rõ ràng).

### Friction Audit

| Bước | Nhãn | Vì sao |
|---|---|---|
| Nút "Bắt đầu verify" thủ công | Remove | Đây là demo artifact; verify nên tự chạy ngay sau Step ⑦, không cần user bấm |
| Progress bar | Keep | AI cần thời gian xử lý thật, nhưng nên tự chạy không cần click khởi động |
| Header giải thích 4 mức | Simplify | Rút còn 1 dòng, chi tiết đầy đủ chuyển vào icon "ⓘ" |
| Legend 5 màu | Delay | Chỉ giải thích badge khi user gặp lần đầu (contextual disclosure) |
| Thứ tự claim list (auto-kept trước actionable) | Simplify | Đẩy claim cần xử lý lên đầu danh sách |
| Resolved-tag tĩnh | Simplify | Thêm chỉ số tiến độ "x/y claim cần xem đã xử lý" |

### Current-State metrics (ước tính từ prototype, chưa có tracking thật)

| Chỉ số | Giá trị ước tính |
|---|---|
| Số bước tới first core action | 2 click + 1 lần chờ ~1.5s |
| Số trường thông tin cần điền | 0 |
| Số permission cần cấp | 0 |
| TTFCA (Time to First Core Action) ước tính | ~25–30s |
| TTV (Time to Value) ước tính | ~tương đương TTFCA, chưa tách Aha moment riêng |
| Điểm drop-off cao nhất | Đoạn giải thích dài ở đầu màn + việc user phải tự dò claim nào cần xử lý |

### Redesigned Journey
Vào màn (verify auto-run ngay) → 1 dòng giải thích ngắn (chi tiết đầy đủ nằm trong icon ⓘ) → claim cần xử lý xuất hiện đầu danh sách → **First Core Action** (resolve claim đầu tiên) → Evidence of value ("✓ Đã xử lý 1/3 claim cần xem") → khi resolve hết toàn bộ claim cần xem trong theme → **Aha moment/Activation banner** ("✅ Theme này đã verify xong — bạn có thể tự tin đưa vào bài") → CTA sang theme tiếp theo / Step ⑨.

**Activation vs First Core Action:**
- *First Core Action* = resolve 1 claim (atomic event, dùng để định nghĩa Active User và đo TTFCA).
- *Activation* = resolve **toàn bộ** claim cần xem trong theme đầu tiên — đây là full value moment (cả theme đáng tin để đưa vào bài viết). Hai khái niệm tách biệt có chủ đích: core action đo tốc độ bắt đầu tương tác, activation đo việc user nhận được giá trị hoàn chỉnh.

**Recovery path:** Khôi phục claim bị tự xóa (Screen 3, nút "Khôi phục") — giữ nguyên, đã đáp ứng yêu cầu vì route user trở lại hành trình (không kết thúc ở error screen).

### Before/After Comparison

| Tiêu chí | Before | After | Vì sao thay đổi |
|---|---|---|---|
| Số bước tới core action | 2 click | 1 click | Bỏ nút "Bắt đầu verify" thủ công, verify auto-run |
| Permission trước core action | 0 | 0 | Không đổi |
| TTFCA | ~25–30s | ~8–10s | Header rút ngắn, claim cần xử lý đưa lên đầu danh sách |
| Evidence of value | Không có | Có (tiến độ x/y + banner hoàn tất) | Củng cố cảm giác tiến triển và Aha moment |
| Recovery path | Có (Khôi phục) | Giữ nguyên | Đã đáp ứng yêu cầu, không cần thay đổi |

---

## Bài 4 — Measurement Ladder và North Star Metric

### Measurement Ladder
- **Marketing/Traffic:** ngoài phạm vi lab này.
- **Visitor → Activation:** Activation Rate.
- **Core Action:** Core Action Completion Rate, Time to First Core Action (TTFCA).
- **Retention:** Project Return Rate.
- **Revenue:** ngoài phạm vi lab này (sản phẩm hiện tại chưa có mô hình thu phí trong scope của lab).

### North Star Metric
**NSM: "Số theme đạt Activation (verify hoàn chỉnh — toàn bộ claim cần xem đã được resolve) mỗi tuần, tính trên toàn bộ user."** (Weekly Activated Themes)

**Input Metrics (tối đa 3):**
1. Activation Rate
2. Core Action Completion Rate
3. Time to First Core Action (TTFCA)

**Kết quả kinh doanh/khách hàng trung-dài hạn:** Project Return Rate tăng → customer value: tiết kiệm thời gian kiểm tra nguồn + tăng sự tự tin về academic integrity khi nộp/bảo vệ bài.

**Leading vs Lagging:**
- Leading: Activation Rate, Core Action Completion Rate, TTFCA, và NSM bản thân nó.
- Lagging: Project Return Rate, niềm tin academic-integrity dài hạn (khó đo trực tiếp, thể hiện qua hành vi quay lại).

**Trade-off cần lưu ý:** Giảm số claim bị flag để hỏi user (tức tăng tỷ lệ tự động Act) sẽ làm NSM tăng nhanh hơn (nhiều theme "đạt activation" hơn vì ít việc phải resolve) nhưng đồng thời tăng rủi ro claim sai nguồn lọt qua mà không được review. Vì vậy **không nên hạ ngưỡng Ask** trong cơ chế 3-tier verification (Day 18) chỉ để đẩy NSM lên — NSM phải phản ánh giá trị thật, không phải vanity metric đạt được bằng cách giảm chất lượng review.

---

## Bài 5 — Nature, Nurture và Habit Loop

### Nature vs Nurture

| Nội dung | Trả lời |
|---|---|
| Natural frequency | Project-based: nhiều lần/ngày trong giai đoạn dự án active, giảm mạnh gần về 0 giữa các dự án |
| Internal trigger | Cảm giác lo lắng về academic integrity / cảm giác "việc chưa xong" khi biết có claim chưa verify |
| External trigger hiện có | Tự động chuyển sang ClaimVerifier ngay sau Step ⑦ (owned trigger, nằm trong chính sản phẩm) |
| Nurture phù hợp | Digest weekly/biweekly thông báo paper mới liên quan tới các theme đã verify trước đó |
| Vì sao không quá dày/thưa | Daily sẽ gây annoyance vì giữa các dự án user không có nhu cầu; quarterly sẽ làm mất liên kết với sản phẩm. Weekly/biweekly cân bằng được giữa việc duy trì presence và tránh làm phiền |
| Metric theo dõi nurture | Tỷ lệ click vào digest dẫn tới quay lại mở ClaimVerifier (góp phần vào Project Return Rate) |

**Lưu ý quan trọng:** Nurture không tạo ra nhu cầu từ số 0 — digest chỉ duy trì sự liên kết giữa các giai đoạn dự án, không thể biến một hành vi vốn không thường xuyên (verify giữa các đề tài) thành hành vi hàng ngày.

### Hook Model — Pre-check
Hành vi của use case này có **hai tầng tần suất khác nhau**, nên Hook Model không áp dụng đồng nhất cho cả use case:
- **Tầng macro** (quay lại dùng sản phẩm giữa các dự án): tần suất < weekly → **không** ép habit formation ở tầng này; xử lý bằng Nurture (digest) như trên, không bằng Hook Model.
- **Tầng trong-dự-án-active** (resolve claim khi đang viết một theme): tần suất nhiều lần/ngày → đủ điều kiện rơi vào "habit zone" → Hook Model **chỉ** áp dụng cho within-project loop này.

### Hook Model Components (within-project loop)

- **Trigger:**
  - *Internal* (qua 5 Whys): Sợ tồn đọng claim chưa kiểm → lo về academic integrity → ảnh hưởng kết quả học tập/bảo vệ → đại diện cho năng lực nghiên cứu cá nhân.
  - *External*: Màn hình tự động chuyển sang ClaimVerifier ngay sau Step ⑦ (owned trigger).
  - Completed sentence: "Mỗi khi user thấy theme mới vừa sinh xong nhưng chưa verify, họ sẽ mở ClaimVerifier để xử lý ngay."

- **Action:** Bấm 1 nút (Giữ/Sửa/Xóa) trên claim đầu tiên cần xử lý — khoảng 1-2 bước. Ability barrier chính là **Brain cycles** (phải đọc và đánh giá evidence). Ba cách giảm barrier: (1) highlight trực tiếp phần khác biệt giữa claim và nguồn, (2) gợi ý sẵn bản sửa mẫu để user chỉ cần xác nhận, (3) thêm phím tắt cho hành động Giữ/Xóa.

- **Variable Reward:** Thuộc nhóm **The Self** (làm chủ, hoàn thành, kiểm soát chất lượng bài viết của chính mình) — không phải Tribe (xã hội) hay Hunt (tài nguyên/thông tin mới); phục vụ trực tiếp core action, không phải phần thưởng giả tạo gắn ngoài.

- **Investment:** Quyết định xử lý từng claim + lý do feedback (đồng ý/không đồng ý với cách AI flag) → giảm priority cảnh báo cho pattern tương tự ở lần sau (đã có sẵn ở kịch bản 5/Day 18) → việc này load sẵn trigger tiếp theo khi theme kế tiếp được sinh ra (thường vài phút sau, trong cùng phiên làm việc).

- **Ethics check:** Không sử dụng dark pattern; thông tin hiển thị (số claim cần xem, trạng thái nguồn) phản ánh đúng trạng thái thật của dữ liệu; hook cải thiện thật sự (giảm rủi ro academic integrity, tiết kiệm thời gian) chứ không tạo nghiện vô nghĩa; rủi ro đạo đức thấp vì hook chỉ vận hành trong phiên làm việc active, không kéo dài ngoài phạm vi đó.

---

## Bài 6 — Metric Tracking Requirement

### Metric Definition Table

| Metric | Câu hỏi trả lời | Định nghĩa | Công thức | Khoảng thời gian | Segment | Event cần có |
|---|---|---|---|---|---|---|
| Core Action Completion Rate | Bao nhiêu % claim được flag thực sự được xử lý? | Tỷ lệ claim_flagged có claim_resolved tương ứng | resolved claims / flagged claims | Theo theme, rolling 7 ngày | Theo user, theo loại claim (Partially Supported/Auto-deleted/Case C/Contrasting) | claim_flagged, claim_resolved |
| Activation Rate | Bao nhiêu % theme được verify hoàn chỉnh? | Tỷ lệ theme có toàn bộ claim flagged đã resolved | theme_activated count / theme có claim_flagged | Rolling 7 ngày | Theo user | claim_flagged, claim_resolved, theme_activated |
| TTFCA | User mất bao lâu để có hành động xử lý claim đầu tiên? | Thời gian từ verification_started tới claim_resolved đầu tiên trong theme | timestamp(first claim_resolved) − timestamp(verification_started) | Theo theme | Theo user | verification_started, claim_resolved |
| TTV | User mất bao lâu để nhận giá trị đầy đủ (theme verify xong)? | Thời gian từ verification_started tới theme_activated | timestamp(theme_activated) − timestamp(verification_started) | Theo theme | Theo user | verification_started, theme_activated |
| Project Return Rate | Bao nhiêu % user quay lại ở đề tài tiếp theo? | Tỷ lệ user có project_started mới sau khoảng nghỉ ≥ vài tuần kể từ project_ended trước | users với project mới / users có project trước đó đã ended | Theo cohort dự án (không daily/weekly) | Theo user | project_started, project_ended |
| NSM (Weekly Activated Themes) | Có bao nhiêu theme đạt activation mỗi tuần? | Tổng số theme_activated trong 7 ngày, toàn user | count(theme_activated) trong tuần | Tuần | Toàn bộ user, có thể cắt theo persona | theme_activated |

### Event Tracking Requirement Table

| Event | Ghi khi nào | User identity | Properties | Metric sử dụng | Tránh ghi trùng |
|---|---|---|---|---|---|
| `verification_started` | Khi màn ClaimVerifier auto-run bắt đầu xử lý một theme (lần đầu cho theme đó trong phiên) | user_id, session_id | theme_id, timestamp, total_claims | TTFCA, TTV | Chỉ ghi 1 lần/theme/phiên; không ghi lại khi user quay lại xem màn đã verify xong |
| `claim_flagged` | Khi hệ thống xác định một claim cần user xem (Partially Supported/Case C/Contrasting) | user_id, session_id | claim_id, theme_id, claim_type, timestamp | Core Action Completion Rate, Activation Rate | Ghi đúng 1 lần khi claim được tạo/flag; không ghi lại khi user mở lại màn hình |
| `claim_resolved` | Khi user thực sự chọn một hành động có cơ sở (Giữ/Sửa/Xóa/Khôi phục/Đồng ý/Không đồng ý) trên claim đã flag | user_id, session_id | claim_id, theme_id, action_type, timestamp | Core Action Completion Rate, TTFCA, Activation Rate | Chỉ ghi khi có thay đổi state thật; không ghi khi user chỉ mở rộng evidence rồi đóng lại; không ghi trùng nếu user bấm lại cùng action trên claim đã resolved |
| `theme_activated` | Khi toàn bộ claim_flagged của một theme đã có claim_resolved tương ứng | user_id, session_id | theme_id, timestamp, total_claims_resolved | Activation Rate, TTV, NSM | Ghi đúng 1 lần/theme; nếu claim mới được flag lại sau đó (vd theme bị sinh lại), cần theme_id mới hoặc version để tránh đè |
| `project_started` / `project_ended` | Khi user bắt đầu một đề tài mới / khi đề tài được đánh dấu hoàn thành hoặc không hoạt động ≥ ngưỡng thời gian | user_id | project_id, timestamp | Project Return Rate | project_ended chỉ ghi 1 lần khi đề tài chuyển trạng thái; không ghi lại mỗi lần user không mở app |
| `nurture_click` | Khi user click vào digest weekly/biweekly | user_id | digest_id, timestamp, theme_ref (nếu có) | Hỗ trợ phân tích đóng góp của Nurture vào Project Return Rate | Ghi theo từng lần click, không cần dedupe đặc biệt |

### Events Mapped onto Flow Diagram

```
Step ⑦ hoàn thành theme
        │
        ▼
[verification_started] ── auto-run, không cần click
        │
        ▼
claim_flagged × N  (mỗi claim cần xem được flag)
        │
        ▼
User resolve claim đầu tiên
        │
        ▼
[claim_resolved] (lần đầu → tính TTFCA)
        │
        ▼
claim_resolved × (N−1)  (các claim còn lại trong theme)
        │
        ▼
[theme_activated]  (khi flagged count == resolved count) → tính TTV, đóng góp NSM
        │
        ▼
CTA sang theme tiếp theo / Step ⑨
```

### Acceptance Criteria cho Tracking

1. `claim_resolved` chỉ được ghi khi có thay đổi state thật trên claim (action_type hợp lệ); việc mở rộng/đóng evidence không được kích hoạt event này.
2. `verification_started` và `claim_flagged` không bị ghi trùng khi user refresh hoặc mở lại màn hình đã xử lý — mỗi theme/claim chỉ có một bản ghi gốc.
3. Mọi event đều có đủ user_id và session_id để truy vết theo user và theo phiên làm việc, phục vụ tính Active User và Project Return Rate.
4. Tất cả timestamp được ghi theo UTC và nhất quán giữa các event, để các phép tính khoảng thời gian (TTFCA, TTV) không bị lệch múi giờ.
5. `theme_activated` phải đối chiếu được số lượng `claim_flagged` và `claim_resolved` của đúng theme_id đó trước khi ghi — tránh activate sai khi còn claim chưa resolved.
6. Không đẩy nội dung claim hoặc feedback dạng free-text vào hệ thống analytics — chỉ gửi id, loại, trạng thái; nội dung claim thật giữ trong hệ thống sản phẩm, không qua tracking pipeline.

---

## Self-Review Notes

- **Placeholder scan:** Không còn mục TBD/TODO; toàn bộ Bài 1–6 đã có nội dung cụ thể.
- **Internal consistency:** Core Action (Bài 2) khớp với First Core Action trong Bài 3; Activation (Bài 3) khớp với theme_activated (Bài 6) và Activation Rate (Bài 4); Retention Metric (Bài 2) khớp với Project Return Rate (Bài 4) và project_started/ended (Bài 6); Hook Model (Bài 5) chỉ áp dụng tầng within-project, không mâu thuẫn với Nurture ở tầng macro.
- **Scope check:** Toàn bộ nội dung tiếp tục đúng 1 use case (Claim Verification & Routing) đã chọn ở Day 18, không mở rộng sang sản phẩm hoặc scenario mới.
- **Ambiguity check:** Đã làm rõ ranh giới First Core Action vs Activation (atomic event vs full-theme completion) để tránh nhầm lẫn khi đo TTFCA và TTV.

---

## Prototype Changes Implemented (xem `claim_verifier_prototype.html`)

1. Bỏ nút "Bắt đầu verify" thủ công — verification tự động chạy khi vào màn (instrument `verification_started`).
2. Header rút gọn còn 1 dòng + icon "ⓘ" mở rộng chi tiết khi cần.
3. Legend màu chuyển sang hiển thị theo ngữ cảnh (chỉ giải thích badge khi gặp lần đầu).
4. Claim cần xử lý (actionable) được đưa lên đầu danh sách, claim auto-kept xuống dưới.
5. Thêm chỉ số tiến độ "x/y claim cần xem đã xử lý" cập nhật sau mỗi lần resolve (evidence of value).
6. Thêm banner hoàn tất theme ("✅ Theme này đã verify xong...") khi toàn bộ claim cần xem đã resolved, kèm CTA sang theme tiếp theo (Activation/Aha moment).
7. Instrument các event: `verification_started`, `claim_flagged`, `claim_resolved`, `theme_activated` (demo qua console.log + chỉ số hiển thị, vì đây là prototype không có backend thật).
