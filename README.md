# SQL Notları

## Kaynaklar

Notlar bu iki video kullanılarak çıkarılmıştır:
* [Verinin Kadim Dili SQL - Ömer Çolakoğlu](https://www.youtube.com/watch?v=Bcona5Fmu0E&t=2910s)
* [SQL Tutorial - Full Database Course for Beginners](https://www.youtube.com/watch?v=HXV3zeQKqGY&t=5943s)

## Veri Tipleri

### Sayısal Veri Tipleri

* bigint : min = -2^63, max = 2^63, 8 byte
* int:  min = -2^31, max = 2^31, 4 byte
* smallint: min = -2^15, max = 2^15, 2 byte
* tinyint: min = 0, max = 255, 1 byte
* float: -1.79308 ve -2.23308 arası 7 basamağa kadar 4 byte, 2.23208 ve 1.79308 arası 15 basamağa kadar 8 byte

### Metin Veri Tipleri

* char: her veri için karakter uzunluğunu ne kadar verdiysek o kadar yer tutar
* varchar: metin boyutu ne kadarsa o kadar yer tutar
* nchar: uluslararası karakterleri destekler(çin alfabesi vb.), char özelliği taşır, daha fazla yer kaplar  
* nvarchar: uluslararası karakterleri destekler(çin alfabesi vb.), varchar özelliği taşır, daha fazla yer kaplar  

### Tarih-Saat Veri Tipleri

* date: min = 0001-01-01 max = 9999-12-31, 4 byte
* smalldate: min = 1900-01-01 max = 2079-06-06, 3 byte
* datetime: min = 1753-01-01 00:00:00 max = 9999-12-31 23:59:59, 8 byte

## SQL Dili

## Temel SQL Komutları

#### Data Manipülasyon Komutları

* Select: Veri tabanındaki tablolardan kayıtları çeker
*	Insert: Tabloya yeni kayıt ekler
*	Update: Tablodaki verilerin bir ya da birden çok alanını değiştirir
* Delete: Tablodan kayıt siler
*	Truncate: Tablonun içini boşaltır(ilk haline çevirir)

#### Veri Tabanı Manipülasyon Komutları

* Create: Bir veri tabanı nesnesini oluşturur(table, view, database…)
* Alter: Bir veri tabanı nesnesinin özelliğini değiştirir
* Drop: Bir veri tabanı nesnesini siler

## SELECT Komutu

**SELECT** KOLON1,KOLON2,KOLON3… **FROM** TABLOADI **WHERE**<ŞARTLAR>

**SELECT** * **FROM** TABLOADI : Tüm kolonlardaki verileri getirir

## INSERT Komutu

**INSERT INTO** TABLOADI (KOLON1, KOLON2,KOLON3…) **VALUES** (DEĞER1,DEĞER2,DEĞER3…)

**INSERT INTO** CUSTOMERS (NAMESURNAME,GENDER,CITY) **VALUES** (“ZEYNEP AKTAŞLI”,”K”,”İSTANBUL”)

## UPDATE Komutu

**UPDATE** TABLOADI **SET** KOLON1=DEĞER1,KOLON2=DEĞER2,KOLON3=DEĞER3… **WHERE**<ŞARTLAR>

**UPDATE** CUSTOMERS **SET** COUNTRY=”TÜRKİYE”

Tabloda doğum tarihleri varsa ve yaş hesaplamak istersek:

**UPDATE** CUSTOMERS **SET** AGE=DATEDIFF(YEAR,BIRTHDATE,GETDATE())

*GETDATE(): Bugünün tarihini verir*

*YEAR: Yıllar arasındaki farkı hesaplamak istediğimiz için verilir*

## DELETE Koumutu

**DELETE FROM** TABLOADI WHERE<ŞARTLAR>

**DELETE FROM** CUSTOMERS: “CUSTOMERS”: veri tabanındaki tüm kayıtları siler

**DELETE FROM** student **WHERE** student_id=5: id’si 5 olan öğrenciyi siler

## TRUNCATE Komutu

**TRUNCATE TABLE** TABLOADI : Veri tabanındaki tüm kayıtları siler 

*DELETE ile farkı TRUNCATE sıra numaralarını sıfırlar(numaralar 1 den başlar), DELETE ise 10 kayıt varsa silip yeni kayıt eklediğimizde sıra numaraları 11 den başlar.*

## WHERE Komutu

*	= eşittir,
*	<> eşit değildir,
*	< büyüktür,
*	> küçüktür,
*	<= büyüktür ya da eşittir,
*	>= küçüktür ya da eşittir,
*	BETWEEN arasındadır,
*	LIKE ile başlar/ile biter/içerir,
*	IN içindedir, 
*	NOT LIKE ile başlamaz/ile bitmez/içermez,
*	NOT IN içinde değildir.

**SELECT** * **FROM** CUSTOMERS **WHERE** ID=1

**SELECT** * **FROM** CUSTOMERS **WHERE** CITY=”İSTANBUL”

**SELECT** * **FROM** CUSTOMERS **WHERE** ID>900

**SELECT** * **FROM** CUSTOMERS **WHERE** ID **BETWEEN** 500 **AND** 600 : 500 ve 600 dahil

**SELECT** * **FROM** CUSTOMERS **WHERE** NAMESURNAME **LIKE** “Serpil%” : Serpil ile başlayanlar

**SELECT** * **FROM** CUSTOMERS **WHERE** NAMESURNAME **LIKE** “%Ali%” : İçinde Ali geçenler

**SELECT** * **FROM** CUSTOMERS **WHERE** NAMESURNAME **LIKE** “%Üçel” : Üçel ile biter

**SELECT** * **FROM** CUSTOMERS **WHERE** CITY **IN** (“ANKARA”,”İSTANBUL”, “İZMİR”) : Ankara, İstanbul veya İzmir de olanlar

**SELECT** * **FROM** CUSTOMERS **WHERE** CITY **NOT IN** (“ANKARA”,”İSTANBUL”, “İZMİR”) : Ankara, İstanbul ve İzmir de olmayanlar

**DELETE FROM** CUSTOMERS **WHERE** ID=1 : ID=1 olanı sil

**UPDATE** CUSTOMERS **SET** GENDER=”ERKEK” **WHERE** GENDER=”E” : GENDER değeri E olanları ERKEK olarak değiştir

## AND OR Operatörleri

**SELECT** * **FROM** CUSTOMERS **WHERE** CITY=”ANKARA” **AND** GENDER=”E” **AND** TOWN=”ÇANKAYA”

**SELECT** * **FROM** CUSTOMERS **WHERE** BIRTHDATE>=”1990-01-01” **AND** BIRTHDATE<=”1995-12-31”

## DISTINCT Komutu

**SELECT DISTINCT** GENDER **FROM** CUSTOMERS : GENDER içinde kaç tür var (erkek ve kadın)

**SELECT DISTINCT** CITY **FROM** CUSTOMERS : Kaç şehir var?

## ORDER BY Komutu

**SELECT** KOLON1,KOLON2,KOLON3… **FROM** TABLOADI **WHERE**<ŞARTLAR> **ORDER** BY KOLON1 **ASC**,KOLON2 **DESC**…

**SELECT** * **FROM** CUSTOMERS **ORDER BY** NAMESURNAME **ASC** : İsimleri alfabetik sıraya göre getirir

**SELECT** * **FROM** CUSTOMERS **ORDER BY** CITY,TOWN : Şehir ve ilçeye göre alfabetik sıra

**SELECT** * **FROM** CUSTOMERS **ORDER BY** 2 **ASC** : 2. kolonu artan sıralı getirir

**SELECT** * **FROM** CUSTOMERS **ORDER BY** 2 : 2. kolonu artan sıralı getirir

**SELECT** * **FROM** CUSTOMERS **ORDER BY** 4 **DESC** : 4. kolonu azalan sıralı getirir

## TOP Komutu

**SELECT TOP** 10 * **FROM** CUSTOMERS **ORDER BY** 4 **DESC** : : 4. kolonun azalan sıralı ilk 10 verisini getirir. 

**SELECT TOP** 10 **PERCENT** * **FROM** CUSTOMERS **ORDER BY** 4 **DESC** : : 4. kolonun azalan sıralı %10 kadar verisini getirir. 

## (MySQL)LIMIT Komutu

**SELECT** * **FROM** STUDENT **ORDER BY** student_id **DESC LIMIT** 2; STUDENT tablosundan student_id’si azalan sıralı 2 veriyi getirir.

## Aggregate Fonksiyonları

*	SUM
*	MIN
*	MAX
*	AVG
*	COUNT

**SELECT SUM**(PRICE),**COUNT**(ID),**MIN**(PRICE),**MAX**(PRICE),**AVG**(PRICE) **FROM** TABLOADI

*	Bir ürünün ilk satış tarihini yazdırmak için:

	**SELECT MIN**(DATE_) **AS** ILKSATISTARIHI **FROM** SALES **WHERE** ITEMNAME **LIKE** “COLGATE”
*	Bir ürünün son satış tarihini yazdırmak için:

	**SELECT MAX**(DATE_) **AS** SONSATISTARIHI **FROM** SALES **WHERE** ITEMNAME **LIKE** “COLGATE”
*	Bir ürünün ilk satış, son satış ve kaç alışverişte alındığını yazdırmak için:

	**SELECT MIN**(DATE_) **AS** ILKSATISTARIHI, **MAX**(DATE_) **AS** SONSATISTARIHI,**COUNT**(*) **AS** SATIRSAYISI **FROM** SALES **WHERE** ITEMNAME **LIKE** “COLGATE”
*	Bir ürünün ilk satış, son satış ve her alışverişte toplam kaç tane satıldığını yazdırmak için:

	**SELECT MIN**(DATE_) **AS** ILKSATISTARIHI, **MAX**(DATE_) **AS** SONSATISTARIHI,**SUM**(AMOUNT) **AS** TOPLAMADET **FROM** SALES **WHERE** ITEMNAME **LIKE** “COLGATE”
*	Bir üründen toplam kazancı yazdırmak için:

	**SELECT SUM**(TOTALPRICE) **AS** TOPLAMTUTAR **FROM** SALES **WHERE** ITEMNAME **LIKE** “COLGATE”
*	Bir ürünün ortalama fiyatı:

	**SELECT AVG**(PRICE) **AS** ORTALAMAFIYAT **FROM** SALES **WHERE** ITEMNAME **LIKE** “COLGATE”
  
## GROUP BY Methodu

Yukarıda hesapladığımız tüm değerleri her ürün için hesaplatmak istersek group by kullanmamız gerekir.

•	Her ürünün ilk satış, son satış ve kaç alışverişte alındığını yazdırmak için:

**SELECT** ITEMNAME **MIN**(DATE_) **AS** ILKSATISTARIHI, **MAX**(DATE_) **AS** SONSATISTARIHI,COUNT(*) **AS** SATIRSAYISI **FROM** SALES **GROUP BY** ITEMNAME

•	Bir mağazanın gün bazlı satış rakamını getirme:

**SELECT CONVERT**(DATE, DATE_) **AS** TARIH,**SUM**(TOTALPRICE) **AS** TOPLAMSATIS **FROM** SALES **WHERE** BRANCH=”İSTANBUL” **GROUP BY** **CONVERT**(DATE, DATE_) **ORDER BY** **CONVERT**(DATE, DATE_)

*CONVERT() methodu ile tarih ve saat olan veri tipini sadece güne çevirdik. DATE güne çevirmek istediğimiz için yazıldı. DATE_ kolonun adı.*

•	Bir günün mağaza bazlı satış rakamını getirme(örneğin 2019-08-02):

**SELECT** CITY **AS** ŞEHİR,**SUM**(TOTALPRICE) **AS** TOPLAMSATIS **FROM** SALES **WHERE** **CONVERT**(DATE, DATE_)=”2019-08-02” **GROUP BY** CITY

•	Mağazaların aylara göre satış rakamını getirme:

**SELECT** CITY **AS** ŞEHİR,**DATEPART**(MONTH, DATE_) **AS** AY,**SUM**(TOTALPRICE) **AS** TOPLAMSATIS **FROM** SALES **GROUP BY** CITY **ORDER BY** CITY, **DATEPART**(MONTH, DATE_)

•	Ürün kategorilerine göre azalan sırada satışları getirme:

**SELECT** CATEGORY **AS** KATEGORİ,**SUM**(TOTALPRICE) **AS** TOPLAMSATIS **FROM** SALES **GROUP BY** CATEGORY **ORDER BY SUM**(TOTALPRICE) **DESC**

•	Mağazaların müşteri sayılarını getirme (müşteri adına göre saydırma):

**SELECT** CITY **AS** ŞEHİR,**COUNT**(**DISTINCT** CUSTOMERNAME) **AS** MUSTERİSAYISI **FROM** SALES **GROUP BY** CITY

*DISTINCT kullandık çünkü bir müşteri birden fazla kez alışveriş yapmış olabilir.*

•	Belli bir cironun üstünde satış yapan mağazaları getirme:

**SELECT** CITY **AS** ŞEHİR,**SUM**(TOTALPRICE) **AS** TOPLAMSATIS **FROM** SALES **GROUP BY** CITY
**HAVING SUM**(TOTALPRICE) >100000 **ORDER BY** SUM(TOTALPRICE) **DESC**

*WHERE içine SUM(TOTALPRICE) >100000 yazamayız çünkü WHERE içinde aggregate fonksiyon kullanılmaz. Bu sebeple HAVING kullandık.*

## CREATE Komutu

**CREATE TABLE** tablo_adı(

kolon_adı **INT AUTO_INCREMENT**,  *AUTO_INCREMENT girilmesi gerekmeden artar*
  
kolon_adı **VARCHAR(20) NOTNULL**,  *NOTNULL o kolonda null olamayacağını gösterir*
  
kolon_adı **VARCHAR(20) UNIQUE**,  *UNIQUE o kolonda aynı değerlerin olamayacağı*
  
**PRIMARY KEY**(kolon_adı)
  
);

## DROP Komutu

**DROP TABLE** student; Tabloyu siler

## ALTER Komutu

Tabloyu düzenlemek için kullanılır.

*	**ALTER TABLE** student **ADD** gpa **DECIMAL**(3,2);  3 sayıdan oluşan, 2si noktadan sonra gelen sayı içeren yeni kolon ekler.

*	**ALTER TABLE** student **DROP COLUMN** gpa; gpa kolonunu siler

## İlişkisel Veri Tabanları

USERS tablosu ID kolonundan ADDRESS kolonunun USERID kolonuna bağlıdır.

*	ID=1 olan datayı çekmek

**SELECT** USERS, ADRESS **FROM** USERS,ADDRESS **WHERE** USERS.ID=ADDRES.USERID **AND** USERS.ID=1

*CITIES tablosu ID kolonundan ADDRESS kolonunun CITYID kolonuna bağlıdır*

*	ID=1 olan datayı çekmek

**SELECT** USERS.USERNAME,USERS.NAMESURNAME, ADRESS *,CITIES.CITY **FROM** USERS,ADDRESS,CITIES **WHERE** USERS.ID=ADDRES.USERID **AND** CITIES.ID=ADDRESS.CITYID **AND** USERS.ID=1

*USERS.USERNAME yazarak USERS tablosundan sadece USERNAME kolonunun gösterilmesi sağlanır.*

Tabloların adlarını kısa kullanabiliriz:

**SELECT** U, A **FROM** USERS U,ADDRESS A **WHERE** U.ID=A.USERID **AND** U.ID=1

## İlişkisel Veri Tabanı Oluşturma Örneği

[Mike Dane Creating Company Database](https://www.mikedane.com/databases/sql/creating-company-database/)

## UNION Komutu

* Çalışan ve şube isimlerinin listesini getir:

*Alt alta önce isimleri sonra şubeleri yazdırır*

**SELECT** first_name **AS** Company_Names **FROM** employee;
**UNION**
**SELECT** branch_name **FROM** branch; 

* Müşteri ve şube tedarikçilerini id ile getir:

**SELECT** client_name, branch_id *(client.branch_id de yazılabilir)* **FROM** client;
**UNION**
**SELECT** supplier_name, branch_id *(branch_supplier.brnach_id de yazılabilir)* **FROM** branch_supplier; 

## JOIN Komutu

![image](https://user-images.githubusercontent.com/79712981/216787453-f33ff596-1ec9-4a0c-a3e3-c581594dd7b2.png)
[Resim Kaynağı](https://tr.wikipedia.org/wiki/Dosya:SQL_Joins.svg)

* Tüm şubeleri ve müdürlerinin isimlerini getir:

**SELECT** employee.emp_id, employee.first_name, branch.branch_name **FROM** employee **JOIN** branch **ON** employee.emp_id=branch.mgr_id;

* Tüm isimleri getirip müdür olanların şubelerini getir:

**SELECT** employee.emp_id, employee.first_name, branch.branch_name **FROM** employee **LEFT JOIN** branch **ON** employee.emp_id=branch.mgr_id;

* Tüm şubeleri ve varsa müdürlerini getir:

**SELECT** employee.emp_id, employee.first_name, branch.branch_name **FROM** employee **RIGHT JOIN** branch **ON** employee.emp_id=branch.mgr_id;




