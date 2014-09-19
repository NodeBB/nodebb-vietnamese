
Arch Linux
--------------------

Đầu tiên, chúng ta cài đặt gói phần mềm cơ bản trước. Hãy thực hiện `pacman -Syu` trước tiên để chắc chán rằng bạn đã đồng bộ với kho và tất cả các gói được cập nhật.

.. code:: bash

	$ sudo pacman -S git nodejs redis imagemagick


Nếu bạn muốn sử dụng MongoDB, LevelDB, hoặc một nền tảng cơ sở dữ liệu khác ngoài Redis, hãy đọc tài liệu :doc:`Cấu hình cơ sở dữ liệu <../../configuring/databases>`.

Tiếp theo, tạo bản sao của kho sau:


.. code:: bash

	$ git clone -b v0.5.x https://github.com/NodeBB/NodeBB.git nodebb


Cài đặt các trình phụ thuộc được yêu cầu bởi NodeBB:

.. code:: bash

    $ cd nodebb
    $ npm install


Bắt đầu đoạn mã cài đặt bằng cách chạy ứng dụng với thẻ ``setup``:


.. code:: bash

	$ ./nodebb setup


Mặc định cài đặt là cho máy chủ nội địa và chạy trên cổng mặc định, với redis lưu trữ trên cùng một máy/cổng. 

Cuối cùng, ta chạy diễn đàn.


.. code:: bash

	$ ./nodebb start


NodeBB cũng có thể khởi động với các trình trợ giúp, như ``supervisor`` và ``forever``. :doc:`Đọc thêm về các tùy chọn ở đây <../../running/index>`.