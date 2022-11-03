## Cách chạy springboot server như 1 service trên Linux.

> Service là 1 tiến trình nhưng chạy trong nền (background)<br>
> Systemd là một công cụ quản lý những process chạy trong nền kia

## Công cụ quản lý đi kèm với systemd
- `systemctl` commandline tool để "ra lệnh" cho systemd
- `journalctl` tool để xem log(thứ được in ra console)
- Vài thứ khác, tham khảo thêm ở [wikipedia](https://en.wikipedia.org/wiki/Systemd)

### Systemctl cơ bản
```
systemctl list: Liệt kê các service
systemctl start/stop <service name>: khởi tạo, dừng service.
systemctl enable/disable <service name>: Thêm vào/Xóa danh sách khởi tạo ở mỗi lần reboot(chạy mỗi lần máy tính khởi động).
systemctl status <service name>: Trạng thái của service, running (chạy ok), loaded(đã load lên và biết về nó nhưng k chạy được), dead (k chạy)
```
### Journalctl
`journalctl -u <name>`: xem log của 1 service 

có thể thêm `-f` thành `journalctl -u <service name> -f` để xem log realtime.

### Tạo 1 service springboot để chạy.

1. Tạo project springboot.
2. Pakage thành file jar + các config vào 1 folder, chẳng hạn /app/app.jar
3. Tạo file springboot-hello.service
```
[Unit]
Description=Springboot server.

[Service]
Type=simple
WorkingDirectory=/app/
ExecStart=/usr/bin/java -jar /app/app.jar

[Install]
WantedBy=multi-user.target
```
4. Copy vào `/etc/systemd/system/` hoặc `/usr/lib/systemd/system/`
   `sudo cp springboot-hello.service /etc/systemd/system/`
5. Reload daemon 
  `sudo systemctl reload-daemon`
6. Start service
  `sudo systemctl start springboot-hello.service`

