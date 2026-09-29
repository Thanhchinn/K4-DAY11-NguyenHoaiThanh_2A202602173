# Exit ticket

Đọc `docs/10-svm360-reading-vi.md` trước khi trả lời câu 1–2. Các câu về zone, `why`, rework, parking và sampling
đã nằm trong file tương ứng nên không hỏi lại ở đây.

1. **Một vật ở vùng seam giữa hai camera thật xuất hiện với hai box khác nhau: đó là lỗi `DUPLICATE` hay cần một quy tắc riêng? Vì sao?**
   Đây là **trường hợp hợp lệ cần một quy tắc riêng (cross-camera seam policy)**, KHÔNG PHẢI là lỗi `DUPLICATE`. Trên mặt phẳng ảnh 2D của từng cảm biến fisheye độc lập, vật thể thực tế đang hiện diện đồng thời trong trường nhìn (FOV) của cả hai camera tại góc chồng lấn. Mỗi camera có phối cảnh quang học và góc méo thấu kính khác nhau, do đó việc giữ 2 box độc lập ở tầng 2D là cần thiết để thuật toán phát hiện vật thể cục bộ không bị sót (false negative). Việc khử trùng lặp và liên kết định danh chỉ được thực hiện ở tầng không gian hợp nhất 3D / Bird's-Eye View (BEV) phía sau.

2. **Một vật đi qua nhiều frame trên cùng camera: khi nào giữ cùng track ID, khi nào thêm keyframe hoặc trạng thái Outside? Nêu bằng chứng sẽ cần trước khi nối track qua hai camera.**
   - *Trong cùng một camera:* Giữ cùng `track ID` khi vật thể di chuyển liên tục và duy trì nhận dạng thực thể trong tầm nhìn; thêm `keyframe` khi vật thể có biến đổi hình học lớn (quay đầu, đổi góc nhìn méo fisheye) hoặc bắt đầu bị che khuất; gán trạng thái `Outside` khi vật thể hoàn toàn vượt ra ngoài vòng kính quang học hoặc ra khỏi biên khung hình.
   - *Bằng chứng cần thiết trước khi nối track liên camera:* Cần đủ 3 yếu tố: (1) Đồng bộ timestamp phần cứng chính xác ở cấp độ micro-giây giữa 2 camera; (2) Ma trận hiệu chuẩn ngoại tại (extrinsics) và nội tại (intrinsics) chuẩn xác để ánh xạ về cùng một hệ quy chiếu mặt đất; (3) Chính sách hợp nhất dữ liệu (fusion policy) xác định camera nào có độ tin cậy cao hơn ở góc nhìn đó.

3. **Nhìn lại cả buổi: một chỗ bạn tin nhãn mình đúng nhưng reference hoặc người soát nghĩ khác (dẫn frame/`object_ref`), bạn đã xử lý thế nào, và nếu làm lại slice này bạn sẽ đổi gì trong cách làm?**
   Tại frame `adasind_086220.jpg` vật thể `L9`: Người gán nhãn đã vẽ box cho phương tiện ở cự ly xa với nhãn `Bus` vì nhìn giống xe khách nhỏ, nhưng QA và reference xác định đây là xe van chở người và có chiều cao H=17.6px (dưới ngưỡng H=40px). Tôi đã xử lý ca này bằng cách đưa vào `findings.csv` với căn cứ quy tắc R01 và R04, sau đó thực hiện rework điều chỉnh lại. Nếu làm lại slice này, tôi sẽ kiểm tra kích thước chiều cao bằng công cụ đo trên CVAT ngay từ đầu để tuân thủ tuyệt đối ngưỡng H=40px, tránh vẽ thừa các vật thể ở quá xa gây nhiễu cho mô hình.
