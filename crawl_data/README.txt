Đây là chương trình Crawl dữ liệu như Văn bản pháp luật, Công văn... từ trang web Thư viện pháp luật (https://thuvienphapluat.vn/). Sau khi Crawl dữ liệu xong, chương trình sẽ lưu dữ liệu vào database, chương trình này hiện hỗ trợ lưu vào một Folder trong máy, văn bản được Crawl về sẽ ở dạng .txt.

Tính năng mới: 
- Chương trình sẽ Crawl văn bản được ra mắt ngày đầu tiên, và sẽ Crawl cho tới văn bản mới nhất, ngoài ra chương trình kiểm tra được những link nào đã cào, những link nào chưa cào, tránh cào trùng.
- Chương trình đã được Dockerize.

How to use:

- Tạo một Folder đặt tên là Data trong ổ đĩa C: (C:\Data)
- Mở chương trình này trong Visual Studio 2022.
- Sau đó mở Terminal trong VS2022 và copy lệnh sau:

docker build -t my-app -f Test2/Dockerfile .

- Sau khi run lệnh build xong, tiếp tục Copy lệnh sau:

docker run -d -p 8080:8080 -p 8081:8081 --name my-dotnet-container -v C:/Data:/Data my-app

- Sau đó chương trình sẽ chạy trong Docker và File công văn sẽ được lưu vào Folder Data mới tạo trên máy.