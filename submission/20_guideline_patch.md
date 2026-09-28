# Guideline patch

- **Rule mới đề xuất:** Bổ sung vào R04 đặc điểm hình dáng để phân biệt `ThreeWheeler` với `Car` khi xe bị che khuất một phần hoặc chụp từ góc khó: khoang lái hẹp (không có cửa hai bên như ô tô), thân sau dạng khoang vuông hở chở người/hàng, và **chiều rộng thân xe thường nhỏ hơn rõ rệt so với Car** cùng khoảng cách. Khi nghi ngờ, ưu tiên nhìn phần bánh xe (3 bánh thường lộ rõ bánh sau đôi hoặc khung gầm hẹp).
- **Áp dụng cho:** class `ThreeWheeler` và `Car` (R04, ánh xạ phương tiện đặc biệt).
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** R04 chỉ liệt kê tên loại xe ("xe ba bánh chở người/hàng → `ThreeWheeler`") mà không mô tả đặc điểm hình dáng nhận diện, dẫn tới nhầm lẫn có hệ thống. Bằng chứng: khi QA bài `B4-dense` của tuấn, phát hiện **5 lần liên tiếp** auto-rickshaw bị gán `Car` thay vì `ThreeWheeler` (`adasind_258420.jpg` L1/L2/L7, `adasind_270517.jpg` L2/L8 — xem `submission/screenshots/qa_258420_wrongclass_threewheeler.png` và `qa_270517_wrongclass_threewheeler.png`); đây không phải lỗi ngẫu nhiên của một người mà là mẫu lặp lại, gợi ý luật hiện tại mô tả chưa đủ rõ.
- **`rules_version` mới:** v1.0.0 → v1.1.0
- **Hiệu lực từ:** đề xuất áp dụng từ round `r1_craft` của slice tiếp theo (không hồi tố sửa các slice đã khoá; các ca đã phát hiện xử lý qua `findings.csv`/escalation).
