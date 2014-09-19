
Debian
======

Hướng dẫn trên Ubuntu hiện tại không hoàn toàn tương thích với Debian và có một vài nét đặc trưng và đặc biệt là cách cài đặt Node.js, và cách lấy được bản mới nhất của Redis.

Yêu cầu
^^^^^^^^^^^^^^^^^^^^^^^
NodeBB cần có các phần mềm sau được cài đặt:

* Node.js ít nhất là bản 0.10 hoặc cao hơn
* Redis, bản 2.6 hoặc cao hơn
* cURL, chỉ cần thực hiện lệnh ``sudo apt-get install curl`` để cài đặt

Cài đặt Node.js
^^^^^^^^^^^^^^^^^^^^^^^

Debian 7 và 6 hoặc cũ hơn mặc định không có gói cài đặt `nodejs`, nhưng có một vài giải pháp để cài đặt Node.js trên Debian của bạn.

Wheezy Backport :
------------------

Giải pháp này **CHỈ cho Debian 7**, đơn giản là chạy đoạn mã dưới đây **với quyền root** :

.. code:: bash

	$ echo "deb http://ftp.us.debian.org/debian wheezy-backports main" >> /etc/apt/sources.list
	$ apt-get update


Để cài đặt Node.js + NPM, chạy :

.. code:: bash

	$ apt-get install nodejs-legacy
	$ curl --insecure https://www.npmjs.org/install.sh | bash


Nó sẽ cài đặt một phiên bản Node.js lớn hơn 0.8 (vào 29 tháng 3 năm 2014 : 0.10.21)

Tập hợp từ nguồn :
------------------

Giải pháp này cho Debian 6 (Squeeze) và hơn, để cài đặt NodeJS, chạy đoạn mã sau với **quyền root** :

.. code:: bash

	$ sudo apt-get install python g++ make checkinstall
	$ src=$(mktemp -d) && cd $src
	$ wget -N http://nodejs.org/dist/node-latest.tar.gz
	$ tar xzvf node-latest.tar.gz && cd node-v*
	$ ./configure
	$ fakeroot checkinstall -y --install=no --pkgversion $(echo $(pwd) | sed -n -re's/.+node-v(.+)$/\1/p') make -j$(($(nproc)+1)) install
	$ sudo dpkg -i node_*


Lấy phiên bản mới nhất qua DotDeb
^^^^^^^^^^^^^^^^^^^^^^^

Dotdeb là một kho chứa các gói để biến các box Debian của bạn thành mạnh mẽ, ổn định và LAMP được cập nhật.

* Nginx,
* PHP 5.4 và 5.3 (Những trình mở rộng PHP hữu ích : APC, imagick, Pinba, xcache, Xdebug, XHpro..)
* MySQL 5.5,
* Percona toolkit,
* Redis,
* Zabbix,
* Passenger…

Dotdeb hỗ trợ :

* Debian 6.0 “Squeeze“ và 7 “Wheezy“
* cả 2 kiến trúc amd64 và i386

Debian 7 (Wheezy) :
------------------

Để có một kho DotDeb đầy đủ :

.. code:: bash

	$ sudo echo 'deb http://packages.dotdeb.org wheezy all' >> /etc/apt/sources.list
	$ sudo echo 'deb-src http://packages.dotdeb.org wheezy all' >> /etc/apt/sources.list


Sau đó, thêm khóa GPC sau :

.. code:: bash

	$ wget http://www.dotdeb.org/dotdeb.gpg
	$ sudo apt-key add dotdeb.gpg


Và cập nhật nguồn:

.. code:: bash

	$ sudo apt-get update


Debian 6 (Squeeze)
------------------

Để có một kho DotDeb đầy đủ :

.. code:: bash

	$ sudo echo 'deb http://packages.dotdeb.org squeeze all' >> /etc/apt/sources.list
	$ sudo echo 'deb-src http://packages.dotdeb.org squeeze all' >> /etc/apt/sources.list


Sau đó, thêm khóa GPC sau :

.. code:: bash

	$ wget http://www.dotdeb.org/dotdeb.gpg
	$ sudo apt-key add dotdeb.gpg


Và cập nhật nguồn:

.. code:: bash

	$ sudo apt-get update


Cài đặt NodeBB
^^^^^^^^^^^^^^^^^^^^^^^

Bây giờ, ta đã có NodeJS và Redis được cài đặt, chạy lệnh sau để cài đặt gói phần mềm nền:

.. code:: bash

	$ apt-get install redis-server imagemagick git


Tiếp theo tạo bản sao của kho sau :

.. code:: bash

	$ cd /path/to/nodebb/install/location
	$ git clone -b v0.5.x https://github.com/NodeBB/NodeBB.git nodebb

Chúng ta sẽ tiến hành cài đặt các trình phụ thuộc cho NodeBB qua NPM :

.. code:: bash

	$ cd /path/to/nodebb/install/location/nodebb (hoặc nếu bạn đang ở đường dẫn cài đặt run : cd nodebb)
	$ npm install

Cài đặt NodeBB bằng cách chạy ứng dụng với thẻ `--setup` :

.. code:: bash

	$ ./nodebb setup


1. `URL of this installation` là địa chỉ IP hoặc tên miền trỏ về IP đó.

    **Ví dụ:** ``http://0.0.0.0`` hoặc ``http://example.org``  

2. ``Port number of your NodeBB`` là cổng để có thể truy cập vào trang:  
    **Chú ý:** Nếu bạn không tạo proxy cho cổng của bạn với một giải pháp nào đó như Nginx thì nên sử dụng cổng 80.
3. Nếu bạn đã thực hiện các bước trên để cài đặt redis-server thì sử dụng giá trị cài đặt mặc định là redis.

Và sau cùng.. hãy bắt đầu chạy NodeBB

.. code:: bash

	$ ./nodebb start


**Chú ý:** Nếu NodeBB hoặc máy chủ của bạn gặp sự cố, NodeBB sẽ không khởi đông lại, đây là lý do tại sao bạn nên đọc qua các cách khác để khởi động NodeBB với các trình trợ giúp như ``supervisor`` và ``forever``, chỉ cần :doc:`đọc ở đây <../../running/index>` đơn giản như 1 cú nhấp chuột!

Phụ lục, thủ thuật và lời khuyên
^^^^^^^^^^^^^^^^^^^^^^^

Bạn nên bảo mật cài đặt NodeBB của bạn, `đọc thêm ở đây <https://github.com/NodeBB/NodeBB#securing-nodebb>`_.

Bạn nên sử dụng Nginx (hoặc tương tự) để tạo proxy cho NodeBB về cổng 80, :doc:`đọc thêm ở đây <../../configuring/proxies>`