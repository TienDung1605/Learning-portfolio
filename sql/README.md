# SQL Learning

Nơi lưu bài tập và ghi chú học SQL.

I. Bài 1: HIểu dữ liệu dạng bảng và câu lệnh `SELECT`.
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


II. Bài 2: Lọc dữ liệu bằng WHERE
 - WHERE dùng để chỉ lấy những dòng thỏa màn một điều kiện

 - Ví dụ 1: Lọc theo kênh bán hàng
    SELECT *
    FROM orders
    WHERE channel = 'Website'
- Ý nghĩa:
   Chỉ hiển thị các đơn hàng đến từ kênh Website
- Chuỗi chữ như 'Website' cần đặt trong dấu nháy đơn

- Ví dụ 2: Lọc đơn hàng có doanh thu lớn hơn 400000
   SELECT order_id, product_name, revenue
   FROM orders
   WHERE revenue > 400000

- Các toán tử thường dùng
  | Toán tử | Ý nghĩa              |
  | =       | bằng                 |
  | >       | lớn hơn              |
  | <       | nhỏ hơn              |
  | >=      | Lớn hơn hoặc bằng    |
  | <=      | nhỏ hơn hoặc bằng    |
  | <>      | khác                 |

- Kết hợp WHERE và ORDER BY
   SELECT order_id, product_name, channel, revenue
   FROM orderes
   WHERE channel = 'Website'
   ORDER BY revenue DESC;

- Cách đọc:
   Lấy các đơn hàng từ Website và sắp xếp theo doanh thu giảm dần

- Thứ tự viết câu lệnh là:
  SELECT
  FROM
  WHERE
  ORDER BY
- Không viết ORDER BY trước WHERE

BÀI TẬP MỚI
 Dùng bảng orders giống bài trước
 Bài 6: Hiển thị tất cả đơn hàng đến từ kênh Website
  SELECT *
  FROM orders
  WHERE channel = 'Website';
  
 Bài 7: Hiển thị mã đơn hàng, tên sản phẩm và doanh thu của các đơn hàng có doanh thu lớn hơn 400000
  SELECT order_id, product_name, revenue
  FROM orders
  WHERE revenue > 400000;
  
 Bài 8: Hiển thị các đơn hàng có số lượng từ 2 trở lên, sắp xếp số lượng từ cao xuống thấp
  SELECT *
  FROM orders
  WHERE quantity >= 2
  ORDER BY quantity DESC;
  
 Bài 9: Hiển thị mã đơn hàng, sản phẩm và doanh thu của các đơn hàng từ kênh Website, sắp xếp doanh thu giảm dần
  SELECT order_id, product_name, revenue
  FROM orders
  WHERE channel = 'Website'
  ORDER BY revenue DESC
  
 Bài 10: Giải thích bằng lời câu SQL sau:
   SELECT product_name, revenue
   FROM orders
   WHERE revenue >= 450000
   ORDER BY revenue DESC;
   ORDER BY revenue DESC;
Lấy tên các sản phẩm và doanh thu của những đơn hàng có doanh thu lớn hơn hoặc bằng 450000, sau đó sắp xếp các kết quả theo doanh thu từ cao xuống thấp

III. Bài 3: nhiều điều kiện với AND và OR
 1. Dùng AND
    `AND` nghĩa là đồng thời thỏa mãn tất cả điều kiện
 - Ví dụ:
   SELECT order_id, product_name, revenue
   FROM orders
   WHERE channel = 'Website'
   AND revenue >= 400000;
 - Ý nghĩa:
   Lấy các đơn hàng vừa đến từ Website, vừa có doanh thu 400000 trở lên

2. Dùng OR
  - `OR` nghĩa là thỏa mã ít nhất một trong các điều kiện
    SELECT order_id, product_name, channel
    FROM orders
    WHERE channel = 'Website'
    OR channel = 'Shoppe'
  - Ý nghĩa
    Lấy các đơn hàng đến từ Website hoặc Shoppe

3. Kết hợp với điều kiện và sắp xếp
   SELECT order_id, product_name, channel, revenue
   FROM orders
   WHERE channel = 'Website'
   AND revenue >= 400000
   ORDER BY revenue DESC
 - Thứ tự câu lệnh vẫn là:
   SELECT
   FROM
   WHERE
   ORDER BY

4. Bài tập
   Bài 11: Lấy mã đơn hàng, sản phẩm và doanh thu của các đơn hàng:
    + Đến từ `Website`
    + Có doanh thu từ 400000 trở lên
       SELECT order_id, product_name, revenue
       FROM orders
       WHERE channel = 'Website'
       AND revenue >= 400000;
      
   Bài 12: Lấy tất cả đơn hàng đến từ `Website` hoặc `Shoppe`
     SELECT *
     FROM orders
     WHERE channel = 'Website'
     OR channel = 'Shoppe';
   
   Bài 13: Lấy mã đơn hàng, sản phẩm, số lượng và doanh thu của các đơn hàng:
    + Có số lượng từ 2 trở lên
    + Có doanh thu từ 400000 trở lên
    + Sắp xếp doanh thu giảm dần
       SELECT order_id, product_name, quantity, revenue
       FROM orders
       WHERE quantity >= 2
       AND revenue >= 400000
       ORDER BY revenue DESC;
       
   Bài 14: Giải thích câu SQL sau bằng lời
     SELECT order_id, product_name, channel, revenue
     FROM orders
     WHERE channel = 'Shoppe'
     OR revenue >= 700000
     ORDER BY revenue DESC;
       Lấy mã đơn hàng, tên sản phẩm, kênh bán hàng và doanh thu của những đơn hàng đến từ kênh bán hàng Shoppe hoặc doanh thu lớn hơn hoặc bằng 700000, sau đó sắp xếp các đơn hàng có doanh thu từ cao xuống thấp
   Bài 15: suy nghĩ nghiệp vụ
     Trong công việc thương mại điện tử, trường hợp nào nên dùng AND, và trường hợp nào nên dùng OR?
      Trong công việc thương mại điện tử, trường hợp lấy thỏa mãn tất cả các điều kiện thì dùng AND và trường hợp chỉ cần thỏa mãn ít nhất một trong các điều kiện thì dùng OR

IV. Bài 4: Các hàm tổng hợp cơ bản
 1. COUNT - Đếm
    - Đếm số dòng trong bảng
      SELECT COUNT(*) AS total_rows
      FROM order
     + Kết quả
      | total_rows |
      |          4 |
     + COUNT(*) đếm tất cả các dòng, kể cả khi một số cột có giá trị trống
   

    - Đếm một cột
      SELECT COUNT(order_id) AS total_orders
      FROM orders;
      + Nếu order_id không vị trống, kết quả cũng là 4
     
    - Lưu ý về COUNT
      COUNT(*)
      + Đếm tất cả các dòng
      COUNT(column_name)
      + Chỉ đếm các dòng một cột đó không bị NULL
      + Trong phân tích số đơn hàng, thường dùng
        COUNT(order_id)
        Hoặc
        COUNT(*)
        Tùy cấu trúc dữ liệu

     - SUM - Tính tổng
       + Tính tổng doanh thu
         SELECT SUM(revenue) AS total_revenue
         FROM orders;
   
       + Tính tổng số lượng sản phẩm
         SELECT SUM(quantity) AS total_quantity
         FROM orders;

       + Với dũ liệu mẫu:
         Tổng doanh thu = 300000 + 800000 + 450000 + 450000 = 2000000

     - AVG - Tính trung bình
       SELECT AVG(revenue) AS average_revenue
       FROM orders;

       + Doanh thu trung bình mỗi dòng đơn hàng là:
         2000000 / 4 = 500000

      - MIN và MAX
        + Doanh thu thấp nhất:
          SELCET MIN(revenue) AS minimuim_revenue
          FROM orders;

        + Doanh thu cao nhất
          SELECT MAX(revenue) AS maximum_revenue
          FROM orders

        + Có thể dùng nhiều hàm trong cùng một câu
          SELECT
             COUNT(*) AS total_orders,
             SUM(quantity) AS total_quantity,
             SUM(revenue) AS total_revenue,
             AVG(revenue) AS average_revenue,
             MIN(revenue) AS minimum_revenue,
             MAX(revenue) AS maximum_revenue,
          FROM orders;

        + Kết quả dự kiến:
| total_orders | total_quantity | total_revenue | average_revenue | minimum_revenue | maximum_revenue |
|            4 |              7 |       2000000 |          500000 |          300000 |          800000 |

 2. Bí danh với AS
    - Trong câu lệnh:
       SUM(revenue) AS total_revenue
      + SUM(revenue) là phép tính
      + AS total_revenue đặt tên dễ hiểu cho cột kết quả
     
    - Nếu không dùng AS, tên cột có kết quả có thể khó đọc như:
       sum(revenue)
    - Nên tạo bí danh rõ ràng
       COUNT(*) AS total_orders
       SUM(revenue) AS total_revenue
       AVG(revenue) AS average_revenue

 3. GROUP BY dùng để làm gì?
    - Nếu không có GROUP BY, các hàm tổng hợp tính trên toàn bộ bảng
    - Ví dụ:
      SELECT SUM(revenue) AS total_revenue
      FROM orders
    - Kết quả là tổng doanh thu của tất cả các kênh
    - Nếu muốn tính doanh thu theo từng kênh, dùng:
      SELECT
         channel,
         SUM(revenue) AS total_revenue
      FROM orders
      GROUP BY channel
    - Kết quả:
      | channel     | total_revenue |
      | Website     |        750000 |
      | Shopee      |        800000 |
      | TikTok Shop |        450000 |

    - Cách đọc:
      Nhóm các dòng theo channel, sau đó tính tổng revenue trong từng nhóm

 4. Đếm số đơn hàng theo kênh
    SELECT
       channel,
       COUNT(*) AS total_orders
    FROM orders
    GROUP BY channel;

    | channel     | total_orders |
    | Website     |            2 |
    | Shopee      |            1 |
    | TikTok Shop |            1 |

    - Đây là câu hỏi kinh doanh thường gặp:
       Mỗi kênh đang có bao nhiêu đơn hàng?

5. Tính nhiều chỉ số theo nhóm
   - Bạn có thể tính nhiều hàm tổng hợp cùng lúc:
      SELECT
          channel,
          COUNT(*) AS total_orders,
          SUM(quantity) AS total_quantity,
          SUM(revenue) AS total_revenue,
          AVG(revenue) AS average_revenue
      FROM orders
      GROUP BY channel;
    - Kết quả dự kiến
      | channel        | total_orders | total_quantity | total_revenue | average_revenue |
      | Website        |            2 |              5 |        750000 |          375000 |
      | Shopee         |            1 |              1 |        800000 |          375000 |
      | TikTok Shop    |            1 |              1 |        450000 |          375000 |
    - Đây đã là một báo cáo kinh doanh nhỏ
  
6. Quy tắc quan trong khi dùng GROUP BY
   - Khi dùng GROUP BY, các cột trong SELECT thường phải thuộc một trong hai loại:
      1. Có trong GROUP BY
      2. Được sử dụng với hàm tổng hợp
    
   - Câu đúng:
        SELECT channel, SUM(revenue)
        FROM orders
        GROUP BY channel
   - Vì:
      + channel có trong GROUP BY
      + revenue được tính bằng SUM
    
   - Câu dễ sai:
      SELECT channel, product_name, SUM(revenue)
      FROM orders
      GROUP BY channel;

   - Vì product_name không có trong GROUP_BY và cũng không nằm trong hàm tổng hợp
   - Nếu muốn nhóm theo cả kênh và sản phẩm:
      SELECT
         channel,
         product_name,
         SUM(revenue) AS total_revenue
      FROM orders
      GROUP BY channel, product_name

7. Sắp xếp kết quả nhóm
   - Muốn xem kênh có tổng doanh thu cao nhất trước:
     SELECT
        channel,
        SUM(revenue) AS total_revenue
     FROM orders
     GROUP BY channel
     ORDER BY total_revenue DESC
   - Có thể dùng bí danh total_revenue trong ORDER BY
   - Câu này trả lời:
        Kênh bán hàng nào đang tạo ra nhiều doanh thu nhất?

8. Kết hợp WHERE với GROUP BY
   - Ví dụ: chỉ tính doanh thu của các đơn hàng từ Website:
     SELECT
        channel,
        SUM(revenue) AS total_revenue
     FROM orders
     WHERE channel = 'Website'
     GROUP BY channel;

   - Thứ tự câu lệnh
     SELECT
     FROM
     WHERE
     GROUP BY
     ORDER BY

   - Cách hoạt động:
     1. FROM: lấy dữ liệu từ orders
     2. WHERE: lọc những dòng cần thiết
     3. GROUP BY: gom các dòng thành nhóm
     4. SELECT: Tính và hiển thị kết quả
     5. ORDER BY: sắp xếp kết quả
    
9. Phân biệt COUNT(*) và COUNT(DISTINCT ...)
    - Nếu bảng có nhiều dòng cho cùng một đơn hàng, COUNT(*) có thể không đại diện cho số đơn hàng duy nhất
    - Ví dụ:
         SELECT COUNT(*) AS total_rows
         FROM orders;

   - Đếm số dòng
   - Nếu muốn đếm số mã đơn hàng khác nhau:
     SELECT COUNT(DISTINCT order_id) AS unique_orders
     FROM orders;
      + DISTINCT loại bỏ giá trị trùng lặp
   =>  Trong dữ liệu đơn giản, mỗi dòng là một đơn hàng thì hai cách có thể cho cùng kết quả. Nhưng trong dữ liệu thực tế, cần hiểu cấu trúc bảng trước khi kết luận

10. Bài tập
    Hãy dùng bảng orders mẫu để làm các bài sau
    1. Bài 16: Tính tổng doanh thu của toàn bộ bảng
      SELECT
         revenue
         SUM(revenue) AS total_revenue,
      FROM orders;
      
    3. Bài 17: Đếm tổng số dòng hoặc số đơn hàng trong bảng
     - Đếm số dòng
      SELECT COUNT(*) AS total_rows
       FROM orders;

     - Đếm số đơn hàng trong bảng
          SELECT COUNT(order_id) AS total_orders
          FROM orders;
       
    4. Bài 18: Tính tổng số lượng sản phẩm đã bán
      SELECT SUM(quantity) AS total_quantity
      FROM orders;

    6. Bài 19: Tính doanh thu theo từng kênh bán hàng
       Kết quả cần có:
        + Tên kênh
        + Tổng doanh thu
      
         SELECT
            channel,
            SUM(revenue) AS total_revenue
         FROM orders
         GROUP BY channel;
      
    8. Bài 20: Đếm số đơn hàng theo từng kênh bán hàng
       Kết quả cần có:
        + Tên kênh
        + Đơn hàng
      
         SELECT
            channel,
            COUNT(*) AS total_orders
         FROM orders;
      
    10. Bài 21: Tính các chỉ số sau theo từng kênh:
       + Số đơn hàng
       + Tổng số lượng sản phẩm
       + Tổng doanh thu
       + Doanh thu trung bình
   
         SELECT
            channel,
            COUNT(*) AS total_orders,
            SUM(quantity) AS total_quantity,
            SUM(revenue) AS total_revenue,
            AVG(revenue) AS total_revenue
         FROM orders
         GROUP BY channel;
      
    11. Bài 22: Hiển thị các kênh bán hàng theo thứ tự tổng doanh thu từ cao xuống thấp
      SELECT
        channel,
        SUM(revenue) AS total_revenue,
      FROM orders
      GROUP BY channel
      ORDER BY total_revenue DESC;

    13. Bài 23: Suy nghĩ nghiệp vụ
       Giải thích câu SQL sau bằng lời:
          SELECT
             channel,
             COUNT(*) AS total_orders,
             SUM(revenue) AS total_revenue
          FROM orders
          GROUP BY channel
          ORDER BY total_revenue DESC

        - Nhóm các đơn hàng theo từng kênh bán hàng, đếm số đơn hàng tính tổng doanh thu của mỗi kênh. Sau đó sắp xếp các kênh theo tổng doanh thu từ cao xuống thấp

    15. Bài 24: Phát hiện lỗi
        Câu SQL sau có vấn đề gì?
          SELECT channel, product_name, SUM(revenue) AS total_revenue
          FROM orders
          GROUP BY channel;
        - product_name không nằm trong GROUP BY
