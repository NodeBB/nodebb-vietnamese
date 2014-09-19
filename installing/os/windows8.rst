Windows 8
==========

Phần mềm yêu cầu
---------------------

Đầu tiên, cài đặt các chương trình dưới đây:

* https://windows.github.com/
* http://nodejs.org/
* http://sourceforge.net/projects/redis/files/redis-2.6.10/
* http://imagemagick.org/script/binary-releases.php#windows/

Bạn có thể phải khởi động lại máy tính của mình.

Chạy NodeBB
---------------------

Khởi động Redis Server

.. note::

	The default location of Redis Server is

	**C:\\Program Files (x86)\\Redis\\StartRedisServer.cmd**

Mở Git Shell, và đánh dòng lệnh sau. Tạo bản sao NodeBB repo:

.. code:: bash

    git clone -b v0.5.x https://github.com/NodeBB/NodeBB.git

Truy cập đường dẫn: 

.. code:: bash

    cd NodeBB

Cài đặt trình phụ thuộc:

.. code:: bash

    npm install

Chạy trình tương tác cài đặt:

.. code:: bash

    node app.js

Bạn có thể để mọi tùy chọn là mặc định.

Và bạn đã xong! Sau khi cài đặt, chạy

.. code:: bash

    node app.js

Bạn có thể truy cập diễn đàn tại ``http://127.0.0.1:4567/``


Phát triển trên Windows
---------------------

Sẽ có đôi chút khó chịu khi phải tắt và khởi động lại NodeBB mỗi khi bạn thay đổi. Hãy cài đặt supervisor:

.. code:: bash

    npm install -g supervisor

Mở bash:

.. code:: bash

    bash

Và chạy NodeBB trong chế độ "watch":

.. code:: bash

    ./nodebb watch

Nó sẽ bật NodeBB trong chế độ nhà phát triển, và sẽ theo dõi các file được thay đổi và tự động khởi động lại diễn đàn.