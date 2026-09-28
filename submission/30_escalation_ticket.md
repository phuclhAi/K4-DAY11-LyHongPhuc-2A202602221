# Escalation ticket

## Ticket 1

- **Frame:** `adasind_258420.jpg` (L1, L2, L7) và `adasind_270517.jpg` (L2, L8) — slice `B4-dense`, bài của tuấn, phát hiện khi QA ở P3.
- **Ảnh chụp:** `submission/screenshots/qa_258420_wrongclass_threewheeler.png`, `submission/screenshots/qa_270517_wrongclass_threewheeler.png`
- **Expected impact:** Nhầm `ThreeWheeler` thành `Car` lặp lại 5/8 lần trong một slice — nếu đây là mẫu phổ biến trên toàn bộ dữ liệu, số liệu thống kê theo class (ví dụ phân bố `Car` so với `ThreeWheeler` trong sampling/gold set bốn camera) sẽ bị lệch, ảnh hưởng đến việc ước lượng tỷ lệ loại phương tiện cần ưu tiên khi lập kế hoạch review.
- **Owner:** `guideline` (cần patch rule R04 — xem `20_guideline_patch.md`); đồng thời báo `annotator` gốc (tuấn) để tự soát lại slice `B4-dense`.
- **Recommendation:** (1) Duyệt và áp dụng patch R04 đề xuất ở `20_guideline_patch.md`; (2) tuấn tự rà lại các box `Car` còn lại trong `B4-dense` xem có case tương tự chưa phát hiện; (3) không tự ý đổi class thay tuấn — đây là quyết định của annotator gốc sau khi có rule rõ hơn, QA chỉ nêu bằng chứng.
