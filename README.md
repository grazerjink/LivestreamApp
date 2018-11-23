# LivestreamApp
Hướng dẫn sử dụng ứng dụng livestream dạy học trên MacOS.

Cài đặt server NGINX với RTMP module
------

Mở terminal và gõ 2 lệnh sau:\

`brew tap denji/nginx`\
`brew install nginx full --with-rtmp-module --with-debug`

Đường dẫn thư mục nginx sẽ được tạo ra ở đường dẫn:\

`/usr/local/etc/nginx/`

Chúng ta vào thư mục và mở file **nginx.conf**, xóa hết những mã lệnh mặc định. Sau đó copy đoạn mã sau paste vào và thay đường dẫn **[your_root_directory_path]** trỏ vào thư mục mong muốn của bạn:

```ruby
worker_processes  auto;

events {
    worker_connections  1024;
}

# Config rtmp protocol
rtmp {
    server {
        listen 1935;
        chunk_size 4096;

        application live {
            live on;
            allow play all;

            # Turn on recorder
            record all;
            record_path [your_root_directory_path]/recordings/;
            record_unique on;

            # Turn on HLS
            hls on;
            hls_nested on;
            hls_fragment_naming system;
            hls_path [your_root_directory_path]/live/;
            hls_fragment 3;
            hls_playlist_length 60;
            
          #on_publish http://localhost:3000/publish;
          #on_publish_done http://localhost:3000/done-streaming;
        }
    }
}

# Config http protocol
http {
    default_type application/octet-stream;
    sendfile off;
    tcp_nopush on;
    keepalive_timeout 65;

    server {
        listen 8080;
        server_name localhost;
        root [your_root_directory_path];

        location /live {

            # Disable cache
            add_header Cache-Control no-cache;
            
	    # CORS setup
            add_header 'Access-Control-Allow-Origin' '*' always;
            add_header 'Access-Control-Expose-Headers' 'Content-Length';
            	
	    # Allow CORS preflight requests
            if ($request_method = 'OPTIONS') {
                add_header 'Access-Control-Allow-Origin' '*';
                add_header 'Access-Control-Max-Age' 1728000;
                add_header 'Content-Type' 'text/plain charset=UTF-8';
                add_header 'Content-Length' 0;
                return 204;
            }

            types {
                application/vnd.apple.mpegurl m3u8;
                video/mp2t ts;
            }
        }
    }
}
```
Quay lại terminal và khởi chạy server bằng lệnh sau:
* Khởi chạy server: `nginx`
* Làm mới server: `nginx -s reload`
* Dừng server: `nginx -s stop`

Cài đặt môi trường MQTT với thư viện emqttd.io
------

[Tải thư viện emqtt cho MacOS tại đây](http://emqtt.io/downloads)

Sau khi tải thành công, tiến hành giải nén ra ta sẽ có được thư mục có tên là emqttd. Di chuyển vào trong thư mục gõ những lệnh sau:

* Khởi chạy dịch vụ: `./bin/emqttd start`
* Tắt dịch vụ: `./bin/emqttd stop`

Cài đặt PostgreSQL
------



4. Cài đặt npm và yarn (mới nhất)
5. Cài đặt ruby-gems (mới nhất)
6. Cài đặt ruby(2.3.1) và rails framework (5.0)
7. Cấu hình và khởi chạy ứng dụng
- Chạy lệnh bundle: để cài đặt tất cả các gem đã yêu cầu.
- Chạy lệnh db:migrate: để map db schema mới nhất.
- Chạy lệnh yarn install: để cài đặt tất cả các pkg npm.
- Chạy lệnh rails s: khởi chạy ứng dụng.
