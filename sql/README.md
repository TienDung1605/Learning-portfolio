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

    14. Bài 24: Phát hiện lỗi
        Câu SQL sau có vấn đề gì?
          SELECT channel, product_name, SUM(revenue) AS total_revenue
          FROM orders
          GROUP BY channel;
        - product_name không nằm trong GROUP BY
       
11. Bài làm thêm
     1. Bài 1: Viết câu SQL tính tổng số lượng sản phẩm theo từng sản phẩm, sắp xếp từ nhiều đến ít
         SELECT
             product_name,
             SUM(quantity) AS total_quantity
         FROM orders
         GROUP BY product_name
         ORDER BY total_quantity DESC;

     2. Bài 2: Viết câu SQL đếm số đơn hàng theo từng kênh, sắp xếp từ nhiều đến ít
         SELECT
            channel,
            COUNT(*) AS total_order
         FROM orders
         GROUP BY channel
         ORDER BY total_order DESC;
     3. Bài 3: Viết câu SQL tính tổng doanh thu theo từng kênh, sắp xếp từ thấp đến cao
         SELECT
             channel,
             SUM(revenue) AS total_revenue
         FROM orders
         GROUP BY channel
         ORDER BY total_revenue ASC;

     4. Bài 4: Câu lệnh sau làm gì?
        SELECT
          product_name,
          AVG(revenue) AS average_revenue
        FROM orders
        GROUP BY product_name
        ORDER BY average_revenue DESC;
          - Câu lệnh này tính doanh thu trung bình của từng sản phẩm, sau đó sắp xếp theo thứ tự giảm dần
    
     5. Bài 5: Trong câu sau, phần nào là GROUP BY, phần nào là ORDER BY
        SELECT
           channel,
           SUM(revenue) AS total_revenue
        FROM orders
        GROUP BY channel
        ORDER BY total_revenue DESC
          - GROUP BY channel dùng để gom dữ liệu theo từng kênh bán hàng. SUM(revenue) tính tổng doanh thu của mỗi kênh. ORDER BY total_revenue DESC sắp xếp các kênh theo tổng doanh thu giảm dần

V. HAVING - câu lệnh dùng để lọc kết quả sau khi đã GROUP BY
   1. Nhắc lại sự khác nhau giữa WHERE và HAVING
      - WHERE
         + WHERE lọc các dòng dữ liệu ban đầu, trước khi nhóm
         + Ví dụ:
             SELECT *
             FROM order
             WHERE channel = 'Website';
         + Ý nghĩa: Chỉ lấy các đơn hàng từ Website
       
      - HAVING
         + HAVING lọc các nhóm sau khi đã tổng hợp
         + Ví dụ:
              SELECT
                 channel,
                 SUM(revenue) AS total_revenue
              FROM orders
              GROUP BY channel
              HAVING SUM (revenue) > 1000000;
        + Ý nghĩa: Gom dữ liệu theo kênh, tính tổng doanh thu, rồi chỉ giữ lại những kênh có tổng doanh thu lớn hơn 1000000
       
   2. Vì sao không dùng WHERE để lọc tổng doanh thu ?
      - Câu sau thường sai:
           SELECT
              channel,
              SUM(revenue) AS total_revenue
           FROM orders
           WHERE total_revenue > 1000000
           GROUP BY channel;
        + Lý do: total_revenue là kết quả được tạo ra sau khi GROUP BY và SUM() thực hiện. Ở bước WHERE, kết quả này chưa tồn tại
        + Khi điều kiện liên quan đến:
          • SUM()
          • COUNT()
          • AVG()
          • MIN()
          • MAX()
          thường phải dùng HAVING

   3. Ví dụ đơn giản
      - Giả sử kết quả tổng doanh thu theo kênh là:
        | channel     | total_revenue  |
        | Website     |         950000 |
        | Shopee      |        1700000 |
        | TikTok Shop |         450000 |

      - Muốn chỉ xem các kênh có doanh thu trên 1000000:
        SELECT
           channel,
           SUM(revenue) AS total_revenue
        FROM orders
        GROUP BY channel
        HAVING SUM(revenue) > 1000000;
         + Kết quả:
           | channel | total_revenue  |
           | Shopee  |        1700000 |

   4. Lọc theo số lượng đơn hàng
      SELECT
         channel,
         COUNT(*) AS total_orders
      FROM orders
      GROUP BY channel
      HAVING COUNT(*) >= 2;
      - Ý nghĩa: Chỉ hiển thị những kênh có ít nhất 2 đơn hàng
     
      - Bạn cũng có thể dùng bí danh:
        SELECT
           channel,
           COUNT(*) AS total_orders
        FROM orders
        GROUP BY channel
        HAVING total_orders >= 2;

      - Tuy nhiên, khả năng dùng bí danh trong HAVING có thể khác nhau tùy hệ quản trị cơ sơ dữ liệu. Cách an toàn và phổ biến là viết lại hàm
        HAVING COUNT(*) >= 2

   5. Kết hợp WHERE, GROUP BY, HAVING và ORDER BY
      - Ví dụ:
        + Trong các đơn hàng từ Website, tìm những sản phẩm có tổng doanh thu ít nhất 400000 và sắp xếp giảm dần
          SELECT
             product_name,
             SUM(revenue) AS total_revenue
          FROM orders
          WHERE channel = 'Website'
          GROUP BY product_name
          HAVING SUM(revenue) >= 400000
          ORDER BY total_revenue DESC;

      + Câu lệnh này thực hiện theo thứ tự:
        1. FROM orders: lấy dữ liệu từ bảng orders
        2. WHERE channel = 'Website': chỉ giữ đơn hàng Website
        3. GROUP BY product_name: gom theo sản phẩm
        4. SUM(revenue): tính tổng doanh thu từng sản phẩm
        5. HAVING SUM(revenue) >= 400000: chỉ giữ sản phẩm đạt ngưỡng
        6. ORDER BY total_revenue DESC: sắp xếp doanh thu giảm dần
       
   6. So sánh trực tiếp WHERE và HAVING
      - Lọc dòng trước khi nhóm
        SELECT
           channel,
           SUM(revenue) AS total_revenue
        FROM orders
        WHERE revenue >= 400000
        GROUP BY channel;
        + Ý nghĩa: Chỉ lấy những dòng đơn hàng có doanh thu từ 400000 trở lên, sau đó tính tổng theo kênh
       
      - Lọc nhóm sau khi nhóm
        SELECT
           channel,
           SUM(revenue) AS total_revenue
        FROM orders
        GROUP BY channel
        HAVING SUM(revenue) >= 400000
        + Ý nghĩa: Tính tổng doanh thu của từng kênh, sau đó chỉ giữ các kênh có tổng doanh thu từ 400000 trở lên
     => Hai câu lệnh này không giống nhau
        + WHERE revenue >= 400000: lọc từng đơn hàng
        + HAVING SUM(revenue) >= 400000: lọc tổng doanh thu của từng kênh
       
   7. Ví dụ để thấy sự khác biệt
      - Dữ liệu:
         | channel | revenue |
         | Website |  300000 |
         | Website |  450000 |
         | Website |  200000 |
         | Shopee  |  800000 |
         | Shopee  |  900000 |
     - Trường hợp dùng WHERE
        SELECT
           channel,
           SUM(revenue) AS total_revenue
        FROM orders
        WHERE revenue >= 400000
        GROUP BY channel;

        + SQL loại bỏ các dòng 300000 và 200000 trước, rồi tính:
          | channel | total_revenue  |
          | Website |         450000 |
          | Shopee  |        1700000 |
     - Trường hợp dùng HAVING
          SELECT
             channel,
             sum(revenue) AS total_revenue
          FROM orders
          GROUP BY channel
          HAVING SUM(revenue) >= 400000;
       + SQL tính tổng đầy đủ trước:
         | channel | total_revenue  |
         | Website |         950000 |
         | Shopee  |        1700000 |
       -> Sau đó lọc nhóm. Cả hai kênh đều được giữ lại

   8. Điều kiện trong HAVING
      - Bạn có thể dùng các toán tử quen thuộc:
        + HAVING SUM(revenue) > 1000000;
        + HAVING COUNT(*) >= 5;
        + HAVING AVG(revenue) < 500000;
       
      - Có thể kết hợp nhiều điều kiện
        SELECT
           channel,
           COUNT(*) AS total_orders,
           SUM(revenue) AS total_revenue
        FROM orders
        GROUP BY channel
        HAVING COUNT(*) >= 2
           AND SUM(revenue) >= 1000000;
        
        + Ý nghĩa: Chỉ lấy các kênh vừa có ít nhất 2 đơn hàng, vừa có tổng doanh thu từ 1000000 trở lên
       
   9. Thứ tự chuẩn của câu SQL
       - Khi viết câu lệnh, thứ tự là:
         SELECT
         FROM
         WHERE
         GROUP BY
         HAVING
         ORDER BY;

       - Ví dụ đầy đủ:
         SELECT
            channel,
            COUNT(*) AS total_orders
            SUM(revenue) AS total_revenue
         FROM orders
         WHERE order_date >= '2026-10-01'
         GROUP BY channel
         HAVING SUM(revenue) >= 500000
         ORDER BY total_revenue DESC
         + Cách đọc:
            Lọc các đơn hàng từ ngày 01/10/2026, gom theo kênh, chỉ giữ các kênh có tổng doanh thu từ 500000 trở lên, rồi sắp xếp tổng doanh thu giảm dần

   10. Bảng ghi nhớ nhanh
       | Câu lệnh                        | Lọc cái gì?             | Thời điểm        |
       | ------------------------------- | ----------------------- | ---------------- |
       | `WHERE revenue > 400000`        | Từng dòng đơn hàng      | Trước `GROUP BY` |
       | `GROUP BY channel`              | Gom các dòng thành nhóm | Sau `WHERE`      |
       | `HAVING SUM(revenue) > 1000000` | Các nhóm đã tổng hợp    | Sau `GROUP BY`   |
       | `ORDER BY total_revenue DESC`   | Sắp xếp kết quả         | Cuối cùng        |

       - Câu ghi nhớ:
          WHERE lọc dòng, HAVING lọc nhóm


   11. Bài tập
       Dùng bảng orders hiện tại
       1. Bài 25: Tính tổng doanh thu theo từng kênh, chỉ hiển thị các kênh có tổng doanh thu lớn hơn 700000
           SELECT
             channel,
             SUM(revenue) AS total_revenue
           FROM orders
           GROUP BY channel
           HAVING SUM(revenue) > 700000;      

       3. Bài 26: Đếm số đơn hàng theo từng kênh, chỉ hiển thị các kênh có ít nhất 2 đơn hàng
           SELECT
              channel,
              COUNT(*) AS total_orders
           FROM orders
           GROUP BY channel
           HAVING COUNT(*) >= 2;

       5. Bài 27: Tính tổng số lượng sản phẩm theo từng sản phẩm, chỉ hiển thị sản phẩm có tổng số lượng từ 3 trở lên
          SELECT
             product_name,
             SUM(quantity) AS total_quantity
          FROM orders
          GROUP BY product_name
          HAVING SUM(quantity) >= 3
          

       7. Bài 28: Tính tổng doanh thu theo từng sản phẩm, sắp xếp từ cao xuống thấp và chỉ hiển thị sản phẩm có tổng doanh thu ít nhất 500000
          SELECT
             product_name,
             SUM(revenue) AS total_revenue
          FROM orders
          GROUP BY product_name
          HAVING SUM(revenue) >= 500000
          ORDER BY total_revenue DESC

       9. Bài 29:
          - Giải thích sự khác nhau giữa hai câu SQL:
            SELECT
               channel,
               SUM(revenue) AS total_revenue
            FROM orders
            WHERE revenue >= 400000
            GROUP BY channel;
             - Chỉ giữ lại những dòng đơn hàng có doanh thu từ 400000 trở lên. Sau đó gom các dòng lại theo kênh và tính tổng doanh thu theo từng kênh

          - Và
            SELECT
               channel,
               SUM(revenue) AS total_revenue
            FROM orders
            GROUP BY channel
            HAVING SUM(revenue) >= 400000
             - Gom toàn bộ đơn hàng theo từng kênh, tính tổng doanh thu của mỗi kênh, rồi chỉ hiển thị những kênh có tổng doanh thu từ 400000 trở lên
            
   6. Bài 30: Phát hiện lỗi trong câu SQL sau:
          SELECT
             channel,
             SUM(revenue) AS total_revenue
          FROM orders
          WHERE SUM(revenue) >= 1000000
          GROUP BY channel;
            - Không dùng WHERE với SUM(total_revenue)
                + Vì SUM(revenue) là kết quả sau khi nhóm dữ liệu, nên phải dùng HAVING
            - Viết lại
              SELECT
                 channel,
                 SUM(revenue) AS total_revenue
              FROM orders
              GROUP BY channel
              HAVING SUM(revenue) >= 1000000
               + Gom đơn hàng theo từng kênh, tính tổng doanh thu mỗi kênh, rồi chỉ hiển thị những kênh có tổng doanh thu từ 1000000 trở lên

VI. CASE WHEN
 1. CASE WHEN là gì?
  - Có thể hiểu đơn giản:
      Nếu điều kiện đúng thì trả về kết quả A, nếu không thì kiểm tra điều kiện tiếp theo
  - Cấu trúc cơ bản:
    CASE
       WHEN điều_kiện_1 THEN kết_quả_1
       WHEN điều_kiện_2 THEN kết_quả_2
       ELSE kết_quả_khác
    END

  - Ví dụ:
    CASE
      WHEN revenue >= 700000 THEN 'Đơn lớn'
      WHEN revenue >= 400000 THEN 'Đơn vừa'
      ELSE 'Đơn nhỏ'
    END

  - Câu lệnh này phân loại doanh thu thành ba nhóm:
    | Điều kiện           | Kết quả |
    | `revenue >= 700000` | Đơn lớn |
    | `revenue >= 400000` | Đơn vừa |
    | Còn lại             | Đơn nhỏ |

 2. Dùng CASE WHEN trong SELECT
    SELECT
       order_id
       product_name,
       revenue,
       CASE
          WHEN revenue >= 700000 THEN 'Đơn lớn'
          WHEN revenue >= 400000 THEN 'Đơn vừa'
          ELSE 'Đơn nhỏ'
       END AS order_segment
   FROM orders;

 -  Kết quả có thể như sau:
   | order_id  | product_name  | revenue | order_segment  |
   |      1001 | Áo thun       |  300000 | Đơn nhỏ        |
   |      1002 | Giày thể thao |  800000 | Đơn lớn        |
   |      1003 | Túi xách      |  450000 | Đơn vừa        |
   |      1004 | Áo thun       |  450000 | Đơn vừa        |
     + order_segment là tên của cột mới được tạo ra
  
 3. Ý nghĩa của ELSE
    - ELSE là kết quả mặc định nếu không có điều kiện WHEN nào đúng
    - Ví dụ:
      CASE
         WHEN revenue >= 700000 THEN 'Đơn lớn'
         WHEN revenue >= 400000 THEN 'Đơn vừa'
         ELSE 'Đơn nhỏ'
      END AS order_segment

    - Nếu doanh thu là 300000, không điều kiện nào ở trên đúng, nên kết quả là: đơn nhỏ
    - Nếu bỏ ELSE:
      CASE
         WHEN revenue >= 700000 THEN 'Đơn lớn'
         WHEN revenue >= 400000 THEN 'Đơn vừa'
      END AS order_segment
      + Những dòng không thỏa mãn điều kiện sẽ có kết quaer NULL
      + Thông thường, nên dùng ELSE để tránh giá trị trống không mong muốn
     
 4. Thứ tự của các điều kiện rất quan trọng
    - Hãy xem câu này:
      CASE
         WHEN revenue >= 400000 THEN 'Đơn vừa'
         WHEN revenue >= 700000 THEN 'Đơn lớn'
         ELSE 'Đơn nhỏ'
      END

    -  Câu này có lỗi logic
    -  Vì đơn hàng có doanh thu 800000 cũng thỏa mãn điều kiện đầu tiên
        revenue >= 400000
    - SQL sẽ dừng ngay ở điều kiện đầu tiên và gán là Đơn vừa. Nó không đi tiếp để kiểm tra revenue >= 700000
   
    - Cách đúng
      + Đặt điều kiện cụ thể hoặc mức cao hơn trước:
        CASE
           WHEN revenue >= 700000 THEN 'Đơn lớn'
           WHEN revenue >= 400000 THEN 'Đơn vừa'
           ELSE 'Đơn nhỏ'
        END

    - Câu ghi nhớ
      CASE WHEN kiểm tra từ trên xuống dưới và dừng ở điều kiện đúng đầu tiên

 5. CASE WHEN với số lượng
    SELECT
       order_id,
       product_name,
       quantity,
       CASE
          WHEN quantity >= 3 THEN 'Số lượng cao'
          WHEN quantity >= 2 THEN 'Số lượng vừa'
          ELSE 'Số lượng thấp'
       END AS quantity_segment
    FROM orders

    - Cách phân loại:
      + Từ 3 sản phẩm trở lên: Số lượng cao
      + Từ 2 đến dưới 3: Số lượng vừa
      + Dưới 2: Số lượng thấp
     
 6. CASE WHEN với kênh bán hàng
    - Bạn cũng có thể phân loại theo giá trị chữ:
      SELECT
         order_id,
         channel,
         CASE
            WHEN channel = 'Website' THEN 'Kênh sở hữu'
            WHEN channel = 'Shopee' THEN 'Sàn thương mại điện tử'
            ELSE 'Kênh khác'
         END AS channel_group
      FROM orders

    - Kết quả:
      | channel     | channel_group          |
      | Website     | Kênh sở hữu            |
      | Shopee      | Sàn thương mại điện tử |
      | TikTok Shop | Kênh khác              |

 7. CASE WHEN kết hợp với SUM
    - Bạn có thể dùng CASE WHEN bên trong SUM để tính tổng theo điều kiện
    - Tính doanh thu từ các đơn lớn
      SELECT
         SUM(
            CASE
               WHEN revenue >= 700000 THEN revenue
               ELSE 0
            END
         ) AS large_order_revenue
      FROM orders

   - Ý nghĩa:
     + Nếu doanh thu của dòng đó từ 700000 trở lên, lấy doanh thu
     + Nếu không, lấy không
     + Sau đó cộng tất cả lại
    
   - Tính số đơn lớn
     SELECT
        SUM(
           CASE
              WHEN revenue >= 700000 THEN 1
              ELSE 0
           END
        ) AS large_order_count
     FROM orders;

   - Cách hoạt động:
     + Đơn lớn: gán 1
     + Không phải đơn lớn: gán 0
     + Tổng các số 1 chính là số đơn lớn
    
 8. Phân loại rồi đếm số đơn theo nhóm
    - Bạn có thể đặt CASE WHEN trong GROUP BY:
      SELECT
         CASE
            WHEN revenue >= 700000 THEN 'Đơn lớn'
            WHEN revenue >= 400000 THEN 'Đơn vừa'
            ELSE 'Đơn nhỏ'
         END AS order_segment,
         COUNT(*) AS total_orders
      FROM orders
      GROUP BY
         CASE
            WHEN revenue >= 700000 THEN 'Đơn lớn'
            WHEN revenue >= 400000 THEN 'Đơn vừa'
            ELSE 'Đơn nhỏ'
         END;

   - Kết quả có thể là:
     | order_segment | total_orders   |
     | Đơn lớn        |             1 |
     | Đơn vừa        |             2 |
     | Đơn nhỏ        |             1 |

   - Một số hệ quản trị cho phép dùng bí danh trong GROUP BY, nhưng viết lại toàn bộ CASE là cách tương thích mở rộng hơn

 9. Cách dùng CASE WHEN với GROUP BY
     - Một cách dễ đọc hơn là tạo nhóm trước trong một truy vấn con
       SELECT
          order_segment,
          COUNT(*) AS total_orders,
          SUM(revenue) AS total_revenue
       FROM(
          SELECT
             revenue,
             CASE
                WHEN revenue >= 700000 THEN 'Đơn lớn'
                WHEN revenue >= 400000 THEN 'Đơn vừa'
                ELSE 'Đơn nhỏ'
             END AS order_segment
          FROM orders
       ) AS classified_orders
       GROUP BY order_segment

     - Ở đây:
         + Truy vấn bên trong phân loại từng đơn hàng
         + Truy vấn bên ngoài nhóm theo nhãn đã tạo
         + Tính số đơn và doanh thu theo từng nhóm

 10. CASE WHEN khác WHERE như thế nào?
     - WHERE loại bỏ dòng
       SELECT *
       FROM orders
       WHERE revenue >= 700000;
        -> Kết quả chỉ còn những đơn lớn. Cacs dòng khác biến mất khỏi kết quả

     - CASE WHWEN giữ lại dòng và thêm nhãn
       SELECT
          order_id,
          revenue,
          CASE
             WHEN revenue >= 700000 THEN 'Đơn lớn'
             ELSE 'Không phải đơn lớn'
          END AS order_type
       FROM orders;
        -> Tất cả các dòng vẫn còn, nhưng mỗi dòng được thêm một nhãn
     - Ghi nhớ:
          + WHERE dùng để lọc bỏ dữ liệu
          + CASE WHEN dùng để phân loại hoặc tạo cột mới
      
 11. CASE WHEN kết hợp với WHERE
     SELECT
        order_id,
        product_name,
        channel,
        revenue,
        CASE
           WHEN revenue >= 700000 THEN 'Đơn lớn'
           WHEN revenue >= 400000 THEN 'Đơn vừa'
           ELSE 'Đơn nhỏ'
        END AS order_segment
     FROM orders
     WHERE channel = 'Website'
     - Ý nghĩa
       1. Chỉ lấy các đơn hàng từ Website
       2. Phân loại các đơn Website thành đơn lớn, vừa hoặc nhỏ
      
 12. CASE WHEN kết hợp với HAVING
     - Ví dụ: phân loại đơn hàng, nhóm theo kênh và chỉ hiển thị kệnh có ít nhất 2 đơn:
       SELECT
          channel,
          COUNT(*) AS total_orders
       FROM orders
       GROUP BY channel
       HAVING COUNT(*) >= 2
     - Nếu muốn lọc theo điều kiện tổng hợp phức tạp hơn, vẫn dùng HAVING
     - Điều quan trọng là phân biệt:
       + Điều kiện trên từng dòng: WHERE
       + Điều kiện tạo nhãn: CASE WHEN
       + Điều kiện trên nhóm: HAVING
      
 13. Ví dụ nghiệp vụ: đánh giá KPI
     - Giả sử mục tiêu doanh thu của mỗi kênh là 1000000:
       SELECT
          channel,
          SUM(revenue) AS total_revenue,
          CASE
             WHEN SUM(revenue) >= 1000000 THEN 'Đạt KPI'
             ELSE 'Chưa đạt KPI'
          END AS kpi_status
       FROM orders
       GROUP BY channel;

     - Kết quả:
       | channel     | total_revenue  | kpi_status   |
       | Website     |         950000 | Chưa đạt KPI |
       | Shopee      |        1700000 | Đạt KPI      |
       | TikTok Shop |         450000 | Chưa đạt KPI |

     - Ở đây:
       CASE
          WHEN SUM(revenue) >= 1000000 THEN 'Đạt KPI'
          ELSE 'Chưa đạt KPI'
       END
       + Đang phân loại kết quả của từng nhóm, không phải doanh thu của từng dòng

 14. Một số lỗi thường gặp
     1. Lỗi 1: Quên END
        - Sai:
          CASE
             WHEN revenue >= 700000 THEN 'Đơn lớn'
             ELSE 'Đơn nhỏ'

        - Đúng:
          CASE
             WHEN revenue >= 700000 THEN 'Đơn lớn'
             ELSE 'Đơn nhỏ'
          END AS order_segment

     2. Dùng = thay vì WHEN
        - Sai:
          CASE revenue >= 700000 THEN 'Đơn lớn'
        - Đúng
          CASE
             WHEN revenue >= 700000 THEN 'Đơn lớn'
          END

     3. Lỗi 3: Đặt điều kiện rộng trước điều kiện hẹp
        - Sai:
          CASE
             WHEN revenue >= 400000 THEN 'Đơn vừa'
             WHEN revenue >= 700000 THEN 'Đơn lớn'
        - Đúng:
          CASE
             WHEN revenue >= 700000 THEN 'Đơn lớn'
             WHEN revenue >= 400000 THEN 'Đơn vừa'
             ELSE 'Đơn nhỏ'
          END

     4. Lỗi 4: Nhầm CASE WHEN với WHERE
        - CASE WHEN không tự động loại bỏ dòng
          CASE
             WHEN revenue >= 700000 THEN 'Đơn lớn'
             ELSE 'Đơn nhỏ'
          END
          -> Nó chỉ tạo nhãn cho từng dòng

 15. Bài tập
     Dùng bảng orders
     1. Bài 31: Tạo cột order_segment để phân loại
        - Đơn lớn nếu revenue >= 700000
        - Đơn vừa nếu revenue >= 400000
        - Đơn nhỏ nếu thấp hơn 400000
      Hiển thị:       
        - order_id
        - revenue
        - order_segment
       
         SELECT
            order_id,
            revenue,
            CASE
              WHEN revenue >= 700000 THEN 'Đơn lớn'
              WHEN revenue >= 400000 THEN 'Đơn vừa'
              ELSE 'Đơn nhỏ'
            END AS order_segment
        FROM orders
       
     3. Bài 32:
        Tạo cột quantity_segment để phân loại:
           - Số lượng cao nếu qunatity >= 3
           - Số lượng vừa nếu quantity = 2
           - Số lượng thấp nếu quantity < 2
       
               SELECT
                  order_id,
                  quantity,
                  CASE
                     WHEN quantity >= 3 THEN 'Số lượng cao'
                     WHEN quantity = 2 THEN 'Số lượng vừa'
                     ELSE 'Số lượng thấp'
                  END AS quantity_segment
                FROM orders
             
     4. Bài 33:
        Phân loại kênh khách hàng:
           - Kênh sở hữu nếu là Website
           - Sàn thương mại điện tử nếu là Shopee hoặc Tiktok Shop
           - Kênh khác trong các trường hợp còn lại
       Hiển thị:
           - channel
           - Cột phân loại mới
       
              SELECT
                 order_id,
                 channel
                 CASE
                   WHEN channel = 'Website' THEN 'Kênh sở hữu'
                   WHEN channel = 'Shopee'
                     OR channel = 'Tiktok Shop'
                   THEN 'Sàn thương mại điện tử'
                   ELSE 'Kênh khác'
                 END AS channel_segment
             FROM orders
       
     5. Bài 34:
        Tính số đơn hàng lớn:
          Đơn lớn là đơn có revenue >= 700000
             SELECT 
                SUM(
                  CASE revenue >= 700000 THEN 1
                  ELSE 0
                END
                ) AS order_large_quantity
             FROM orders;

     7. Bài 35: Tính tổng doanh thu của các đơn hàng lớn
          SELECT
            order_id,
            SUM(revenue) AS total_revenue
            CASE
               WHEN revenue >= 700000 THEN 'Đơn lớn'
               ELSE 'Đơn nhỏ'
            END AS total_revenue_large
          FROM orders;

     9. Bài 36:
        Giải thích sự khác nhau giữa hai câu lệnh:
           SELECT *
           FROM orders
           WHERE revenue >= 700000;
        và:
           SELECT
              order_id,
              revenue,
              CASE
                 WHEN revenue > 700000 THEN 'Đơn lớn'
                 ELSE 'Đơn không lớn'
              END AS order_type
           FROM orders;

          - Câu lệnh đầu tiên: Hiển thị các đơn hàng có doanh thu từ 700000 trở lên
          - Câu lệnh thứ 2: Phân loại các đơn hàng, nếu đơn hàng nào có doanh thu từ 700000 trở là 'Đơn lớn', còn lại là 'Đơn không lớn'
       

     10. Bài 37
        Phát hiện lỗi trong câu SQL
           SELECT
              order_id
              revenue,
              CASE
                 WHEN revenue >= 400000 THEN 'Đơn vừa'
                 WHEN revenue >= 700000 THEN 'Đơn lớn'
              AS order_segment
           FROM orders;
        Hãy chỉ ra ít nhất hai lỗi và viết lại câu đúng
          - Lỗi số 1: Điều kiện rộng trước điều kiện hẹp (đơn vừa trước đơn lớn)
          - Lỗi số 2: không có END kết thúc câu lệnh CASE
          - Viết lại đúng
                 SELECT
                    order_id
                    revenue,
                    CASE
                       WHEN revenue >= 700000 THEN 'Đơn lớn'
                       WHEN revenue >= 400000 THEN 'Đơn vừa'
                    END AS order_segment
                 FROM orders;
