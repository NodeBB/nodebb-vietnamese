SmartOS
========

Yêu cầu
----------------

NodeBB cần có những chương trình này được cài đặt:

* Node.js (phiên bản 0.10 hoặc hơn, hướng dẫn ở dưới).  
* Redis (phiên bản 2.6 hoặc hơn, hướng dẫn ở dưới) hoặc MongoDB (phiên bản 2.6 hoặc hơn).  
* nginx (phiên bản 1.3.13 hoặc hơn, **chỉ khi** bạn có ý định sử dụng nginx tạo proxy cho NodeBB).  

Truy cập máy chủ
----------------

1. Đăng nhập vào tài khoản Joyent của bạn: `Joyent.com <http://joyent.com>`_

2. Chọn: ``Create Instance``

3. Tạo image ``smartos nodejs`` mới nhất.  

    **Chú ý:** Những bước này đã được thử nghiệm với image: ``smartos nodejs 13.1.0`` ``smartos nodejs 13.2.3``

4. Đợi phiên bản của bạn hiện ``Running`` sau đó click chọn tên của nó.

5. Tìm ``Login`` và mật khẩu quản trị. Nếu khu vực ``Credentials`` bị thiếu, hãy tải lại trang.  

    **Ví dụ:** ``ssh root@0.0.0.0`` ``A#Ca{c1@3`` 

6. Truy cập SSH theo quyền admin không root: ``ssh admin@0.0.0.0``  

    **Chú ý:** Đối với những người dùng Windows chưa có cài đặt SSH thì đây là 1 tùy chọn: `Cygwin.com <http://cygwin.com>`_

Cài đặt
----------------

1. Cài đặt trình phụ thuộc cho NodeBB:

    .. code:: bash

        $ sudo pkgin update
        $ sudo pkgin install scmgit nodejs build-essential ImageMagick redis

    Nếu một trong số dòng trên thất bại thì chạy lênh dưới:

    .. code:: bash

        $ pkgin search *failed-name*
        $ sudo pkgin install *available-name*

2. **Nếu cần** cài đặt redis-server với mặc định là service (tự động khởi động và khởi động lại):  
    
   Nếu bạn muốn sử dụng MongoDB, LevelDB, hoặc 1 cơ sở dữ liệu khác ngoài Redis thì hãy đọc :doc:`Cấu hình cơ sở dữ liệu <../../configuring/databases>`.
    
    **Chú ý:** Những bước này để cài đặt nhanh 1 server redis nhưng không tối ưu để dùng chính thức. 
    
    **Chú ý:** Nếu bạn đã chạy ``redis-server`` rồi thì hãy thoát khỏi nó ngay.

    .. code:: bash

        $ svcadm enable redis
        $ svcs svc:/pkgsrc/redis:default
    **Chú ý:** Nếu STATE là maintenance thì:
    
    .. code:: bash

        $ scvadm clear redis  

    *-* Để tắt redis-server và ngăn nó khởi động lại:

    .. code:: bash

        $ scvadm disable redis

    *-* Để khởi động redis-server và cho nó luôn chạy:

    .. code:: bash

        $ scvadm enable redis

3. Chuyển đến nơi mà bạn muốn tạo folder cài đặt nodebb:

    .. code:: bash

        $ cd /parent/directory/of/nodebb/

4. Tạo bản sao NodeBB's repository (bạn có hể đổi nodebb ở cuối thành tên folder khác mà bạn muốn):

    .. code:: bash

        $ git clone -b v0.5.x https://github.com/NodeBB/NodeBB.git nodebb

5. Cài đặt trình phụ thuộc npm của NodeBB:

    .. code:: bash

        $ cd nodebb
        $ npm install

6. Chạy mã cài đặt NodeBB:  

    .. code:: bash

        $ ./nodebb setup

    a. ``URL used to access this NodeBB`` là địa chỉ ip bạn dùng để đăng nhập SSH hoặc tên miền trỏ đến IP này.  

        **Ví dụ:** ``http://0.0.0.0`` hoặc ``http://example.org``  

    b. ``Port number of your NodeBB`` là cổng cần để truy cập đến trang của bạn:  

        **Chú ý:** Nếu bạn không sử dụng nginx hoặc 1 server web nào khác để tạo proxy thì nên để cổng 80.  
    
    c. ``Please enter a NodeBB secret`` - Không gửi email và công khai mã này.
    
    d. ``IP or Hostname to bind to`` - Sử dụng giá trị mặc định trừ khi máy chủ bạn có yêu cầu khác.
    
    e. Nếu bạn sử dụng các bước cài đặt redis-server trên thì hãy sử dụng giá trị cài đặt mặc định cho redis.  

7. Khởi động tiến trình NodeBB thủ công:  
    **Chú ý:** Điều này không nên sử dụng cho bản chính thức nhưng thay vì sử dụng daemon thì nên sử dụng Forever hoặc Supervisor. :doc:`Đọc các tùy chỉnh ở đây <../../running/index>`.  

    .. code:: bash

        $ node app

8. Truy cập ứng dụng của bạn!  
    **Ví dụ:** Với cổng là 4567: ``http://0.0.0.0:4567`` or ``http://example.org:4567``

    **Chú ý:** Với cổng là 80 thì ``:80`` không cần phải nhập.  

**Chú ý:** Nếu hướng dẫn trên không rõ ràng với bạn hoặc nếu bạn có gặp rắc rối gì, hãy cho chúng tôi biết bằng cách `báo cáo lỗi tại đây <https://github.com/NodeBB/NodeBB/issues>`_.

Cập nhật NodeBB
----------------

**Chú ý:** Chi tiết về việc cập nhật NodeBB xin đọc :doc:`Cập nhật NodeBB <../../upgrading/index>`.