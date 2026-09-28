# Đối chiếu chất lượng cục bộ — rectangle

Teaching reference, không phải gold set đã phê duyệt; không có điểm đạt tự động.
Nguồn: export r1_craft đã khóa SHA256 `4b7feb279a2d865d764b8fc26efa41a7465969dab4698b08d8754852b99a3ee7`; slice `B1-mid`.
Ghép hình học greedy một-một theo IoU ≥ 0.50, rồi so class; H ≥ 40 px.
Box trái nằm chủ yếu trong ignore_region reference không tính. Polygon, polyline, track không được chấm.
Đây là phép tính offline của lab, không phải báo cáo hay kết quả tương đương CVAT Premium.

Frame được tính: adasind_014670.jpg, adasind_032280.jpg, adasind_034080.jpg. Frame thiếu trong export: không.
TP=19; FP=6; FN=1; số lần đối chiếu=26; mean IoU của TP=0.802.

| Chỉ số | Micro | Macro | Nhãn thấp nhất |
|---|---:|---:|---:|
| accuracy | 0.731 | 0.946 | 0.885 |
| precision | 0.760 | 0.810 | 0.667 |
| recall | 0.950 | 0.960 | 0.800 |
| jaccard | 0.731 | 0.790 | 0.571 |
| dice | 0.844 | 0.872 | 0.727 |

| Nhãn | TP | FP | FN | Accuracy | Precision | Recall | Jaccard | Dice |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bike | 4 | 2 | 0 | 0.923 | 0.667 | 1.000 | 0.667 | 0.800 |
| Car | 4 | 2 | 1 | 0.885 | 0.667 | 0.800 | 0.571 | 0.727 |
| Pedestrian | 5 | 0 | 0 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 |
| ThreeWheeler | 5 | 2 | 0 | 0.923 | 0.714 | 1.000 | 0.714 | 0.833 |
| Truck | 1 | 0 | 0 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 |

| Frame | TP | FP | FN | Accuracy | Precision | Recall |
|---|---:|---:|---:|---:|---:|---:|
| adasind_014670.jpg | 5 | 1 | 0 | 0.833 | 0.833 | 1.000 |
| adasind_032280.jpg | 6 | 2 | 0 | 0.750 | 0.750 | 1.000 |
| adasind_034080.jpg | 8 | 3 | 1 | 0.667 | 0.727 | 0.889 |

Confusion matrix: hàng = teaching reference; cột = export đã khóa.
`<missing>` là thiếu box; `<extra>` là box thừa. Xem `local_quality_confusion.csv`.

| Reference \ Export | Bike | Car | Pedestrian | ThreeWheeler | Truck | <missing> |
|---|---:|---:|---:|---:|---:|---:|
| Bike | 4 | 0 | 0 | 0 | 0 | 0 |
| Car | 0 | 4 | 0 | 0 | 0 | 1 |
| Pedestrian | 0 | 0 | 5 | 0 | 0 | 0 |
| ThreeWheeler | 0 | 0 | 0 | 5 | 0 | 0 |
| Truck | 0 | 0 | 0 | 0 | 1 | 0 |
| <extra> | 2 | 2 | 0 | 2 | 0 | 0 |

Chi tiết xung đột trong `local_quality_conflicts.csv`; dữ liệu máy đọc trong `local_quality.json`.
Mismatching label đóng góp một FP cho class vẽ và một FN cho class reference; attribute khác được báo riêng.
Micro accuracy đếm mỗi cặp ghép sai class là một lần đối chiếu; Jaccard đếm cả FP và FN.
Macro/worst bỏ nhãn không xuất hiện ở cả hai phía; chỉ số không có mẫu là N/A.
