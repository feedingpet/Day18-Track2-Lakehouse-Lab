### Dữ liệu của nhóm dễ gặp phải lỗi thiết kế (anti-pattern) nào nhất và giải thích lý do tại sao?

**Lỗi thiết kế (Anti-pattern) dễ gặp nhất:** Data Swamp (Đầm lầy dữ liệu)

**Giải thích lý do:**
Dự án của nhóm xử lý luồng dữ liệu đa phương thức (multi-modal pipeline) bao gồm nhiều định dạng bán cấu trúc và phi cấu trúc phức tạp như tập tin PDF, mã nguồn cũ (legacy code), CSV và đặc biệt là dữ liệu thô trả về từ các mô hình ngôn ngữ lớn (ví dụ: `llm_calls_raw` dạng JSON). 

Với tính chất đa dạng, thiếu đồng nhất và lược đồ (schema) thay đổi liên tục của các loại dữ liệu này, lớp Bronze của Lakehouse rất dễ bị biến thành nơi "đổ đống" mọi thứ mà không được phân loại hay gắn thẻ siêu dữ liệu (metadata) rõ ràng. Nếu các khâu kiểm tra chất lượng (semantic quality control gates) không hoạt động hiệu quả khi làm sạch và chuyển dữ liệu sang lớp Silver, cấu trúc Lakehouse sẽ hoàn toàn mất kiểm soát. Khi đó, dữ liệu trở nên khó truy xuất, thiếu độ tin cậy và không thể phân tích, khiến hệ thống biến thành một "đầm lầy dữ liệu" (Data Swamp) thay vì một kiến trúc Lakehouse hữu ích.
