# SQL Learning

Nơi lưu bài tập và ghi chú học SQL.

Bài 1: HIểu dữ liệu dạng bảng và câu lệnh `SELECT`.
 - Mục tiêu:
   + Đọc cấu trúc một bảng dữ liệu
   + Phân biệt bảng, dòng và cột
   + Hiểu khóa chính
   + Viết câu SQL đầu tiên để xem dữ liệu
   + Chọn những cột cần thiết thay vì lấy toàn bộ bảng
  
1. SQL dùng để làm gì?
   - SQL là ngôn ngữ dùng để làm việc với cơ sở dữ liệu
   - Trong thương mại điện tử, bạn có thể dùng SQL để trả lời:
     + Có bao nhiêu đơn hàng?
     + Đơn hàng nào có doanh thu cao?
     + Sản phẩm nào bán chạy?
     + Doanh thu đến từ kênh nào?
     + Khách hàng nào đã mua hàng?
 => Dữ liệu thường được lưu trong các bảng

2. Bảng, dòng và cột
   Hãy xem bảng `orders` bên dưới:
   order_id | order_date |   product_name  |   channel  | quantity | revenue |
   1001     | 2026-10-01 | Áo thun         | Website    |        2 | 300000  |
   1002     | 2026-10-01 | Giày thể thao   | Shoppe     |        1 | 800000  |
   1003     | 2026-10-02 | Túi xách        | TikTok Shop|        1 | 450000  |
   1004     | 2026-10-02 | Áo thun         | Website    |        3 | 450000  |

   - Bảng
   `orders` là tên của bảng. Bảng này lưu thông tin các đơn hàng
   - Dòng
   Mỗi dòng đại diện cho một bản ghi
     Ví dụ:
   1001 | 2026-10-01 | Áo thun | Website | 2 | 300000 |
    Đây là thông tin của một đơn hàng
   - Cột
     Mỗi cột đại diện cho một thuộc tính:
       + `order_id`: mã đơn hàng
       + `order_date`: ngày đặt hàng
       + `product_name`: tên sản phẩm
       + `channel`: kênh bán hàng
       + `quantity`: số lượng
       + `revenue`: doanh thu
    
3. Khóa chính là gì?
   - `order_id` là khóa chính - Primary Key
   - Khóa chionhs dùng để định danh duy nhất một dòng dữ liệu
   - Ví dụ:
     1001
     1002
     1003
     1004
   - Mỗi mã đơn hàng cần khác nhau. Không nên có hai dòng cùng `order_id = 1001`
   - Trong thực tế:
     + `order_id` có thể là khóa chính của bảng đơn hàng
     + `product_id` có thể là khóa chính của bảng sản phẩm
     + `customer_id` có thể là khóa chính của bảng khách hàng
    
   - Khóa chính giúp chúng ta liên kết các bảng với nhau ở những bài học sau
  
4. Câu SQL đầu tiên: `SELECT`
   - Cấu trúc cơ bản:
       SELECT tên_cột
       FROM tên_bảng
   - Ví dụ:
       SELECT product_name
     FROM orders;
   - Ý nghĩa:
       Lấy cột `product_name` từ bảng `orders`
   - Kết quả:
       product_name
       Áo thun
       Giày thể thao
       Túi xách
       Áo thun

5. Chọn nhiều cột
   - Bạn có thể chọn nhiều cột bằng cách phân cách chúng bằng dấu phẩy
     SELECT order_id, product_name, revenue
     FROM order

   - Kết quả:
    | order_id |  product_name  | revenue |
    |     1001 | Áo thun        | 300000  |
    |     1002 | Giày thể thao  | 800000  |
    |     1003 | Túi xách       | 450000  |
    |     1004 | Áo thun        | 450000  |

- Hãy chú ý:
  + SELECT cho biết muốn xem cột nào
  + FROM cho biết lấy dữ liệu từ bảng nào
  + Dấu ; đánh dấu kết thúc câu lệnh
 
6. Lấy tất cả các cột bằng *
   - Nếu muốn xem toàn bộ bảng:
     SELECT *
     FROM orders;

   - Dấu * nghĩa là tất cả các cột
   - Cách nãy hữu ích khi bạn mới làm quen với một bảng và muốn kiểm tra dữ liệu. Tuy nhiên, khi viết báo cáo thực tế, nên chọn rõ các cột cần dùng:
       SELECT order_id, order_date, revenue
       FROM orders;
     -> Cách viết rõ cột thường dễ đọc và hiệu quả hơn

7. Sắp xếp dữ liệu với ORDER BY
   - Muốn sắp xếp doanh thu từ thấp đến cao:
       SELECT product_name, revenue
       FROM orders
       ORDER BY revenue ASC;
   - Trong đó:
     + ASC: tăng dần
     + DESC: giảm dần
    
   - Muốn xem doanh thu cao nhất trước:
       SELECT product_name, revenue
       FROM orders
       ORDER BY revenue DESC;
       ORDER BY revenue DESC

   - Kết quả:
     |  product_name  | revenue |
     | Giày thể thao  | 800000  |
     | Túi xách       | 450000  |
     | Áo thun        | 450000  |
     | Áo thun        | 300000  |

   - Đây là dạng truy vấn rất thường dùng trong công việc
      "Cho tôi danh sách các đơn hàng hoặc sản phẩm có doanh thu cao nhất"

8. Ghi nhớ quy tặc đọc câu SQL
   - Đọc câu sau:
       SELECT order_id, product_name, revenue
       FROM orders
       ORDER BY revenue DESC;
   - Theo cách tự nhiên:
       Lấy mã đơn hàng, tên sản phẩm và doanh thu từ bảng đơn hàng, sắp xếp doanh thu theo thứ tự giảm dần
   - Bạn có thể nhớ theo thứ tự:
       SELECT -> FROM -> ORDER BY
       Chọn   -> Từ   -> Sắp xếp

9. Bài tập
    Dựa vào bảng orders trên, hãy tự viết SQL cho các yêu cầu sau

   Bài 1: Hiển thị tất cả các cột trong bảng orders
     SELECT *
     FROM orders;
   
   Bài 2: Chỉ hiển thị
     - Mã đơn hàng
     - Tên sản phẩm
     - Kênh bán hàng
          SELECT order_id, product_name, channel
          FROM orders;
        
   Bài 3: Hiển thị tên sản phẩm và số lượng, sắp xếp số lượng từ cao xuống thấp
     SELECT product_name, quantity
     FROM orders
     ORDER BY quantity DESC;
   
   Bài 4: Hiển thị mã đon hàng, ngày đặt hàng và doanh thu, sắp xếp doanh thu từ cao xuống thấp
     SELECT order_id, order_date, revenue
     FROM orders
     ORDER BY revenue DESC;
   
   Bài 5: Liên hệ công việc
       Viết một câu giải thích ngắn:
         Trong công việc thương mại điện tử, câu lệnh `ORDER BY revenue DESC` có thể giúp tôi làm gì?
         Trong công việc thương mại điện tử, câu lệnh `ORDER BY revenue DESC` có thể sắp xếp doanh thu từ cao xuống thấp, từ đó nhanh chóng xác định sản phẩm bán tốt hoặc đơn hàng có giá trị cao để ưu tiên phân tích và hành động kinh doanh
