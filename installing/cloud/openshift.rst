Openshift Paas
===========

Hướng dẫn dưới đây dành cho `Openshift <http://openshift.com>` Paas.

**Bước 1:** Tạo ứng dụng mới :

.. code:: bash
	
	rhc app create nodebb nodejs-0.10

**Bước 2:** Thêm cartridge Redis

.. code:: bash
	
	rhc add-cartridge http://cartreflect-claytondev.rhcloud.com/reflect?github=smarterclayton/openshift-redis-cart -a nodebb

**Bước 3:** SSH đến ứng dụng của bạn

.. code:: bash
	
	rhc app ssh -a nodebb
	
**Bước 4:** Xác định ip của NodeJS và Redis để NodeBB có thể chạy chính xác. Đây là một yêu cầu của Openshift và là cách duy nhất để nó chạy. Bạn không thể sử dụng $IP trong config.json (Có nghĩa là bạn không thể nhập $IP trong lệnh node app –setup). Dòng đầu tiên : NodeJS và dòng thứ hai : Redis
Giá trị xuất ra của lệnh echo $REDIS_CLI sẽ như sau : -h ip_redis -p port_redis -a password

.. code:: bash

  echo $OPENSHIFT_NODEJS_IP && echo $REDIS_CLI
  
**Bước 5:** Thoát SSH

**Bước 6:** Thêm mã nguồn của NodeBB vào repository của ứng dụng

.. code:: bash
	
	cd nodebb && git remote add upstream -m master https://github.com/NodeBB/NodeBB.git

**Bước 7:** Lấy file về và push

.. code:: bash
	
	git pull -s recursive -X theirs upstream v0.5.x && git push
	
**Bước 8:** Ngừng chạy ứng dụng

.. code:: bash
	
	rhc app stop -a nodebb

**Bước 9:** SSH vào ứng dụng

.. code:: bash
	
	rhc app ssh -a nodebb

**Bước 10:** Sửa môi trường chạy của NodeJS trong terminal với SSH

.. code:: bash
	
	cd ~/nodejs/configuration && nano node.env
	
**Bước 11:** Thay server.js bằng app.js và thoát khỏi editor

.. code:: bash
	
	ctrl + x
	
**Bước 12:** Trong terminal khác, bắt đầu chạy ứng dụng

.. code:: bash
	
	rhc app start -a nodebb

**Bước 13:** Chạy mã cài đặt NodeBB trên terminal với SSH

.. code:: bash
	
	cd ~/app-root/repo && node app --setup

URL để cài đặt nên đặt là 'http://nodebb-username.rhcloud.com', thay username với username của bạn. 

Port number : 8080

IP or Hostname to bind to: Nhập giá trị xuất của $OPENSHIFT_NODEJS_IP trong Bước 4.

Host IP or address of your MongoDB instance: Nhập giá trị xuất của $REDIS_CLI trong Bước 4.

Host port of your MongoDB instance: Nhập giá trị xuất của $REDIS_CLI trong bước Bước 4.

Redis Password: Nhập giá trị xuất của $REDIS_CLI trong Bước 4.

**Bước 14:** Và cuối cùng, trong terminal khác, khởi động lại ứng dụng

.. code:: bash
	
	rhc app restart -a nodebb

Và sau đó truy cập http://nodebb-username.rhcloud.com trong trình duyệt.

Chú ý
---------------------------------------
Restart NodeBB trong trang Admin không hoạt động. Sử dụng :

.. code:: bash
	
	rhc app restart -a nodebb
