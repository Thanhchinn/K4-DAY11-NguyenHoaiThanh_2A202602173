# Quan sát vạch ô đỗ

- Hai vạch `parking_line` đã vẽ (mô tả vị trí trong ảnh): Các đoạn vạch sơn trắng chia ranh giới các ô đỗ riêng lẻ ở tiền cảnh (hàng ô đỗ phía dưới đáy ảnh bên trái và bên phải, tạo thành ranh giới phân định từng vị trí đỗ xe).
- Một vạch/dấu sơn hoặc biên **không** vẽ, và vì sao: Dải sơn dài phân chia tim đường lối xe chạy và các vạch kẻ xa ở hậu cảnh không được vẽ gán nhầm thành `parking_line` vì chúng có chức năng phân luồng di chuyển hoặc cảnh báo mép đường, không phải vạch phân chia ranh giới một ô đỗ riêng lẻ.
- Polygon `free_space` dừng ở đâu; có phần bị che nào không: Polygon `free_space` bao trùm phần mặt đường nhựa trống của lối xe chạy chính giữa các dãy ô đỗ; dừng chính xác tại mép ranh giới các ô đỗ xe và gờ vỉa hè (curb), không đè qua vỉa hè hay vật cản, không bị che khuất.
- Ca chưa chắc cần hỏi người soát (nếu không có, ghi “không có”): không có
