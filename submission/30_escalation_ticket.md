# Escalation ticket

## Ticket 1

- **Frame:** `adasind_086220.jpg`
- **Ảnh chụp:** `submission/screenshots/qa_evidence_L11_truncated.png`
- **Expected impact:** Khi xe ba bánh hoặc các phương tiện lớn ở góc sát rìa thấu kính không được gán đúng thuộc tính `truncated=true`, các mô hình 3D bounding box và tracking đa camera sẽ ước lượng sai kích thước hình học và khoảng cách vật thể thực tế trong điểm mù, tiềm ẩn nguy cơ chậm trễ cảnh báo va chạm sườn xe.
- **Owner:** `guideline`
- **Recommendation:** Ban hành bổ sung quy tắc R11 vào tài liệu guideline nội bộ, kèm hình ảnh minh họa về ranh giới thấu kính `lens_border`; đồng thời chạy lại batch kiểm tra tự động thuộc tính `truncated` cho toàn bộ các frame có box chạm biên `xbr/ybr` tối đa trước khi đưa dữ liệu vào tập huấn luyện AI.
