# Sensor context

- **Rig:** Camera fisheye góc siêu rộng (FOV xấp xỉ 180°–190°) được gắn ở vị trí phía trước xe thử nghiệm (front-facing, khu vực cản trước hoặc nắp ca-pô/kính lái), hướng về phía trước theo luồng di chuyển của giao thông đường phố (tập dữ liệu ADASIND).
- **`ego_body`:** Phần thân xe tự thân (ego vehicle) xuất hiện ở mép đáy / góc dưới của khung hình (thường là phần cản trước hoặc nắp ca-pô). Thấy rõ ở hầu hết các frame (46/48 frame ADASIND), cần khoanh vùng polygon `ignore_region` gắn nhãn `ego_body`. Đối với các frame ngoại lệ không nhìn thấy thân xe (như 006840, 271039) thì không vẽ để tránh polygon thừa.
- **Vòng kính (lens circle):** Vòng tròn quang học của thấu kính mắt cá nằm cân đối ở vùng trung tâm khung hình, chiếm khoảng 85% – 90% diện tích ảnh. Vùng ngoài vòng tròn và 4 góc là viền đen quang học nằm ngoài trường nhìn, được bao bọc bởi 2 polygon `lens_border`.
