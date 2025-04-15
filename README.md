# Bai-Tap-4-HQTCSDL  
## Tạo DataBase TKB  
![image](https://github.com/user-attachments/assets/2e85a024-3711-496d-a055-7c71d946c217)  
Trong đó có các bảng dữ liệu:  
- LichDay
- GiangVien
- MonHoc
- Lop
- Phong  
## Tables
![image](https://github.com/user-attachments/assets/21e622d0-c507-42bb-bf66-64a89334eda2)  
các bảng khác cũng được tạo tương tự, lưu ý các bảng tạo ra phải đạt chuẩn 3NF. Chuẩn 3NF (Third Normal Form) là một cấp độ chuẩn hóa cơ sở dữ liệu nhằm loại bỏ sự dư thừa dữ liệu và đảm bảo tính toàn vẹn.  
Sau khi tạo xong các bảng ta sẽ có sơ đồ như sau:  
![image](https://github.com/user-attachments/assets/957cba76-94f9-466f-8b6a-65a5626f8a78)  
## Demo nhập dữ liệu cho các bảng dữ liệu  
Lấy dữ liệu thời khóa biểu trong trang web http://tms.tnut.edu.vn  
![image](https://github.com/user-attachments/assets/e65b19d6-e5c2-4f72-8037-d2186500014d)  
Nhập những dữ liệu đã có vào các bảng trong sql  
Demo bảng LichDay  
![image](https://github.com/user-attachments/assets/a04c792e-4c96-448b-9c8a-5ccc95b0df2e)  
Demo bảng GV  
![image](https://github.com/user-attachments/assets/4ecc7574-b892-4cc2-a6f8-2393a01d53b8)  
Demo bảng MonHoc  
![image](https://github.com/user-attachments/assets/afef75a2-e99d-42f9-b7c0-d947b6e33231)  
Demo bảng Lop  
![image](https://github.com/user-attachments/assets/77433cc8-6e9a-4be6-b82e-3cba95ffffac)  
Demo bảng Phong  
![image](https://github.com/user-attachments/assets/358c0405-cdb8-4d88-b4b8-a2f98e448c17)  
## Tạo query truy vẫn thông tin  
![image](https://github.com/user-attachments/assets/690a72c5-3a0b-40e8-83d5-37ad5312e17d)  
```
USE TKB
GO 

DECLARE @datetime1 DATETIME = '2025-04-16 06:30:00';
DECLARE @datetime2  DATETIME = '2025-04-16 09:10:00';

SELECT DISTINCT
    GV.Ten_GV      AS N'Họ tên GV',
    MH.TenMonHoc      AS N'Môn dạy',
    L.TenLop             AS N'Lớp học',
    LD.MaPhong    AS N'Phòng học',
    LD.GioVao    AS N'tiết bắt đầu',
    LD.GioRa    AS N'tiết kết thúc'
FROM dbo.LichDay LD
JOIN dbo.GV GV  ON LD.Ma_GV = GV.Ma_GV
JOIN dbo.MonHoc MH  ON LD.MaMon = MH.MaMon
JOIN dbo.Lop L ON LD.MaLop = l.MaLop 
WHERE
    CAST(LD.Ngay AS DATETIME) + CAST(LD.GioRa AS DATETIME) > @datetime1
AND CAST(LD.Ngay AS DATETIME) + CAST(LD.GioVao AS DATETIME) < @datetime2;
```  
