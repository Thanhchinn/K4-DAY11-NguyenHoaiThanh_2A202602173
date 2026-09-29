# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 9 | 3 | 2 | 5 | 8 | MISSING (3) |
| mid | 8 | 0 | 2 | 4 | 10 | SPURIOUS (2) |
| edge | 3 | 1 | 1 | 2 | 0 | WRONG_CLASS (1) |

## Nhận xét

- **Zone người (L) và model (M) gãy nhiều nhất:**
  - **Người (L):** Gặp nhiều lỗi nhất ở vùng **`center`** với 3 missing và 2 spurious (tổng 5 lỗi), tiếp theo là vùng `mid` với 2 box thừa (spurious). Lỗi chính ở center là bỏ sót vật thể (MISSING) do mật độ phương tiện đông đúc. Ở vùng `edge`, người gặp 1 lỗi sai phân loại (WRONG_CLASS) và 1 missing.
  - **Model (M):** Gãy nặng nhất ở vùng **`mid`** với 10 box thừa (`LM_noR` + `M_only`) và 4 box bị bỏ sót (`LR_noM` + `R_only`), kế đến là vùng **`center`** với 8 box thừa và 5 box bỏ sót. Tổng cộng model sinh ra tới 18 false positives ở hai vùng này.
- **Giả thuyết nguyên nhân và giới hạn lát cắt 3 frame:**
  - *Về phía Người (L):* Vùng `center` tập trung nhiều phương tiện nhỏ ở xa sát ngưỡng H=40px và bị che khuất đan xen (`occluded`) khiến annotator dễ bỏ sót; ở vùng `edge`, độ méo quang học thấu kính fisheye làm biến dạng hình học phương tiện dẫn đến gán nhầm nhãn class.
  - *Về phía Model (M):* Mô hình gặp hiện tượng domain shift rõ rệt với ảnh mắt cá góc rộng, nhầm lẫn bóng đổ và các chi tiết kết cấu mặt đường thành vật thể dẫn đến bùng nổ box thừa (FP) ở mid và center; đồng thời không nhận diện tốt các vật thể biến dạng cong ở vùng rìa.
  - *Giới hạn:* Đây chỉ là lát cắt 3 frame trên 1 camera trước (ADASIND) trong điều kiện ban ngày tiêu chuẩn, các con số này mang tính chẩn đoán cục bộ để tìm loại lỗi, không phản ánh toàn diện tỷ lệ lỗi ngoài thực tế hay cho cả hệ thống 4 camera SVM.
