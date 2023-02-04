# SQL-Notlar

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

### Temel SQL Komutları

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

### SELECT Komutu

**SELECT** KOLON1,KOLON2,KOLON3… **FROM** TABLOADI **WHERE**<ŞARTLAR>

**SELECT** * **FROM** TABLOADI : Tüm kolonlardaki verileri getirir

### INSERT Komutu

**INSERT INTO** TABLOADI (KOLON1, KOLON2,KOLON3…) **VALUES** (DEĞER1,DEĞER2,DEĞER3…)

**INSERT INTO** CUSTOMERS (NAMESURNAME,GENDER,CITY) **VALUES** (“ZEYNEP AKTAŞLI”,”K”,”İSTANBUL”)

### UPDATE Komutu

**UPDATE** TABLOADI **SET** KOLON1=DEĞER1,KOLON2=DEĞER2,KOLON3=DEĞER3… **WHERE**<ŞARTLAR>

**UPDATE** CUSTOMERS **SET** COUNTRY=”TÜRKİYE”

Tabloda doğum tarihleri varsa ve yaş hesaplamak istersek:

**UPDATE** CUSTOMERS **SET** AGE=DATEDIFF(YEAR,BIRTHDATE,GETDATE())

*GETDATE(): Bugünün tarihini verir*

*YEAR: Yıllar arasındaki farkı hesaplamak istediğimiz için verilir*

### DELETE Koumutu

**DELETE FROM** TABLOADI WHERE<ŞARTLAR>

**DELETE FROM** CUSTOMERS: “CUSTOMERS”: veri tabanındaki tüm kayıtları siler

**DELETE FROM** student **WHERE** student_id=5: id’si 5 olan öğrenciyi siler

### TRUNCATE Komutu

**TRUNCATE TABLE** TABLOADI : Veri tabanındaki tüm kayıtları siler 

*DELETE ile farkı TRUNCATE sıra numaralarını sıfırlar(numaralar 1 den başlar), DELETE ise 10 kayıt varsa silip yeni kayıt eklediğimizde sıra numaraları 11 den başlar.*

### WHERE Komutu

*	= eşittir,
*	 <> eşit değildir,
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

### AND OR Operatörleri

**SELECT** * **FROM** CUSTOMERS **WHERE** CITY=”ANKARA” **AND** GENDER=”E” **AND** TOWN=”ÇANKAYA”

**SELECT** * **FROM** CUSTOMERS **WHERE** BIRTHDATE>=”1990-01-01” **AND** BIRTHDATE<=”1995-12-31”

### DISTINCT Komutu

**SELECT DISTINCT** GENDER **FROM** CUSTOMERS : GENDER içinde kaç tür var (erkek ve kadın)

**SELECT DISTINCT** CITY **FROM** CUSTOMERS : Kaç şehir var?

### ORDER BY Komutu

**SELECT** KOLON1,KOLON2,KOLON3… **FROM** TABLOADI **WHERE**<ŞARTLAR> **ORDER** BY KOLON1 **ASC**,KOLON2 **DESC**…

**SELECT** * **FROM** CUSTOMERS **ORDER BY** NAMESURNAME **ASC** : İsimleri alfabetik sıraya göre getirir

**SELECT** * **FROM** CUSTOMERS **ORDER BY** CITY,TOWN : Şehir ve ilçeye göre alfabetik sıra

**SELECT** * **FROM** CUSTOMERS **ORDER BY** 2 **ASC** : 2. kolonu artan sıralı getirir

**SELECT** * **FROM** CUSTOMERS **ORDER BY** 2 : 2. kolonu artan sıralı getirir

**SELECT** * **FROM** CUSTOMERS **ORDER BY** 4 **DESC** : 4. kolonu azalan sıralı getirir

### TOP Komutu

**SELECT TOP** 10 * **FROM** CUSTOMERS **ORDER BY** 4 **DESC** : : 4. kolonun azalan sıralı ilk 10 verisini getirir. 

**SELECT TOP** 10 **PERCENT** * **FROM** CUSTOMERS **ORDER BY** 4 **DESC** : : 4. kolonun azalan sıralı %10 kadar verisini getirir. 

### (MySQL)LIMIT Komutu

**SELECT** * **FROM** STUDENT **ORDER BY** student_id **DESC LIMIT** 2; STUDENT tablosundan student_id’si azalan sıralı 2 veriyi getirir.

## Aggregate Fonksiyonları

*	SUM
*	MIN
*	MAX
*	AVG
*	COUNT


