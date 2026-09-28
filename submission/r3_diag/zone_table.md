# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 7 | 1 | 3 | 3 | 7 | SPURIOUS (2) |
| mid | 11 | 0 | 2 | 5 | 7 | SPURIOUS (2) |
| edge | 2 | 0 | 1 | 0 | 1 | SPURIOUS (1) |

## Nhận xét

- Zone nào người (L) và model (M) gãy nhiều nhất, dẫn số ở bảng trên: `center` gãy nặng nhất về phía người (L missing=1, L spurious=3 — cao nhất cả bảng) đồng thời model cũng thừa nhiều nhất ở đây (M thừa=7). Zone `mid` model bỏ sót nhiều nhất (M missing=5). Zone `edge` ít vật nhất (n_ref=2) nên số tuyệt đối thấp nhưng tỷ lệ lỗi trên mỗi vật lại cao (1/2 vật bị L spurious).
- Giả thuyết vì sao và giới hạn của slice ba frame: Zone `center` (r/R<0.35) tuy ít méo hình học nhất nhưng lại là nơi mật độ vật cao nhất trong 3 frame này (gần camera, nhiều xe/người chồng lấn ở `034080.jpg`) — nên dễ xảy ra bất đồng về việc có bao nhiêu vật thật (SPURIOUS ở cả L và M) hơn là do méo ống kính. Model có thể đã học trên phân bố khác (ít cảnh đông đúc kiểu chợ/đường làng) nên bỏ sót nhiều ở `mid` và dự đoán thừa ở `center`. Giới hạn quan trọng: chỉ 3 frame trong 1 slice, mẫu quá nhỏ để kết luận đây là lỗi hệ thống của model hay chỉ là đặc thù riêng của 3 frame này; không nên suy rộng ra toàn bộ 48 frame ADASIND từ bảng này.
