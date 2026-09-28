# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| `B1-mid` zone `center`+`mid` (slice của tôi, cả 3 frame) | 12+11=23 `SPURIOUS`, 4+5=9 `MISSING` (chủ yếu `M_only`/`LR_noM` — model) | Khối lượng khác biệt lớn nhất trong toàn bài; cần tách rõ phần do model (đa số) khỏi phần do annotator (thiểu số, đã xử lý ở rework) trước khi dùng slice này làm ví dụ dạy | `submission/r3_diag/model_compare.html`, `local_quality_conflicts.csv`, `findings.csv` (round=`r3_diag`) |
| `B4-dense` (bài của tuân, đã QA) | 4 `WRONG_CLASS` ở zone `center` (5 ca thực tế trên 2 frame) | Lỗi lặp lại có hệ thống (auto-rickshaw→Car), không phải ngẫu nhiên — ảnh hưởng trực tiếp đến việc đếm đúng loại phương tiện nếu dùng slice này làm mẫu | `submission/screenshots/qa_258420_wrongclass_threewheeler.png`, `qa_270517_wrongclass_threewheeler.png`, `20_guideline_patch.md`, `30_escalation_ticket.md` |

Giới hạn của kết luận từ ba frame ADASIND: Chỉ 3 frame trên 1 camera (không phải bốn camera SVM), lấy từ cùng một tuyến đường/điều kiện ánh sáng — không đủ đại diện cho các điều kiện khác (đêm, mưa, camera góc khác). Số lỗi tuyệt đối (SPURIOUS=23, WRONG_CLASS=5...) không nên quy đổi thành "tỷ lệ lỗi %" của toàn bộ 48 frame hay của bốn camera thật, vì mẫu quá nhỏ và không ngẫu nhiên (do giáo viên chọn slice có tính minh hoạ).

## Chuyển sang kế hoạch bốn camera giả lập

Với 200 frame ở `45_sampling_plan.csv`, cách soát độ phủ: nhóm các frame liên tiếp/cùng một đoạn đường-thời điểm thành **một ca quan sát**, không đếm riêng từng frame trong cùng một sự kiện là nhiều ca độc lập (ví dụ 5 frame liên tiếp cùng chụp một xe băng qua giao lộ chỉ tính là 1 ca "cắt ngang giao lộ", không phải 5 ca). Kế hoạch 45_sampling_plan.csv chỉ giúp **tìm ra ca nào cần soi** (phân bổ theo camera × độ khó normal/hard) — nó **chưa đo được tỷ lệ lỗi thật** vì: (1) chưa có nhãn/gold set để so sánh, chỉ là kế hoạch lấy mẫu; (2) 200 frame là ngân sách chọn trước, không phải kết quả đo random trên 50.000 frame; (3) giống bài học từ `B1-mid`/`B4-dense` ở trên — một mẫu nhỏ có thể lẫn cả lỗi hệ thống (cần patch rule) lẫn nhiễu ngẫu nhiên (model), phải review từng ca bằng mắt mới tách được, không thể suy ra tỷ lệ % lỗi chỉ từ việc đếm frame.
