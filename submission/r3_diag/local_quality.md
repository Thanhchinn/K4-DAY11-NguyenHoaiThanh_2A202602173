# Đối chiếu chất lượng cục bộ — rectangle

Teaching reference, không phải gold set đã phê duyệt; không có điểm đạt tự động.
Nguồn: export r1_craft đã khóa SHA256 `a81f7e36b06bbdc12faa773c694432e440b2a6eb1a3677b0d6afe9cd074700ea`; slice `B2-mid`.
Ghép hình học greedy một-một theo IoU ≥ 0.50, rồi so class; H ≥ 40 px.
Box trái nằm chủ yếu trong ignore_region reference không tính. Polygon, polyline, track không được chấm.
Đây là phép tính offline của lab, không phải báo cáo hay kết quả tương đương CVAT Premium.

Frame được tính: adasind_060000.jpg, adasind_086220.jpg, adasind_102750.jpg. Frame thiếu trong export: không.
TP=16; FP=5; FN=4; số lần đối chiếu=24; mean IoU của TP=0.864.

| Chỉ số | Micro | Macro | Nhãn thấp nhất |
|---|---:|---:|---:|
| accuracy | 0.667 | 0.906 | 0.833 |
| precision | 0.762 | 0.744 | 0.500 |
| recall | 0.800 | 0.743 | 0.333 |
| jaccard | 0.640 | 0.629 | 0.250 |
| dice | 0.780 | 0.738 | 0.400 |

| Nhãn | TP | FP | FN | Accuracy | Precision | Recall | Jaccard | Dice |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bike | 3 | 1 | 1 | 0.917 | 0.750 | 0.750 | 0.600 | 0.750 |
| Pedestrian | 4 | 0 | 0 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 |
| ThreeWheeler | 8 | 3 | 1 | 0.833 | 0.727 | 0.889 | 0.667 | 0.800 |
| Truck | 1 | 1 | 2 | 0.875 | 0.500 | 0.333 | 0.250 | 0.400 |

| Frame | TP | FP | FN | Accuracy | Precision | Recall |
|---|---:|---:|---:|---:|---:|---:|
| adasind_060000.jpg | 9 | 0 | 1 | 0.900 | 1.000 | 0.900 |
| adasind_086220.jpg | 4 | 2 | 1 | 0.571 | 0.667 | 0.800 |
| adasind_102750.jpg | 3 | 3 | 2 | 0.429 | 0.500 | 0.600 |

Confusion matrix: hàng = teaching reference; cột = export đã khóa.
`<missing>` là thiếu box; `<extra>` là box thừa. Xem `local_quality_confusion.csv`.

| Reference \ Export | Bike | Pedestrian | ThreeWheeler | Truck | <missing> |
|---|---:|---:|---:|---:|---:|
| Bike | 3 | 0 | 0 | 0 | 1 |
| Pedestrian | 0 | 4 | 0 | 0 | 0 |
| ThreeWheeler | 0 | 0 | 8 | 0 | 1 |
| Truck | 0 | 0 | 1 | 1 | 1 |
| <extra> | 1 | 0 | 2 | 1 | 0 |

Chi tiết xung đột trong `local_quality_conflicts.csv`; dữ liệu máy đọc trong `local_quality.json`.
Mismatching label đóng góp một FP cho class vẽ và một FN cho class reference; attribute khác được báo riêng.
Micro accuracy đếm mỗi cặp ghép sai class là một lần đối chiếu; Jaccard đếm cả FP và FN.
Macro/worst bỏ nhãn không xuất hiện ở cả hai phía; chỉ số không có mẫu là N/A.
