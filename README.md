# QL_Ngan_Hang_Thuong_Mai
--Tạo Database
create database QL_Ngan_Hang_Thuong_Mai
go
----------------------------------------------------------
/*tạo các table */
use QL_Ngan_Hang_Thuong_Mai
go
-- Tạo table CHINHANH
create table CHINHANH
( 
  MaCN varchar(10) primary key,
  TenCN nvarchar(100) not null,
  Taisan bigint,
  Diachi nvarchar(200)
)
go

-- Tạo table KHACHHANG
create table KHACHHANG
(
 MaKH varchar(10) primary key,
 TenKH nvarchar(50) not null,
 SDT nvarchar(20),
 Diachi nvarchar(200)
)
go

-- Tạo bảng CHUNGCHI
create table CHUNGCHI
(
  SoSR nvarchar(20) primary key,
  TenChungChi nvarchar(50) not null,
  NgayPH datetime,
  MaKH varchar(10),
  Laisuat float,
  Thoihan int,
  MaCN  varchar(10),
)
go

-- Tạo bảng GIAODICH_vay
create table GIAODICH_vay
(
 MaGD varchar(10) primary key,
 MaVay varchar(10),
 NgayGD datetime,
 SotienGD BIGint,
 MaKH varchar(10),
)
go

-- Tạo bảng GIAODICH_gui
create table GIAODICH_gui
(
 MaGD varchar(10) primary key,
 MaGui varchar(10),
 NgayGD datetime,
 SotienGD BIGint,
 MaKH varchar(10),
)
go
-- Tạo table CN_&_DN_covon
create table CN_VS_DN_covon
( 
 MaKH varchar(10) primary key,
 TenKH nvarchar(100) not null,
 TgGiaoDich datetime,
 MaGD varchar(10) not null,
)
go

-- tạo bảng KHOANVAY
create table KHOANVAY
(
 MaKvay varchar(10) primary key,
 LoaiVay nvarchar(50) not null,
 Laisuat float,
 
)
go
-- tạo bảng KHOANGUI
create table KHOANGUI
(
 MaKgui varchar(10) primary key,
 LoaiGui nvarchar(50) not null,
 Laisuat float,
 
)
go

-- tạo bảng TAIKHOAN
create table TAIKHOAN
(
  MaTK varchar(20) primary key,
  NgayMo datetime,
  SoDuTK int,
  MaKH varchar(10) not null,
  MaCN varchar(10) not  null,
)
go

-- tạo bảng THETD
create table THETD
(
  MatheTD varchar(20) primary key,
  Thoihan int,
  MaCVV varchar(20),
  MaTK varchar(20) not null,
)
go

-- Tạo bảng THEGN
create table THEGN
(
  MatheGN varchar(20) primary key,
  Thoihan int,
  MaCVV varchar(20),
  MaTK varchar(20) not null,
  Loaithe nvarchar(20),
)
go

-- tạo bảng HOIPHIEU
create table HOIPHIEU
(
  MaHP varchar(20) primary key,
  TenHP nvarchar(50) not null,
  TenCTphathanh nvarchar(50) not null,
  NgayPH datetime,
  NgayDH datetime,
  MaCT varchar(10) not null,
  MaCN varchar(10) not null,
)
go

-- tạo bảng CTY
create table CTY
(
  MaCT varchar(10) primary key,
  TenCT nvarchar(100) not null,
  Diachi nvarchar(200)
)
go

-- tạo bảng DICHVUTHANHTOAN
create table DICHVUTHANHTOAN
(
 MaDV varchar(10) primary key,
 TenDV nvarchar(100) not null,
 NgayPS_Dichvu datetime,
)
go

-- tạo bảng DVTHANHTOANQUATK
create table DV_THANHTOANQUATK
(
 MaLuotDV nvarchar(20) primary key,
 MaDV varchar(10) not null,
 MaKH varchar(10) not null,
 MaCN varchar(10) not null,
)
go

---------------------------------------------------------------------------

/* tạo khóa ngoại */
use QL_Ngan_Hang_Thuong_Mai
go
-- Tạo khóa ngoại FK_CHINHANH_VS_DV_THANHTOANQUATK--
alter table DV_THANHTOANQUATK
add constraint FK_CHINHANH_VS_DV_THANHTOANQUATK
foreign key (MaCN)
references CHINHANH(MaCN)
go

--  Tạo khóa ngoại FK_CHINHANH_VS_CHUNGCHI--
alter table CHUNGCHI
add constraint FK_CHINHANH_VS_CHUNGCHI
foreign key (MaCN)
references CHINHANH(MaCN)
go



--  Tạo khóa ngoại FK_CHINHANH_VS_TAIKHOAN
alter table TAIKHOAN
add constraint FK_CHINHANH_VS_TAIKHOAN
foreign key (MaCN)
references CHINHANH(MaCN)
go

--  Tạo khóa ngoại FK_CHINHANH_VS_HOIPHIEU --
alter table HOIPHIEU
add constraint FK_CHINHANH_VS_HOIPHIEU
foreign key (MaCN)
references CHINHANH(MaCN)
go


--  Tạo khóa ngoại FK_KHACHHANG_VS_TAIKHOAN --
alter table TAIKHOAN
add constraint FK_KHACHHANG_VS_TAIKHOAN
foreign key (MaKH)
references KHACHHANG(MaKH)
go

--  Tạo khóa ngoại FK_KHACHHANG_VS_DV_THANHTOANQUATK --
alter table DV_THANHTOANQUATK
add constraint FK_KHACHHANG_VS_DV_THANHTOANQUATK
foreign key (MaKH)
references KHACHHANG(MaKH)
go

-- Tạo khóa ngoại FK_GIAODICH_vay_VS_KHOANVAY++
alter table giaodich_vay
add constraint FK_GIAODICH_vay_VS_KHOANVAY
foreign key (mavay)
references khoanvay(makvay)
go

-- Tạo khóa ngoại FK_GIAODICH_vay_VS_khachhang +++++++
alter table giaodich_vay
add constraint FK_GIAODICH_vay_VS_KHachhang
foreign key (makh)
references khachhang(makh)
go

-- Tạo khóa ngoại FK_GIAODICH_gui_VS_KHOANGUI++
alter table giaodich_gui
add constraint FK_GIAODICH_gui_VS_khoangui
foreign key (magui)
references khoangui(makgui)
go

-- Tạo khóa ngoại FK_GIAODICH_gui_VS_khachhang ++++++
alter table giaodich_gui
add constraint FK_GIAODICH_gui_VS_khachhang
foreign key (makh)
references khachhang(makh)
go

-- Tạo khóa ngoại FK_CN_VS_DN_covon_VS_CHUNGCHI
alter table CHUNGCHI
add constraint  FK_CN_VS_DN_covon_VS_CHUNGCHI
foreign key (MaKH)
references CN_VS_DN_covon(MaKH)
go

--  Tạo khóa ngoại FK_TAIKHOAN_VS_THETD
alter table THETD
add constraint FK_TAIKHOAN_VS_THETD
foreign key (MaTK)
references TAIKHOAN(MaTK)
go

--  Tạo khóa ngoại FK_TAIKHOAN_VS_THEGN --
alter table THEGN
add constraint FK_TAIKHOAN_VS_THEGN
foreign key (MaTK)
references TAIKHOAN(MaTK)
go

--  Tạo khóa ngoại FK_CTY_VS_HOIPHIEU
alter table HOIPHIEU
add constraint FK_CTY_VS_HOIPHIEU
foreign key (MaCT)
references CTY(MaCT)
go

--  Tạo khóa ngoại FK_DICHVUTHANHTOAN_VS_DV_THANHTOANQUATK
alter table DV_THANHTOANQUATK
add constraint FK_DICHVUTHANHTOAN_VS_DV_THANHTOANQUATK
foreign key (MaDV)
references DICHVUTHANHTOAN(MaDV)
go




--------------------------------------------------------------------
--------------------------------------------------------------------

-- nhập data

-- bảng chinhanh
insert CHINHANH(MaCN,TenCN,Taisan,Diachi)
values ('MB291HD',N'Chi nhánh Hà Đông',7000000000000 ,N'Q.Hà Đông, Hà Nội')
insert CHINHANH(MaCN,TenCN,Taisan,Diachi)
values ('MB296BT',N'Chi nhánh Minh Khai',7500000000000,N'Q.Hai Bà Trưng, Hà Nội')
insert CHINHANH(MaCN,TenCN,Taisan,Diachi)
values ('MB298CG',N'Chi nhánh Cầu Giấy',6800000000000 ,N'Q. Cầu Giấy, Hà Nội')
insert CHINHANH(MaCN,TenCN,Taisan,Diachi)
values ('MB170TB',N'Chi nhánh Thái Bình',7200000000000,N'TP Thái Bình, Thái Bình')
insert CHINHANH(MaCN,TenCN,Taisan,Diachi)
values ('MB412SG',N'Chi nhánh Thủ Đức',8000000000000,N'TP Thủ Đức, TP Hồ Chí MinH')


-- BẢNG KHACHHANG
INSERT KHACHHANG(MaKH,TenKH,SDT,Diachi)
VALUES ('291M03',N'Lê Việt Anh',N'0985634739',N'Q.Hà Đông, Hà Nội')
INSERT KHACHHANG(MaKH,TenKH,SDT,Diachi)
VALUES ('291F06',N'Nguyễn Thị Hồng',N'0896345710',N'Q. Hà Đông, Hà Nội')
INSERT KHACHHANG(MaKH,TenKH,SDT,Diachi)
VALUES ('298M26',N'Đỗ Hoàng Minh',N'0974631420',N'Q.Cầu Giấy, Hà Nội')
INSERT KHACHHANG(MaKH,TenKH,SDT,Diachi)
VALUES ('170F36',N'Vũ Thị Hoàng Hạnh',N'0963477103',N'H.Đông Hưng, Thái Bình')
INSERT KHACHHANG(MaKH,TenKH,SDT,Diachi)
VALUES ('170M82',N'Vũ Văn Khỏe',N'0896713640',N'TP.Thái Bình, Thái Bình')


-- BẢNG CHUNGCHI
INSERT CHUNGCHI(SoSR,TenChungChi,NgayPH,Laisuat,Thoihan,MaCN,MaKH)
VALUES ('1268443',N'Chứng chỉ tiền gửi ghi danh','06/18/2022',8.4,18,'MB291HD','291DN003')
INSERT CHUNGCHI(SoSR,TenChungChi,NgayPH,Laisuat,Thoihan,MaCN,MaKH)
VALUES ('2672364',N'Chứng chỉ tiền gửi ghi danh','08/06/2022',7.5,6,'MB298CG','298CN026')
INSERT CHUNGCHI(SoSR,TenChungChi,NgayPH,Laisuat,Thoihan,MaCN,MaKH)
VALUES ('3684026',N'Chứng chỉ tiền gửi vô danh','08/14/2022',8.2,15,'MB170TB','170CN128')
INSERT CHUNGCHI(SoSR,TenChungChi,NgayPH,Laisuat,Thoihan,MaCN,MaKH)
VALUES ('3459145',N'Chứng chỉ tiền gửi ghi danh','08/14/2022',8.0,12,'MB170TB','170CN230')
INSERT CHUNGCHI(SoSR,TenChungChi,NgayPH,Laisuat,Thoihan,MaCN,MaKH)
VALUES ('4526317',N'Chứng chỉ tiền gửi vô danh','08/26/2022',7.8,9,'MB412SG','412DN320')



-- bảng cn_vs_dc_covon
insert CN_VS_DN_covon(MaKH,TenKH,TgGiaoDich,MaGD)
values ('291DN003',N'Doanh nghiệp trách nhiệm hữu hạn Lâm Quyết','06/18/2022','291180601')
insert CN_VS_DN_covon(MaKH,TenKH,TgGiaoDich,MaGD)
values ('298CN026',N'Phạm Văn Quyết','06-08-2022','298060803')
insert CN_VS_DN_covon(MaKH,TenKH,TgGiaoDich,MaGD)
values ('412DN320',N'Công ty Cổ phần sữa Mộc Châu','08/26/2022','412260896')
insert CN_VS_DN_covon(MaKH,TenKH,TgGiaoDich,MaGD)
values ('170CN128',N'Vũ Chiến Thắng','08/14/2022','0549971557')
insert CN_VS_DN_covon(MaKH,TenKH,TgGiaoDich,MaGD)
values ('170CN230',N'Phạm Thanh Tâm','08/14/2022','3478629762')



-- BẢNG GIAODICH_gui +++++++++++++++++++++++++++++++++++++++++++++++++
INSERT GIAODICH_gui(MaGD,NgayGD,MaGui,makh,SotienGD)
VALUES ('170TG001','08/14/2022','170TG001','170F36',7000000)
INSERT GIAODICH_gui(MaGD,NgayGD,MaGui,makh,SotienGD)
VALUES ('298VT012','08/16/2022','291TG063','291F06',10000000)
INSERT GIAODICH_gui(MaGD,NgayGD,MaGui,makh,SotienGD)
VALUES ('170VT036','08/16/2022','291TG063','291M03',20000000)



-- BẢNG GIAODICH_VAY +++++++++++++++++++++++++++++++++++++++++++++++++
INSERT GIAODICH_vay(MaGD,NgayGD,MaVay,makh,SotienGD)
VALUES ('170TG001','08/14/2022','298VT012','298M26',7000000)
INSERT GIAODICH_VAY(MaGD,NgayGD,MaVay,makh,SotienGD)
VALUES ('298VT012','08/16/2022','170VT036','170F36',100000000)
INSERT GIAODICH_VAY(MaGD,NgayGD,MaVay,makh,SotienGD)
VALUES ('170VT036','08/16/2022','298VT012','291F06',200000000)


-- BẢNG KHOANVAY
INSERT KHOANVAY(Makvay,LoaiVay,Laisuat)
VALUES ('298VT012',N'Vay tín chấp',14.5)
INSERT KHOANVAY(MaKvay,LoaiVay,Laisuat)
VALUES ('170VT036',N'Vay thế chấp',10.8)
INSERT KHOANVAY(Makvay,LoaiVay,Laisuat)
VALUES ('291TG095',N'Vay thế chấp',10.8)



-- BẢNG KHOANGUI
INSERT KHOANGUI(MaKgui,LoaiGui,Laisuat)
VALUES ('170TG001',N'Tiết kiệm không kỳ hạn',5.5)
INSERT KHOANGUI(MaKgui,LoaiGui,Laisuat)
VALUES ('291TG063',N'Tiết kiệm có kỳ hạn',6.0)


--BẢNG TAIKHOAN
INSERT TAIKHOAN(MaTK,NgayMo,SoDuTK,MaKH,MaCN)
VALUES ('291036716','05/14/2019',19000000,'291M03','MB291HD')
INSERT TAIKHOAN(MaTK,NgayMo,SoDuTK,MaKH,MaCN)
VALUES ('291036712','04/26/2020',27000000,'291F06','MB291HD')
INSERT TAIKHOAN(MaTK,NgayMo,SoDuTK,MaKH,MaCN)
VALUES ('298364135','07/14/2020',50000000,'298M26','MB298CG')
INSERT TAIKHOAN(MaTK,NgayMo,SoDuTK,MaKH,MaCN)
VALUES ('170368426','08/16/2020',67000000,'170F36','MB170TB')


-- BẢNG THETD
INSERT THETD(MatheTD,Thoihan,MaCVV,MaTK)
VALUES ('29101635',5,'096','291036716')
INSERT THETD(MatheTD,Thoihan,MaCVV,MaTK)
VALUES ('291016975',5,'082','291036712')
INSERT THETD(MatheTD,Thoihan,MaCVV,MaTK)
VALUES ('298014753',3,'365','298364135')
INSERT THETD(MatheTD,Thoihan,MaCVV,MaTK)
VALUES ('170013647',5,'475','170368426')


-- BẢNG THEGN
INSERT THEGN(MatheGN,Thoihan,MaCVV,MaTK,Loaithe)
VALUES ('291023647',10,'951','291036716',N'Nội địa')
INSERT THEGN(MatheGN,Thoihan,MaCVV,MaTK,Loaithe)
VALUES ('291023674',10,'614','291036712',N'Quốc tế')
INSERT THEGN(MatheGN,Thoihan,MaCVV,MaTK,Loaithe)
VALUES ('298022443',5,'024','298364135',N'Quốc tế')
INSERT THEGN(MatheGN,Thoihan,MaCVV,MaTK,Loaithe)
VALUES ('170023679',5,'366','170368426',N'Nội địa')


--BẢNG CTY
INSERT CTY(MaCT,TenCT,Diachi)
VALUES ('40CP003',N'Công ty cổ phần ô tô Trường Hải',N'TP. Thủ Đức, TP. HCM')
INSERT CTY(MaCT,TenCT,Diachi)
VALUES ('29TN036',N'Tập đoàn đá quý Doji',N'Q. Ba Đình, Hà Nội')
INSERT CTY(MaCT,TenCT,Diachi)
VALUES ('29CP047',N'Tập đoàn Hòa Phát',N'Q.Hai Bà Trưng. Hà Nội')
INSERT CTY(MaCT,TenCT,Diachi)
VALUES ('29TN056',N'Tập đoàn Viễn Thông Quân đội Việt Nam',N'Q.Từ Liêm, Hà Nội')


-- BẢNG HOIPHIEU
INSERT HOIPHIEU(MaHP,TenHP,TenCTphathanh,NgayPH,NgayDH,MaCT,MaCN)
VALUES ('003NH035',N'HP Ngân hàng',N'Công ty cổ phần ô tô Trường Hải','06/19/2022','09/19/2022','40CP003','MB291HD')
INSERT HOIPHIEU(MaHP,TenHP,TenCTphathanh,NgayPH,NgayDH,MaCT,MaCN)
VALUES ('036NH036',N'HP Ngân hàng',N'Tập đoàn đá quý Doji','06/20/2022','09/20/2022','29TN036','MB298CG')
INSERT HOIPHIEU(MaHP,TenHP,TenCTphathanh,NgayPH,NgayDH,MaCT,MaCN)
VALUES ('047NH039',N'HP Ngân hàng',N'Tập đoàn Hòa Phát','09/26/2022','12/26/2022','29CP047','MB296BT')
INSERT HOIPHIEU(MaHP,TenHP,TenCTphathanh,NgayPH,NgayDH,MaCT,MaCN)
VALUES ('056NH041',N'HP Ngân hàng',N'Tập đoàn Viễn Thông Quân đội Việt Nam','09/30/2022','12/30/2022','29TN056','MB170TB')


--BẢNG DỊCH VỤ THANH TOÁN
INSERT DICHVUTHANHTOAN(MaDV,TenDV,NgayPS_Dichvu)
VALUES('CT028',N'Chuyển tiền','10/22/2022')
INSERT DICHVUTHANHTOAN(MaDV,TenDV,NgayPS_Dichvu)
VALUES('CT029',N'Thanh toán tiền điện','10/23/2022')
INSERT DICHVUTHANHTOAN(MaDV,TenDV,NgayPS_Dichvu)
VALUES('TT036',N'Thanh toán tiền nước','10/27/2022')


-- BẢNG  DỊCH VỤ THANH TOÁN QUA TÀI KHOẢN
INSERT DV_THANHTOANQUATK(MaLuotDV,MaDV,MaKH,MaCN)
VALUES ('291CT028','CT028','291M03','MB291HD')
INSERT DV_THANHTOANQUATK(MaLuotDV,MaDV,MaKH,MaCN)
VALUES ('296CT029','CT029','291F06','MB291HD')
INSERT DV_THANHTOANQUATK(MaLuotDV,MaDV,MaKH,MaCN)
VALUES ('298TT036','TT036','298M26','MB298CG')




-- -------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------




-- câu 1 Khách hàng thực hiện nhiều giao dịch nhất trong 3 tháng gần đây?
with dem_so_gd_vay(makh,soluongvay)
as (select makh,count(MaGD) from GIAODICH_vay where DATEDIFF(MONTH,NgayGD,CURRENT_TIMESTAMP) <= 3 group by Makh), 
dem_so_gd_gui (makh,soluonggui)
as (select makh ,count(MaGD) from GIAODICH_gui where DATEDIFF(MONTH,NgayGD,CURRENT_TIMESTAMP) <= 3 group by MaKH ) 
select top(1) with ties TenKH
from KHACHHANG,dem_so_gd_vay, dem_so_gd_gui 
where   KHACHHANG.MaKH =dem_so_gd_gui.makh and KHACHHANG.MaKH =dem_so_gd_vay.makh 
order by (soluonggui+ soluongvay) desc



-- câu 2 Tìm top 3 loại dịch vụ thanh toán được sử dụng nhiều nhất
WITH DEM_SO_GD(MADV,SOLUONGDUNG)
AS (SELECT MADV,COUNT(MaLuotDV) FROM DV_THANHTOANQUATK GROUP BY MADV)
SELECT  TOP(3) with ties TenDV
FROM DICHVUTHANHTOAN , DEM_SO_GD
where DICHVUTHANHTOAN.MaDV = DEM_SO_GD.MADV 
order by  DEM_SO_GD.SOLUONGDUNG desc


