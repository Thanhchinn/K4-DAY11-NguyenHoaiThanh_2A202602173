# QA review · B2-mid

Mã khóa: A81F-7E36

| frame | object_ref | rule_id | nhận xét |
|---|---|---|---|
| adasind_086220.jpg | L11 | R05 | Xe ba bánh L11 chạm viền thấu kính ở góc dưới bên phải, bị cắt cụt một phần thân xe nhưng chưa được đánh dấu thuộc tính `truncated=1`. Cần bổ sung để đúng chuẩn hình học thấu kính. |
| adasind_086220.jpg | L9 | R04 | Phương tiện ở cự ly xa có kích thước nhỏ H=17.6px bị gán nhãn nhầm là `Bus`. Theo hình thái xe thực tế đây là van chở người, quy tắc R04 quy định ánh xạ về `Car`. Cần sửa class hoặc loại bỏ do dưới ngưỡng H=40. |
| adasind_060000.jpg | L1 | R01 | Xe hai bánh L1 có chiều cao H=34.9px (< ngưỡng H=40px theo R01). Vật thể ở xa, box vẽ chưa ôm sát phần chân bánh xe nhìn thấy trên mặt đường. Cần căn chỉnh lại geometry. |

Ghi finding r2_qa: cell=L_only, rule_id có giá trị, why để trống.
