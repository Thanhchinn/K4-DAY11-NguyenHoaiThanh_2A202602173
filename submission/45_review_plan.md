# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| `adasind_086220.jpg` | 3 ca: Lỗi thuộc tính `truncated` ở mép lens (`L11`), phân loại nhầm class `WRONG_CLASS` (`L9`), và box xe ở xa (`MISSING`/`SPURIOUS`) | Khung hình có mật độ phương tiện phức tạp, có xe ba bánh lớn chạm mép quang học; đây là ca rủi ro cao ảnh hưởng trực tiếp đến ước lượng kích thước vật thể ở rìa thấu kính | Ảnh crop minh chứng trong `submission/screenshots/`, các dòng finding `r2_qa`, và quy tắc `R04`, `R05` trong `docs/02-rules-vi.md` |
| `adasind_060000.jpg` | 2 ca: Lỗi bỏ sót `MISSING` xe ba bánh bị che khuất (`R9`) và box `BOX_GEOMETRY` chưa ôm khít bánh xe (`L1`) | Cần kiểm tra ranh giới phân định vật thể bị che khuất một phần (`occluded`) và tính nhất quán khi áp dụng ngưỡng kích thước H=40px | Đối chiếu `compare.html` trước/sau rework, dòng finding `r1_craft` cho ca `L8`, và nhãn polygon `ego_body` ở đáy ảnh |

Giới hạn của kết luận từ ba frame ADASIND: Dữ liệu thực hành chỉ gồm 3 frame trên 1 camera fisheye gắn phía trước trong điều kiện ban ngày tiêu chuẩn; không có dữ liệu ban đêm, trời mưa, và hoàn toàn thiếu vắng 3 camera còn lại (sau, trái, phải). Do đó, kết quả phân tích chỉ mang tính chất chẩn đoán loại lỗi cục bộ, không thể ngoại suy để khẳng định tỷ lệ lỗi tổng thể của hệ thống.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv` (kể cả tránh đếm nhiều frame liền nhau trong cùng cảnh như nhiều ca độc lập), và vì sao kế hoạch đó chỉ giúp tìm ca cần soi, chưa đo được tỷ lệ lỗi:
- **Cách soát độ phủ:** Áp dụng phương pháp lấy mẫu phân tầng theo thời gian và cảnh quay (temporal spacing tối thiểu 3–5 giây giữa 2 frame được chọn, hoặc dựa trên cụm khoảng cách di chuyển GPS/odometry) để tránh tình trạng chọn các frame liên tiếp trong cùng một pha đèn đỏ/dừng xe rồi coi là nhiều ca độc lập. Đảm bảo độ phủ trải đều trên cả 4 camera và cân đối giữa kịch bản ban ngày, chói sáng, trời tối và mật độ giao thông hỗn hợp.
- **Bản chất đo lường:** Kế hoạch 200 frame được thiết kế theo phương pháp lấy mẫu tập trung vào ca khó và vùng rủi ro cao (targeted/purposive sampling). Vì vậy, nó chỉ có giá trị tối ưu nguồn lực để **tìm kiếm các dạng lỗi hiểm hóc (defect discovery)** phục vụ việc hoàn thiện guideline và kiểm định an toàn, chứ không phản ánh tỷ lệ lỗi thống kê ngẫu nhiên (statistical error rate) trên toàn bộ quần thể 50.000 frame.
