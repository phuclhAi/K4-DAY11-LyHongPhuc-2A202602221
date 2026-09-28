# So sánh L với R

Chỉ số L/R là thứ tự box cao ≥ H=40 trong từng frame, theo thứ tự XML; bắt đầu từ 1.
Box L trong ignore_region được báo IGNORE_SCOPE, không tính SPURIOUS.

## adasind_014670.jpg
- L5 center SPURIOUS
## adasind_032280.jpg
- L2 mid SPURIOUS
- L7 edge SPURIOUS
## adasind_034080.jpg
- L3 center SPURIOUS
- L4 mid SPURIOUS
- L9+R2 center BOX_GEOMETRY

## Theo zone
| zone | n_ref | matched | missing | spurious |
|---|---|---|---|---|
| center | 7 | 6 | 1 | 3 |
| mid | 11 | 11 | 0 | 2 |
| edge | 2 | 2 | 0 | 1 |
