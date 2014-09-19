Ubuntu
--------------------

Đầu tiên, chúng ta cài đặt các trình nền:

.. code:: bash

	$ sudo apt-get install git nodejs redis-server imagemagick npm


Nếu bạn muốn sử dụng MongoDB, LevelDB, hoặc một cơ sở dữ liệu khác thay cho Redis  xin đọc :doc:`Cấu hình cơ sở dữ liệu <../../configuring/databases>`.

**Nếu trình quản lý gói của bạn chỉ cài đặt phiên bản Node.js nhỏ hơn 0.8 (vd: Ubuntu 12.10, 13.04), dùng lệnh ``node --version`` để xác định phiên bản Node.js của bạn**


.. code:: bash

	$ sudo add-apt-repository ppa:chris-lea/node.js
	$ sudo apt-get update && sudo apt-get dist-upgrade

Nếu bạn muốn cài đặt Node.js v0.11, sử dụng url repo sau ``ppa:chris-lea/node.js-devel``.


Sau đó, tạo bản sao repo:


.. code:: bash

	$ git clone -b v0.5.x https://github.com/NodeBB/NodeBB.git nodebb


Cài đặt các trình phụ thuộc bởi NodeBB:

.. code:: bash

    $ cd nodebb
    $ npm install


Thực hiện cài đặt bằng cách chạy ứng dựng với thẻ ``setup``:


.. code:: bash

	$ ./nodebb setup


Mặc định cài đặt là cho máy chủ nội địa và chạy trên cổng mặc định, với redis lưu trữ trên cùng một máy/cổng. 

Cuối cùng, ta chạy diễn đàn.


.. code:: bash

	$ ./nodebb start


NodeBB cũng có thể khởi động với các trình trợ giúp, như ``supervisor`` và ``forever``. :doc:`Đọc thêm về các tùy chọn ở đây <../../running/index>`.