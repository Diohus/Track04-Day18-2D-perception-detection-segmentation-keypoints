Kết quả thực nghiệm 4C:

- flip_idx giải phẫu: Pose mAP50–95 gốc = 0.4573, gương = 0.4388; giảm 1.85 điểm phần trăm.

- flip_idx đồng nhất: Pose mAP50–95 gốc = 0.4169, gương = 0.2977; giảm 11.92 điểm phần trăm.

Model đồng nhất giảm nhiều hơn model giải phẫu 10.07 điểm phần trăm. Kết quả phù hợp với dự đoán lỗi flip_idx lộ rõ hơn trên ảnh gương.

- flip_idx giải phẫu, chuẩn 1/K: giảm Box mAP50–95 = 1.19, Pose mAP50 = 0.00, Pose mAP50–95 = 1.85 điểm phần trăm.

- flip_idx giải phẫu, độ nhạy: sigma/2: giảm Box mAP50–95 = 1.19, Pose mAP50 = 6.08, Pose mAP50–95 = 1.73 điểm phần trăm.

- flip_idx đồng nhất, chuẩn 1/K: giảm Box mAP50–95 = 0.97, Pose mAP50 = 11.75, Pose mAP50–95 = 11.92 điểm phần trăm.

- flip_idx đồng nhất, độ nhạy: sigma/2: giảm Box mAP50–95 = 0.97, Pose mAP50 = 13.67, Pose mAP50–95 = 1.34 điểm phần trăm.

Box mAP không đo danh tính trái/phải của keypoint. Nếu Box mAP giảm ít nhưng Pose mAP giảm nhiều, box metric đã che lỗi pose trong lần chạy này. Nếu Pose mAP50 giảm ít hơn mAP50–95, ngưỡng OKS 0.5 che một phần sai số. Cần đọc các mức giảm trên để xác định trường hợp thực tế, không kết luận chỉ từ tên metric.

Sigma nhỏ làm OKS nhạy hơn với sai số tọa độ. Chỉ so hai model trong cùng một bộ sigma; mAP khác sigma không phải cùng thước đo. Phép thử sigma/2 là kiểm tra độ nhạy, không chứng minh đó là dung sai đúng của dữ liệu.

Thiết kế val: có hổ quay trái và phải thật, cân bằng hướng nhìn, thêm chân che nhau/cắt mép/nhiều kích thước; thống nhất nhãn giải phẫu và chia train/val theo cá thể hoặc nguồn ảnh để tránh rò rỉ. Báo cáo riêng từng hướng, Box mAP, Pose mAP50 và mAP50–95; xem thêm sai số từng keypoint và các ca tăng OKS sau hoán đổi trái/phải. Val gương là kiểm tra có kiểm soát, chưa thay thế ảnh triển khai thật.

Một seed và 53 ảnh val chưa đủ khẳng định khác biệt có ý nghĩa thống kê; nên lặp nhiều seed và bootstrap theo cặp ảnh gốc/gương.

Chưa có nhãn lặp độc lập nên chưa thực hiện phần sigma tự ước lượng của lựa chọn bài tập về nhà 1.