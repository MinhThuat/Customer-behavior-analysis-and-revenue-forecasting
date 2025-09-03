# Project Summary: Customer Behavior Analysis and Revenue Forecasting

## 1. Mục tiêu dự án

- Dự án gồm 4 mục tiêu chính sau đây:
    + Phân tích hành vi khách hàng từ dữ liệu giao dịch.
    + Phân cụm khách hàng sử dụng các chỉ số RFM và thuật toán Kmeans để xác định các nhóm khách hàng có hành vi tương tự nhau.
    + Mô phỏng tác động của các chiến lược giả định dựa vào các chỉ số Retention, Frequency và AOV vào doanh thu.
    + Xây dựng Dashboard trực quan hóa dữ liệu bằng PowerBI để hỗ trợ ra quyết định kinh doanh cho công ty.

## 2. Nguồn dữ liệu

- Bộ dữ liệu được lấy từ UCI Machine Learning. Đường link: https://archive.ics.uci.edu/dataset/352/online+retail. Bộ dữ liệu bao gồm tập hợp các giao dịch của các khách hàng từ 1/12/2010 đến 9/12/2011 ở UK của một công ty bán lẻ trực tuyến không thông qua cửa hàng. Công ty chủ yếu bán các món hàng quà tặng độc đáo và khách hàng đa số là các nhà buôn bán sỉ.
    
- Để đưa vào PowerBI sau quá trình xử lý được tách ra thành các bảng chính:
    + orders_details: Chi tiết đơn hàng
    + sales_by_month: Doanh thu theo tháng
    + customer_rfm: Điểm RFM theo từng khách hàng
    + cluster_summary: Kết quả tóm tắt phân cụm
    + strategy_impact: Kịch bản chiến lược giả định

## 3. Công cụ và kỹ thuật sử dụng

### Ngôn ngữ **Python**:

- Tiền xử lý dữ liệu: Sử dụng Pandas để loại bỏ các giá trị thiếu, lặp. Chuyển đổi kiểu dữ liệu, tạo thêm các cột cần thiết
- EDA: Sử dụng matplotlib và seaborn để trực quan hóa dữ liệu. Tìm các insight và đưa ra các câu hỏi cần thiết đồng thời đưa ra các nhận định liên quan.
- Thuật toán Kmeans để phân cụm khách hàng dựa vào các điểm số R-F-M. Những người có những hành vi tương đồng như thời gian mua kể từ lần cuối, số tiền đã sử dụng cho việc thanh toán, tần suất mua trong quá trình được khảo sát sẽ được đưa về 1 nhóm. Sau thuật toán, những khách hàng trong bộ dữ liệu được chia làm 3 nhóm: Leave (những người có xu hướng rời bỏ, rất lâu rồi chưa mua lại, số tiền sử dụng ít và tần suất mua thấp), Stable and Potential (những người có xu hướng trung thành, mua nhiều lần và có số tiền sử dụng tương đối và tần suất mua trung bình), VIP (những người có xu hướng mua nhiều lần, số tiền sử dụng nhiều và tần suất mua cao).

### Công cụ trực quan: **PowerBI**

- Sử dụng các công thức DAX để tính toán các chỉ số cần thiết.
- Tạo các biểu đồ chi tiết hơn để tìm ra insight dữ liệu.

### Kỹ thuật phân tích:

- RFM Analysis: sử dụng các chỉ số R (Recency), F (Frequency) và M (Monetary) để xác định các nhóm khách hàng có hành vi tương tự nhau.
- Customer Segmentation (Clustering): Sử dụng thuật toán Kmeans để phân cụm khách hàng dựa trên các chỉ số RFM.
- Suggetion Strategy: Sử dụng các chỉ số Retention, Frequency và AOV để mô phỏng tác động của các chiến lược giả định vào doanh thu.

## 4 Kết quả chính

- Xác định được 3 nhóm khách hàng với các hành vi mua hàng khác nhau. Những nhóm khách hàng này có thể áp dụng các chiến lược khác nhau để tối ưu doanh thu và chi phí vận hành các chiến dịch.
- Đề xuất các chiến lược hợp lý cho từng nhóm. Các chiến lược sẽ sử dụng thêm các trọng số trên từng yếu tố để không bị phóng đại doanh thu kỳ vọng. Dự án sử dụng 3 yếu tố chính để đánh giá 1 chiến lược tác động vào doanh thu dựa vào doanh thu hiện tại là: retention rate (% khách hàng quay lại hoặc giữ lại thêm), frequency uplift (số lần mua tăng thêm của 1 khách hàng), aov uplift (% giá trị đơn hàng tăng thêm dựa vào cross-sell, upsell).

### Các chiến lược được đề xuất trong dự án gồm 4 kịch bản:

- Kịch bản 1: Tăng trưởng nhanh những rủi ro cao:

    + Đối với nhóm khách hàng rời bỏ (1) ta dự định sẽ tung ra chiến dịch tặng voucher để lôi kéo họ quay lại tập trung vào Retention và do họ quay lại thì freq_uplift có thể tăng nhẹ nhưng AOV của họ sẽ thấp.
    + Đối với nhóm khách hàng tiềm năng và ổn định (0) ta chăm sóc bằng email và sẽ làm tăng khả năng mua thêm của nhóm này ta có retention_target vừa phải do nhóm này rủi ro rời bỏ không quá cao. Khuyến khích họ mua nhiều hơn với các chương trình giảm giá đồng thời thúc đấy AOV tăng nhẹ bằng upsell ở giỏ hàng.
    + Đối với nhóm khách hàng VIP (2) ta dự định tặng VIP membership và dự kiến họ sẽ mua nhiều hơn một chút các chỉ số retention_target = 0.15, freq_uplift = 0.1, aov_uplift = 0.2 (tăng 20% giá trị đơn hàng). Cần đặt nặng vào AOV và Frequency ít hơn ở Retention

- Kịch bản 2: Thận trọng tăng trưởng bền vững với rủi ro ở mức thấp nhất:

    + Khách hàng rời bỏ: Tập trung giữ chân, ít ưu tiên cross-sell hơn retention_target = 0.1. Tăng tần suất mua của nhóm này ở mức thấp freq_uplift = 0.1 kéo theo AOV gần như không đổi aov_uplift = 0.01. Trọng số nghiêng mạnh về retention
    + Khách hàng VIP: Chủ yếu giữ chân và ít tập trung vào 2 yếu tố còn lại. retention_target = 0.05, freq_uplift = 0.05, aov_uplift = 0.01.
    + Khách hàng tiềm năng và ổn định: Chiến dịch nhẹ nhàng tập trung cao vào độ ổn định. retention_target = 0.05, freq_uplift = 0.1, aov_uplift = 0.02.

- Kịch bản 3: Tối ưu chi phí giữ chân khách hàng nhiều nhất có thể với chi phí tối ưu nhất

    + Khách hàng rời bỏ: cố gắng tăng retention (0.05) và không tập trung tăng freq và aov.
    + Khách hàng VIP: Gần như giữ nguyên và không đẩy nhiều khuyến mãi
    + Khách hàng tiềm năng và ổn định: tăng nhẹ AOV bằng cross-sell

- Giả định rằng từng chiến dịch ở mỗi kịch bản đều thành công thì doanh thu kỳ vọng cho thấy với Kịch bản 1 cho mức tăng trưởng 22,33%, Kịch bản 2 cho mức tăng trưởng 5,89% và Kịch bản 3 cho mức tăng trưởng 0,90.

## 5 Dashboard 

- Sử dụng PowerBI trực quan hóa dữ liệu gồm 3 trang.
    + Trang 1: Trực quan hóa doanh thu (theo từng tháng, quý, năm). Các sản phẩm cho doanh thu cao nhất, các khách hàng đóng góp nhiều vào doanh thu nhất. Số lượng đơn hàng theo quý, năm. Doanh thu tổng hợp theo từng quốc gia mua hàng.
    + Trang 2: Tỷ trọng khách hàng theo từng nhóm, doanh thu theo từng nhóm, phân bố của nhóm theo các chỉ số RFM.
    + Trang 3: Thay đổi doanh thu theo các yếu tố, doanh thu kỳ vọng theo từng kịch bản và doanh thu kỳ vọng theo từng nhóm.

- Link PowerBI Service: https://app.powerbi.com/links/aM35kkihLh?ctid=40127cd4-45f3-49a3-b05d-315a43a9f033&pbi_source=linkShare

## 6 Kết luận 

- Qua quá trình phân tích, xử lý và đánh giá rút ra được một số kết luận quan trọng:
    + Hiểu rõ hành vi khách hàng theo từng phân khúc, theo từng mùa trong năm: Phân cụm khách hàng có sự khác biệt rõ rệt về tần suất mua và giá trị đơn hàng giữa các nhóm.
    + Yếu tố thời gian, mùa vụ lễ hội cũng ảnh hưởng đến hành vi mua hàng. Các dịp lễ lớn trong năm thường thu hút nhiều khách hàng mua hàng hơn. Các sản phẩm chủ lực cũng đóng vai trò quan trọng trong việc tăng trưởng doanh thu

- Xác định cơ hội tăng trưởng doanh thu:
    + Nắm bắt về thời gian cao điểm trong năm có thể làm tăng trưởng doanh thu.
    + Xác định các sản phẩm chủ lực, mở rộng mẫu mã.
    + Nắm bắt tâm lý của từng nhóm khách hàng. Nhóm khách hàng rời bỏ mặc dù đã lâu không mua và tần suất mua thấp nhưng số tiền trung bình họ bỏ ra cũng khá lớn nên có thể đưa ra thêm các chiến lược giữ chân định kỳ hoặc các chương trình khuyến mãi vào mùa lễ hội.

- Các kịch bản giả định mang lại hiệu quả tăng doanh thu đáng kể:
    + Mô phỏng chiến dịch cho thấy việc cải thiện các chỉ số như Frequency và AOV có thể giúp tăng doanh thu đáng kể.
    + Cân nhắc chi phí bỏ ra cũng là một phần quan trọng trong việc cải thiện doanh thu.