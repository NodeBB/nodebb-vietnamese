Cloud 9 IDE
===========

Hướng dẫn cài đặt dưới đây dành cho IDE nền web `Cloud 9 <https://c9.io/>`_.

**Bước 1:** Tạo bản sao NodeBB vào workspace của bạn từ GitHub. Bạn có thể sử dụng lệnh sau từ terminal:

.. code:: bash
	
	git clone -b v0.5.x https://github.com/NodeBB/NodeBB.git nodebb

Lệnh nodebb sau git url sẽ tạo 1 file tên là nodebb vì vậy bạn phải CD vào trong file đó sau khi bạn tạo xong bản sao của NodeBB.

**Bước 2:** Cài đặt redis với Cloud9's package manager

.. code:: bash
	
	nada-nix install redis

**Bước 3:** Chạy redis server tại cổng 16379 - cổng 6379 đã được sử dụng bởi Cloud 9. "&" để dòng lệnh thực hiện nền. Bạn có thể hủy tiến trình bất cứ lúc nào sau này. $IP là biến hệ thống của Cloud 9 chứa địa chỉ IP instance của bạn.

.. code:: bash
	
	redis-server --port 16379 --bind $IP &

**Bước 4:** Xác định địa chỉ IP instance của bạn để NodeBB có thể chạy chính xác. Đây là 1 trong những yêu cầu của Cloud 9 và có vẻ như là cách duy nhất mới làm nó chạy. Bạn không thể sử dụng $IP trong file config.json (có nghĩa là bạn không thể nhập $IP trong node app --setup).

.. code:: bash
	
	echo $IP

**Bước 5:** Cài NodeBB và trình phụ thuộc:

.. code:: bash
	
	npm install

**Bước 6:** Chạy trình cài đặt nodebb:

.. code:: bash
	
	node app --setup

URL của phần cài đặt này nên là 'http://workspace_name-c9-username.c9.io', thay thế workspace_name bằng tên workspace của bạn và username với username của bạn. Chú ý rằng NodeBB vẫn đang sử dụng kết nối không bảo mật http để tải jQuery bạn sẽ thấy dễ sử dụng http:// hơn nhiều thay vì https:// cho url nền của bạn. Nếu không jQuery sẽ không tải và NodeBB sẽ không chạy.

Số cổng không thực sự quan trọng - Cloud9 sẽ bắt bạn sử dụng cổng 80. Hãy đặt nó là 80. Nếu nó là cổng khác, như 4567, cũng vẫn sẽ bình thường.

Use a port number to access NodeBB? Lại lần nữa, nó cũng không quá khác biệt. Hãy đặt là "no". Hoặc khác cũng vẫn được.

Host IP or address of your Redis instance: localhost (giá trị xuất ra của lệnh $IP cũng được chấp nhận)

IP or Hostname to bind to: Nhập giá trị mà $IP chứa ở Bước 4. Nó sẽ có thể giống như sau: 123.4.567.8

Host port of your Redis instance: 16379

Redis Password: Trừ khi bạn cài đặt nó thủ công, không thì Redis sẽ được cấu hình không có mật khẩu. Hãy để trống và nhấn Enter

Lần cài đặt đầu tiên yêu cầu cần có Admin name, email address và password được đặt.

Vậy là xong! Đừng sử dụng nút Run ở trên cùng của IDE, nó thường có lỗi đối với tôi. Bạn nên sử dụng command line thì tốt hơn. Chạy lệnh sau:

.. code:: bash
	
	node app

Sau đó truy cập http://workspace_name-c9-username.c9.io tại trình duyệt.

Khắc phục
---------------

Vấn đề thường gặp là dịch vụ cơ sở dữ liệu chưa được khởi động. Hãy chắc chắn bạn đã cài đặt Redis 1 cách chính xác và chạy: 

.. code:: bash
	
	redis-server --port 16379 --bind $IP