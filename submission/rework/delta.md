# Rework delta

| zone | matched before | matched after | missing before | missing after | spurious before | spurious after |
|---|---:|---:|---:|---:|---:|---:|
| center | 6 | 6 | 1 | 1 | 3 | 3 |
| mid | 11 | 11 | 0 | 0 | 2 | 2 |
| edge | 2 | 2 | 0 | 0 | 1 | 1 |

## Findings action=rework
- adasind_034080.jpg L9 SPURIOUS: đã sửa

## Giải thích số không đổi

Bảng zone trước/sau giữ nguyên dù box đã được sửa (mép trái kéo từ x≈466 vào x≈510 theo phần xe con thực sự nhìn thấy, không còn lấn sang thân `ThreeWheeler` L10 phía trước). Lý do: lỗi ban đầu là **chồng ranh giới hình học** (BOX_GEOMETRY) giữa hai vật đã tồn tại, không phải thiếu (`missing`) hay thừa (`spurious`) một vật — nên việc sửa không làm thay đổi số lượng matched/missing/spurious theo IoU ở ngưỡng đang dùng (0.5), chỉ cải thiện độ chính xác hình học của chính box đó (không đo được trong bảng đếm theo zone này). Đây là giới hạn của phép so khớp nhị phân (matched/missing/spurious): nó không phản ánh mức cải thiện IoU của một match đã tồn tại từ trước.
