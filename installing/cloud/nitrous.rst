Nitrous.IO
===========

Hướng dẫn cài đặt dưới đây dành cho `Nitrous.IO <http://nitrous.io>`.

**Bước 1:** Tạo ứng dụng mới với NodeJS :

https://www.nitrous.io/app#/boxes/new

**Bước 2:** Mở terminal / SSH vào ứng dụng / Mở IDE

**Bước 3:** Lấy file của NodeBB về, unzip, xóa master.zip và cd vào folder

.. code:: bash
	
	wget https://github.com/NodeBB/NodeBB/archive/v0.5.x.zip && unzip NodeBB-v0.5.x.zip && rm NodeBB-v0.5.x.zip && cd NodeBB-v0.5.x
	
**Bước 4:** NPM Install

.. code:: bash

  npm install
  
**Bước 5:** Cài đặt Redis

.. code:: bash

  parts install redis

**Bước 6:** Cài đặt NodeBB

.. code:: bash
	
	./nodebb setup 

Để mọi thứ là mặc định, nhưng bạn vẫn có thể tự thay đổi.

Tôi đề nghị nên dùng cổng : 8080

**Bước 14:** Và cuối cùng, khởi động NodeBB

.. code:: bash
	
	./nodebb start

Và sao đó mở "Preview URI" không có cổng nếu bạn đã đặt cổng là : 8080.

Chú ý
---------------------------------------
Bạn có thể mở rộng tài nguyên của ứng dụng : http://www.nitrous.io/app#/n2o/bonus.
