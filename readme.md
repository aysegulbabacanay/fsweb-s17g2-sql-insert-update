# SQL Sorgu Alıştırmaları

Bu hafta SQL sorguları üzerine çalışıyorsunuz. Bugünkü alıştırmada sizin için hazırladığımız veritabanında aşağıda istediğimiz sonuçları elde etmenize yarayan SQL sorgularını oluşturacaksınız.

# Proje Kurulumu
Projeyi forklayın ve clonlayın. Tamamladığınızda da pushlayın.

## Kütüphane Bilgi Sistemi

Bu veritabanı, bir okulun kütüphanesinden öğrencilerin aldıkları kitapların bilgisini barındırmaktadır.

#Tablolar 
`ogrenci` tablosu öğrencilerin listesini tutar.
`islem` tablosu öğrencilerin kütüphaneden aldıkları kitapların bilgilerini tutar
`kitap` tablosu kütüphanedeki kitapların bilgisini tutar
`yazar` tablosu kitapların yazarları bilgisini tutar
`tur` tablosu kitapların türlerini tutar.

Tablo ilişiklerini görmek için [ktphn.png] dosyasına göz atın.

Yazdığınız sorguları buradan test edebilirsiniz: [https://ergineer.com/assets/materials/fkg36so5-kutuphanebilgisistemi-sql/]



# Görevler
Aşağıda istenilen sonuçlara ulaşabilmek için gerekli SQL sorgularını yazın. 

	1) ÖRNEK SORU: Yazar tablosunu KEMAL UYUMAZ isimli yazarı ekleyin.
	

     INSERT INTO yazar (yazarad,yazarsoyad) VALUES("KEMAL","UYUMAZ")
	
	2) Biyografi türünü tür tablosuna ekleyiniz.

	INSERT INTO tur (turadi) VALUES ("Biyografi")
	
	
	3) 10A sınıfı olan ÇAĞLAR ÜZÜMCÜ isimli erkek, sınıfı 9B olan LEYLA ALAGÖZ isimli kız ve sınıfı 11C olan Ayşe Bektaş isimli kız öğrencileri tek sorguda ekleyin. 
	
	INSERT INTO ogrenci (ograd,ogrsoyad,cinsiyet,sinif) VALUES ("ÇAĞLAR","ÜZÜMCÜ","E","10A"),("LEYLA","ALAGÖZ","K","9B"),("Ayşe","Bektaş","K","11C");

	4) Öğrenci tablosundaki rastgele bir öğrenciyi yazarlar tablosuna yazar olarak ekleyiniz.
	
	INSERT INTO yazar (yazarad, yazarsoyad) SELECT ograd,ogrsoyad FROM ogrenci ORDER BY random() LIMIT 1

	
	5) Öğrenci numarası 10 ile 30 arasındaki öğrencileri yazar olarak ekleyiniz.

	INSERT INTO yazar(yazarad,yazarsoyad) select ograd,ogrsoyad from ogrenci where ogrno between "10" and "30";
	
	
	6) Nurettin Belek isimli yazarı ekleyip yazar numarasını yazdırınız.
	(Not: Otomatik arttırmada son arttırılan değer @@IDENTITY değişkeni içinde tutulur.)

	//INSERT INTO yazar (yazarad,yazarsoyad) VALUES ("Nurettin","Belek") SELECT yazarno
	
	
	7) 10B sınıfındaki öğrenci numarası 3 olan öğrenciyi 10C sınıfına geçirin.

        UPDATE ogrenci SET sinif="10C" WHERE ogrno=3 
	
	
	8) 9A sınıfındaki tüm öğrencileri 10A sınıfına aktarın

	UPDATE ogrenci SET sinif="10A" WHERE sinif="9A  "
	
	
	9) Tüm öğrencilerin puanını 5 puan arttırın.

	UPDATE ogrenci SET puan=puan+5;
	
	
	10) 25 numaralı yazarı silin.

      DELETE from yazar WHERE yazarno=25;

	11) Doğum tarihi null olan öğrencileri listeleyin. (insert sorgusu ile girilen 3 öğrenci listelenecektir)
	
	select * from ogrenci where dtarih IS NULL;

	12) Doğum tarihi null olan öğrencileri silin. 

	delete from ogrenci where dtarih is null
	
	
	13) Kitap tablosunda adı a ile başlayan kitapların puanlarını 2 artırın.

	update kitap set puan = puan +2 where kitapadi like "A%"
	
	
	14) Kişisel Gelişim isimli bir tür oluşturun.

	INSERT INTO TUR(turadi) VALUES("Kişisel Gelişim")

	//update ogrenci  set sinif= trim(sinif)

	
	
	15) Kitap tablosundaki Başarı Rehberi kitabının türünü bu tür ile değiştirin.
	
	//update tur set turadi=trim(turadi);
     update kitap set turno=(select turno from tur where turadi="Kişisel Gelişim") where kitapadi="Başarı Rehberi";

	
	16) Öğrenci tablosunu kontrol etmek amaçlı tüm öğrencileri görüntüleyen "ogrencilistesi" adında bir prosedür oluşturun.
	
	
	17) Öğrenci tablosuna yeni öğrenci eklemek için "ekle" adında bir prosedür oluşturun.
	
	
	18) Öğrenci noya göre öğrenci silebilmeyi sağlayan "sil" adında bir prosedür oluşturun.
	
	
	19) Öğrenci numarasını kullanarak kolay bir biçimde öğrencinin sınıfını değiştirebileceğimiz bir prosedür oluşturun.

	 CREATE PROCEDURE sinifDegis (
    In no INT
    In newsinif TEXT
)
AS
    BEGIN
        update ogrenci set sinif = newsinif where ogrno = no
    END
GO;

EXEC sinifDegis(1,"10A")

	
	20) Öğrenci adı ve soyadını "Ad Soyad" olarak birleştirip, ad soyada göre kolayca arama yapmayı sağlayan bir prosedür yazın.
	
	
	21) Daha önceden oluşturduğunu tüm prosedürleri silin.
	
	
	#Esnek görevler (Esnek görevlerin hepsini Select in Select ile gerçekleştirmeniz beklenmektedir.)
	22) Select in select yöntemiyle dram türündeki kitapları listeleyiniz.
	
	
	23) Adı e harfi ile başlayan yazarların kitaplarını listeleyin.
	
	select * from kitap where yazarno in (select yazarno from yazar where yazarad like "E%");
	
	24) Kitap okumayan öğrencileri listeleyiniz.


	
	
	25) Okunmayan kitapları listeleyiniz

	select * from kitap where kitapno not in (select kitapno from islem);

    control : select distinct kitapno from islem  order by kitapno


	26) Mayıs ayında okunmayan kitapları listeleyiniz.

	select * from kitap where kitapno in(select kitapno from islem where atarih not like '%-05-%');



# Görevler
Aşağıda istenilen sonuçlara ulaşabilmek için gerekli SQL sorgularını yazın. 



	1) ÖRNEK SORU: Yazar tablosunu KEMAL UYUMAZ isimli yazarı ekleyin.
	

	
	2) Biyografi türünü tür tablosuna ekleyiniz.
	
	
	3) 10A sınıfı olan ÇAĞLAR ÜZÜMCÜ isimli erkek, sınıfı 9B olan LEYLA ALAGÖZ isimli kız ve sınıfı 11C olan Ayşe Bektaş isimli kız öğrencileri tek sorguda ekleyin. 
	
	
	4) Öğrenci tablosundaki rastgele bir öğrenciyi yazarlar tablosuna yazar olarak ekleyiniz.
	
	
	5) Öğrenci numarası 10 ile 30 arasındaki öğrencileri yazar olarak ekleyiniz.
	
	
	6) Nurettin Belek isimli yazarı ekleyip yazar numarasını yazdırınız.
	(Not: Otomatik arttırmada son arttırılan değer @@IDENTITY değişkeni içinde tutulur.)
	
	
	7) 10B sınıfındaki öğrenci numarası 3 olan öğrenciyi 10C sınıfına geçirin.
	
	
	8) 9A sınıfındaki tüm öğrencileri 10A sınıfına aktarın
	
	
	9) Tüm öğrencilerin puanını 5 puan arttırın.
	
	
	10) 25 numaralı yazarı silin.


	11) Doğum tarihi null olan öğrencileri listeleyin. (insert sorgusu ile girilen 3 öğrenci listelenecektir)
	
	
	12) Doğum tarihi null olan öğrencileri silin. 
	
	
	13) Kitap tablosunda adı a ile başlayan kitapların puanlarını 2 artırın.
	
	
	14) Kişisel Gelişim isimli bir tür oluşturun.
	
	
	15) Kitap tablosundaki Başarı Rehberi kitabının türünü bu tür ile değiştirin.
	
	
	16) Öğrenci tablosunu kontrol etmek amaçlı tüm öğrencileri görüntüleyen "ogrencilistesi" adında bir prosedür oluşturun.
	
	
	17) Öğrenci tablosuna yeni öğrenci eklemek için "ekle" adında bir prosedür oluşturun.
	
	
	18) Öğrenci noya göre öğrenci silebilmeyi sağlayan "sil" adında bir prosedür oluşturun.
	
	
	19) Öğrenci numarasını kullanarak kolay bir biçimde öğrencinin sınıfını değiştirebileceğimiz bir prosedür oluşturun.
	
	
	20) Öğrenci adı ve soyadını "Ad Soyad" olarak birleştirip, ad soyada göre kolayca arama yapmayı sağlayan bir prosedür yazın.
	
	
	21) Daha önceden oluşturduğunu tüm prosedürleri silin.
	
	
	#Esnek görevler (Esnek görevlerin hepsini Select in Select ile gerçekleştirmeniz beklenmektedir.)
	22) Select in select yöntemiyle dram türündeki kitapları listeleyiniz.
	
	
	23) Adı e harfi ile başlayan yazarların kitaplarını listeleyin.
	
	
	24) Kitap okumayan öğrencileri listeleyiniz.
	
	
	25) Okunmayan kitapları listeleyiniz

	
	26)Mayıs ayında okunmayan kitapları listeleyiniz.