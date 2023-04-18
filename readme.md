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
    	cevap:  insert into yazar(yazarad,yazarsoyad)
    			values("Kemal","Uyumaz")


    2) Biyografi türünü tür tablosuna ekleyiniz.
    	cevap:  insert into tur(turadi)
    			values("Biyografi")


    3) 10A sınıfı olan ÇAĞLAR ÜZÜMCÜ isimli erkek, sınıfı 9B olan LEYLA ALAGÖZ isimli kız ve sınıfı 11C olan Ayşe Bektaş isimli kız öğrencileri tek sorguda ekleyin.
    	cevap:	insert into ogrenci(sinif,ograd,ogrsoyad,cinsiyet)
    			values("10A","Çağlar","Üzümcü","E"),
    			("9B","Leyla","Alagöz","K"),
    			("11C","Ayşe","Bektaş","K")


    4) Öğrenci tablosundaki rastgele bir öğrenciyi yazarlar tablosuna yazar olarak ekleyiniz.
    	cevap:	insert into yazar(yazarad,yazarsoyad)
    			select ograd,ogrsoyad from ogrenci
    			where rand()
    			limit 1


    5) Öğrenci numarası 10 ile 30 arasındaki öğrencileri yazar olarak ekleyiniz.
    	cevap:	insert into yazar(yazarad,yazarsoyad)
    			values(select ograd,ogrsoyad from ogrenci
    			where ogrno>=10 and ogrno=<30)


    6) Nurettin Belek isimli yazarı ekleyip yazar numarasını yazdırınız.
    (Not: Otomatik arttırmada son arttırılan değer @@IDENTITY değişkeni içinde tutulur.)
    	cevap:	insert into yazar (yazarad,yazarsoyad)
    			values ("Nurettin","Belek");
    			select @@IDENTITY

    7) 10B sınıfındaki öğrenci numarası 3 olan öğrenciyi 10C sınıfına geçirin.
    	cevap:	update ogrenci set sinif="10C" where ogrno=3

    8) 9A sınıfındaki tüm öğrencileri 10A sınıfına aktarın
    	cevap: update ogrenci set sinif='10A' where sinif='9A'

    9) Tüm öğrencilerin puanını 5 puan arttırın.
    	cevap: update ogrenci set puan=puan+5

    10) 25 numaralı yazarı silin.
    	cevap: delete FROM  yazar where yazarno=25


    11) Doğum tarihi null olan öğrencileri listeleyin. (insert sorgusu ile girilen 3 öğrenci listelenecektir)
    	cevao:  select * from ogrenci
    			where dtarih is null

    12) Doğum tarihi null olan öğrencileri silin.
    	cevap:  delete from ogrenci
    			where dtarih  is null

    13) Kitap tablosunda adı a ile başlayan kitapların puanlarını 2 artırın.
    	cevap:  update kitap set puan=puan+2
    			where kitapadi like 'a%'

    14) Kişisel Gelişim isimli bir tür oluşturun.
    	cevap:	insert into tur(turadi)
    			values ('Kişisel Gelişim')

    15) Kitap tablosundaki Başarı Rehberi kitabının türünü bu tür ile değiştirin.
    	cevap:	update kitap set turno=8
    			where kitapadi='Başarı Rehberi'

    16) Öğrenci tablosunu kontrol etmek amaçlı tüm öğrencileri görüntüleyen "ogrencilistesi" adında bir prosedür oluşturun.
    	cevap:	CREATE PROCEDURE ogrencilistesi()
    			BEGIN
    			select * from ogrenci;
    			END ;

    17) Öğrenci tablosuna yeni öğrenci eklemek için "ekle" adında bir prosedür oluşturun.
    	cevap:	create procedure ekle(
    		in name varchar(50)
    		in surname varchar(50)
    	)
    	begin
    	insert into ogrenci(ograd,ogrsoyad)

    18) Öğrenci noya göre öğrenci silebilmeyi sağlayan "sil" adında bir prosedür oluşturun.
    	cevap:	CREATE PROCEDURE sil(no INT)
    			BEGIN
    			delete from ogrenci WHERE ogrno = no ;
    			END;


    19) Öğrenci numarasını kullanarak kolay bir biçimde öğrencinin sınıfını değiştirebileceğimiz bir prosedür oluşturun.
    	cevap:	create procedure sinifdegistir(no INT,sube VARCHARACTER(25))
    			BEGIN
    			update ogrenci set sinif=sube where ogrno = no;
    			END;

    20) Öğrenci adı ve soyadını "Ad Soyad" olarak birleştirip, ad soyada göre kolayca arama yapmayı sağlayan bir prosedür yazın.
    	cevap:	create procedure ogrenciarama(IN AdSoyad varcharacter(35))
    			BEGIN
    			SELECT * FROM ogrenci
    			WHERE CONCAT(ograd, ' ', ogrsoyad) LIKE CONCAT ('%', AdSoyad, '%');
    			END;

    21) Daha önceden oluşturduğunu tüm prosedürleri silin.
    	cevap:	DROP PROCEDURE IF EXISTS ogrenciarama;
    			DROP PROCEDURE IF EXISTS Ekle;
    			DROP PROCEDURE IF EXISTS ogrencilistesi;
    			DROP PROCEDURE IF EXISTS sil;
    			DROP PROCEDURE IF EXISTS sinifdegistir;


    #Esnek görevler (Esnek görevlerin hepsini Select in Select ile gerçekleştirmeniz beklenmektedir.)
    22) Select in select yöntemiyle dram türündeki kitapları listeleyiniz.
    	cevap:	select tur.turadi ,kitap.kitapadi from tur,kitap
    			where kitap.turno=tur.turno
    			and tur.turadi =(
    			select tur.turadi from tur
    			where tur.turadi like '%dram%'
    			)

    23) Adı e harfi ile başlayan yazarların kitaplarını listeleyin.


    24) Kitap okumayan öğrencileri listeleyiniz.


    25) Okunmayan kitapları listeleyiniz


    26) Mayıs ayında okunmayan kitapları listeleyiniz.
