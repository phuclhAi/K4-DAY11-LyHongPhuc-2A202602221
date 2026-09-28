# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B1 | BOX_GEOMETRY | 1 |
| center | B1 | MISSING | 4 |
| center | B1 | SPURIOUS | 12 |
| center | B4 | WRONG_CLASS | 4 |
| center | C0 | SPURIOUS | 3 |
| edge | B1 | SPURIOUS | 3 |
| edge | B4 | WRONG_CLASS | 1 |
| edge | C0 | WRONG_CLASS | 1 |
| mid | B1 | MISSING | 5 |
| mid | B1 | SPURIOUS | 11 |
| unknown | B1 | BOX_GEOMETRY | 1 |
| unknown | B1 | DUPLICATE | 2 |
| unknown | B1 | WRONG_CLASS | 1 |

## Top defects
- SPURIOUS: 29 (ví dụ frame adasind_019560.jpg)
- MISSING: 9 (ví dụ frame adasind_014670.jpg)
- WRONG_CLASS: 7 (ví dụ frame adasind_019560.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy: `SPURIOUS` (29 dòng) chiếm đa số nhưng **không đồng nhất** — phần lớn (15/29) là model dự đoán thừa (`M_only`, ví dụ `adasind_032280.jpg` M3/M5/M7/M8/M9/M11 và `adasind_034080.jpg` M7–M12), tức `E4_model_domain`: model có vẻ nhạy cảm quá mức với cảnh đường phố đông đúc kiểu chợ/thị trấn Nam Á, tạo nhiều box giả trong vùng vật chồng lấn. Phần còn lại (6/29, ví dụ `adasind_014670.jpg` L5, `adasind_032280.jpg` L2/L7) là `L_only` chưa rõ nguyên nhân (`E5_unresolved`) — không khớp cả reference lẫn model nên cần soi ảnh gốc kỹ hơn mới kết luận được là annotator vẽ thừa hay cả hai bên kia cùng bỏ sót. `WRONG_CLASS` (7 dòng) chủ yếu đến từ một lỗi hệ thống: xe ba bánh (auto-rickshaw) bị gán nhầm thành `Car` — lặp lại 5 lần trong QA bài `B4-dense` của tuấn (`adasind_258420.jpg` L1/L2/L7, `adasind_270517.jpg` L2/L8) và 1 lần ở calib C0 — cho thấy đây không phải lỗi ngẫu nhiên mà là nhầm lẫn hình dạng có hệ thống (`E1_annotator_error` lặp lại, khả năng có phần `E2_guideline_gap` vì rule R04 chưa nêu rõ đặc điểm phân biệt hình dáng). `MISSING` (9 dòng) chủ yếu là `LR_noM` — người (L) và reference (R) đều đồng ý có vật nhưng model bỏ sót, không phải lỗi của annotator.
- Cách sửa và ai nhận việc (`owner`): (1) Model dự đoán thừa/bỏ sót ở cảnh đông vật → `owner=ai_team`, cần xem lại ngưỡng confidence/NMS hoặc fine-tune thêm trên dữ liệu đường phố mật độ cao. (2) Nhầm `ThreeWheeler`↔`Car` lặp lại → `owner=guideline`, đề xuất patch bổ sung đặc điểm hình dáng phân biệt vào R04 (khoang lái hẹp, đuôi vuông chở khách/hàng là dấu hiệu `ThreeWheeler`) — đã ghi ở `20_guideline_patch.md`. (3) Box hình học lấn vật khác (`adasind_034080.jpg` L9) → `owner=annotator`, đã sửa xong ở P5 (`rework/delta.md`). (4) Các ca `L_only` chưa rõ nguyên nhân → giữ `keep_with_reason`, cần thêm frame mẫu để kết luận, không nên sửa mù.
- Bằng chứng (ảnh trong `screenshots/`, dòng findings, rule): `findings.csv` các dòng `round=r3_diag` (why=E4_model_domain/E5_unresolved) và `round=r2_qa` slice=`B4-dense` (rule_id=R04); trực quan tại `submission/r2_qa/qa_overlay.html` (5 ca auto-rickshaw→Car) và `submission/r3_diag/model_compare.html` (các ca M_only/LR_noM); luật tham chiếu R02, R03, R04 trong `docs/02-rules-vi.md`.
