# Hướng dẫn tạo máy ảo sử dụng dải mạng VLAN ở MDT

## Hướng dẫn vpn tới hệ thống MDT

- Tham khảo bài viết sau để biết cách connect tới hệ thống vpn của MDT

[Hướng dẫn kết nối vpn tới hệ thống của MDT](https://github.com/thaonguyenvan/meditech-thuctap/blob/master/ThaoNV/ghichep-pfsense/docs/connect-vpn.md)

## Với những máy ảo tạo bằng web-virt

- Khai báo dải vlan theo bảng phân hoạch ip và tùy chọn `virtio`

<img src="https://i.imgur.com/C2DUp7d.png">

- Sau khi tạo máy ảo, nếu để dhcp, máy ảo sẽ tự lấy ip theo dải vlan tương ứng, tiến hành set ip tĩnh theo dải được cấp

## Với những máy ảo tạo bằng virt-manager

- Khai báo source device là dải vlan theo bảng phân hoạch ip và device model là `virtio` hoặc `pcnet`.
Lưu ý: Không chọn `rtl8139`

<img src="https://i.imgur.com/JldlR0f.png">

- Sau khi tạo máy ảo, nếu để dhcp, máy ảo sẽ tự lấy ip theo dải vlan tương ứng, tiến hành set ip tĩnh theo dải được cấp


**Lưu ý:**

- Đối với những máy ảo cũ (tạo với dải bridge 100), để có thể truy cập tới các dải vlan, cần thêm route trên các máy này

  - Đối với máy ảo có HDH là CentOS:

  `ip route add <dải-vlan> via 192.168.100.29 dev <tên-card-mạng>`

  - Đối với máy ảo có HDH là Ubuntu:

  `route add -net <dải-vlan> netmask 255.255.255.0 gw 192.168.100.29 dev <tên-card-mạng>`

Ví dụ:

`ip route add 192.168.30.0/24 via 192.168.100.29 dev ens3`
