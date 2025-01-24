Miễn trừ trách nhiệm: Mình không chịu trách nhiệm cho bất cứ hỏng hóc hay lỗi gì xảy ra trong quá trình anh em làm theo, bài này mình chỉ chia sẻ cách mình đã đưa được thông tin từ biến tần lên xem trên Home Assistant, mình cũng không có liên kết hay hợp tác gì với Chisage hay Waveshare cả. Do it at your own risk!

# Giới thiệu
Mình đã sử dụng Chisage ESS Hybrid 6kw được khoảng 1 tháng, đánh giá chung là nó tạm thời đáp ứng được đúng nhu cầu của mình, tuy nhiên phần app để xem thông tin hơi tệ, cập nhật chậm. Mình đã thử tìm cách lấy data trực tiếp từ cái dongle wifi đi kèm nhưng không thành công và không khai thác được, nên mình đã đọc data trực tiếp từ cổng MODBUS của biến tần qua 1 phụ kiện của Waveshare. Cách này hoàn toàn không phụ thuộc vào bất kỳ server nào, data refresh nhanh hơn theo thời gian thực.

# Phụ kiện cần thiết
- 2 cọng dây mạng LAN
- Waveshare RS485 to ETH (B) hoặc RS485 to POE ETH (B) (có thể dùng RS485 to WIFI nhưng giá đắt hơn, mình chỉ có bản dùng dây nên tận dụng luôn)

# Sơ đồ đấu nối

https://prnt.sc/2_JyPX2LfgOI

- Dây LAN thứ 1: Cắm cổng RS485 (cổng dây mạng) từ Waveshare vào router hay switch mạng nhà bạn.
- Dây Lan thứ 2: cắm 1 đầu vào cổng MODBUS của biến tần, đầu còn lại cắt ra lấy 2 dây số 1 và 2 đấu vào cổng A và B của Waveshare.
- Dùng cọng dây điện 2 chân được tặng kèm trong hộp của Chisage, nối 2 vào chân số 23,24 của biến tần, đầu còn lại đấu vào V+ và V- của Waveshare để cấp nguồn cho nó.

# Cài đặt Waveshare
- Download phần mềm Vircom tại đây: https://github.com/vunhutien/chisage-ess-modbus/blob/main/VirCom_en.zip
- Xem video 2 phần cài đặt và cấu hình Waveshare

# Cài đặt Home Assistant
- Mình sử dụng Home Assistant Core trên Raspberry Pi 4, bạn có thể cài trên máy tính, docker, hay máy ảo tùy bạn.
- Cài đặt Modbus integration trên Home Assistant, bạn có thể tham khảo tại đây: https://www.home-assistant.io/integrations/modbus/
- Nếu bạn dùng Home Assistant OS, thì cài thêm cái File Editor để chỉnh sửa file cấu hình, bạn có thể cài qua Add-on Store. Còn nếu bạn dùng Home Assistant Core, hoặc Docker, thì có thể SSH vào máy rồi chỉnh sửa file cấu hình qua terminal.
- Thêm 2 file modbus.yaml và template.yaml vào thư mục config của Home Assistant, nếu bạn dùng File Editor thì có thể tạo file mới và copy nội dung vào, còn nếu dùng SSH thì có thể tạo file trên máy rồi copy vào.
- Mở file configuration.yaml và thêm dòng sau:
```yaml
modbus: !include modbus.yaml
sensor: !include template.yaml
```

Sau đó reset lại Home Assistant, nếu không có lỗi gì thì bạn đã thêm thành công.



