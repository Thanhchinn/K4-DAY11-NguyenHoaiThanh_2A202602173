# Guideline patch

- **Rule mới đề xuất:** **R11 — Phân định rõ thuộc tính `truncated` tại vùng giao cắt `lens_border`:** Bất kỳ phương tiện hoặc người đi bộ nào có bounding box chạm hoặc cắt qua ranh giới trong của polygon `lens_border` (vành đen quang học của ống kính mắt cá) hoặc chạm 4 cạnh ảnh đều bắt buộc phải được đánh dấu thuộc tính `truncated=true`.
- **Áp dụng cho:** Tất cả 6 class (`Car`, `Bus`, `Truck`, `ThreeWheeler`, `Bike`, `Pedestrian`) nằm ở zone `edge` và vùng tiếp giáp viền ống kính `lens_border`.
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** Quy tắc `R05` hiện tại chỉ nêu định nghĩa hình học định tính ("vật bị cắt bởi vòng kính hoặc biên khung hình"), nhưng thiếu tiêu chuẩn cụ thể về mức độ tiếp xúc với polygon `lens_border`. Điều này khiến annotator thường phân vân và bỏ sót thuộc tính `truncated` đối với các phương tiện lớn nằm sát rìa ảnh (như xe ba bánh `L11` tại frame `adasind_086220.jpg`).
- **`rules_version` mới:** `v1.1.0` (nâng cấp từ `v1.0.0`)
- **Hiệu lực từ:** Vòng `rework` trở đi và toàn bộ các đợt gán nhãn production kế tiếp.
