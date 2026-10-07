# CHỌN CHIẾN LƯỢC PHÂN RÃ EPIC HỦY CHUYẾN GHÉP

## Phần 1 - Đề xuất 2 chiến lược phân rã Epic
- **Chiến lược 1: Phân rã theo quy tắc nghiệp vụ (Business Rules).** Tách Epic thành các tính năng dựa trên từng kịch bản, quy định tính phí và xử lý nghiệp vụ khác nhau.
  - *Feature 1:* Khách hủy chuyến ghép cơ bản (Miễn phí khi tài xế chưa nhận).
  - *Feature 2:* Xử lý phí phạt hủy chuyến (Thu 10.000đ khi tài xế đã nhận).
  - *Feature 3:* Xử lý cập nhật giá chuyến đi và thông báo cho các khách hàng đi cùng.

- **Chiến lược 2: Phân rã theo các bước quy trình kỹ thuật (Workflow Steps / Technical Slicing).** Tách Epic dựa theo tiến trình hoạt động từ giao diện người dùng đến xử lý dữ liệu hệ thống.
  - *Feature 1:* Làm giao diện nút bấm hủy chuyến và các màn hình xác nhận cho khách.
  - *Feature 2:* Hệ thống Back-end xử lý lưu trữ yêu cầu hủy và tính toán thời điểm thu phí.
  - *Feature 3:* Hệ thống Back-end tính lại tiền và gửi thông báo (Notification) đến người liên quan.

## Phần 2 - So sánh (Theo tiêu chí INVEST)

| Tiêu chí | Chiến lược 1 (Nghiệp vụ) | Chiến lược 2 (Luồng quy trình kỹ thuật) |
| :--- | :--- | :--- |
| **Independent (Độc lập)** | **(+) Tốt.** Có thể hoàn thiện và ra mắt trước Feature 1 (hủy miễn phí) mà không cần chờ Feature 2, 3 hoàn thành. | **(-) Kém.** Tính năng bị phụ thuộc lẫn nhau, phải có cả Giao diện và xử lý Back-end thì luồng mới chạy được. |
| **Small (Nhỏ gọn)** | **(+) Tốt.** Mỗi quy tắc nghiệp vụ đã được cắt đủ nhỏ, dễ dàng thực hiện gọn gàng trong 1 Sprint. | **(+) Tốt.** Phân chia theo từng khối kỹ thuật hoặc màn hình cũng rất nhỏ, giúp lập trình viên dễ ước lượng. |
| **Valuable (Có giá trị)** | **(+) Tốt.** Mỗi Feature mang lại giá trị thực tế ngay lập tức cho người dùng (vd: làm xong Feature 1 là khách đã có thể hủy). | **(-) Kém.** Nếu chỉ làm xong giao diện (Feature 1) mà chưa có Back-end, tính năng không thể dùng được và vô giá trị với người dùng. |

## Phần 3 - Lựa chọn & Đặc tả
**Lựa chọn:** 
Nên chọn **Chiến lược 1** (Phân rã theo quy tắc nghiệp vụ). Lý do là chiến lược này đáp ứng rất tốt tiêu chí Independent và Valuable của Agile, giúp nhóm phát triển có thể bàn giao được các chức năng mang lại giá trị trọn vẹn cho người dùng ngay sau mỗi Sprint, tránh tình trạng "làm xong giao diện chờ làm dữ liệu" của Chiến lược 2.

**Đặc tả User Story (Dựa theo Chiến lược 1 - Feature 2):**
- **User Story:** Là một khách hàng đặt xe ghép, tôi muốn hệ thống thông báo rõ ràng về khoản phí phạt 10.000đ nếu tôi quyết định hủy sau khi tài xế đã nhận chuyến, để tôi có thể cân nhắc kỹ quyết định hủy của mình.

- **Acceptance Criteria (Kịch bản: Hủy đúng lúc tài xế nhận chuyến):**
  - **Given:** Khách hàng và tài xế bấm thao tác cùng một lúc trên điện thoại, nhưng hệ thống máy chủ (Server) ghi nhận hành động "Tài xế nhận chuyến" thành công vào thời điểm **T**.
  - **When:** Hành động "Khách hàng hủy chuyến" được truyền tới và máy chủ ghi nhận vào thời điểm **T** (hoặc trễ hơn phần nghìn giây).
  - **Then:** Hệ thống phải sử dụng duy nhất đồng hồ của máy chủ làm căn cứ, xác định khách hủy bằng/sau thời điểm tài xế nhận, từ đó tiến hành tính phí 10.000đ và hiển thị thông báo tới khách hàng.
