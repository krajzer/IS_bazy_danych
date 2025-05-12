# IS_bazy_danych

Właściciel repozytorium: Konrad Rajzer

1. Nagłówki
# Nagłówek poziomu 1 (H1)
## Nagłówek poziomu 2 (H2)
### Nagłówek poziomu 3 (H3)
#### Nagłówek poziomu 4 (H4)
##### Nagłówek poziomu5 (5)
###### Nagłówek poziomu 6 (H6)

2. Listy
1. Element 1
2. Element 2

1. Elem1
2. Elem2
3. Elem3

Lista wypunktowana
* punkt 1
* punkt 2
  * punkt 2.1
 
# Przykładowy format zapisywania rozwiązań

## Rozwiązania zadań lab1, częśc 1

**Zadanie 1**
```sql

create table pracownik2 (
id int auto_increment primary key,
imie varchar(50) not null,
nazwisko varchar(100) not null,
data_urodzenia date,
stanowisko enum ('sprzedawca', 'magazynier', 'księgowa')
);
```

**Zadanie 2**
# Zadanie 2
```
INSERT INTO pracownik(id, imie, nazwisko, data_urodzenia, stanowisko) values
(default, 'Jan', 'Kowalski', '1990-10-10', 'magazynier'),
(default, 'Konrad', 'Rajzer', '1987-07-06', 'sprzedawca'),
(default, 'Anna', 'Biernat', '1995-02-08', 'księgowa');

insert into pracownik(id, imie, nazwisko, data_urodzenia, stanowisko) values
(default, 'Genowef', 'Rudzikowski', '1925-01-01', 'magazynier');
```
###Stwórz tabelę dzial z kolumnami:

#id - liczba, autonumer, klucz główny
#nazwa - tekst, max. 255 znaków

# Zadanie 3
```
create table dzial(
id int auto_increment primary key,
nazwa varchar(255)
);

ALTER TABLE dzial
ADD sprzedaz VARCHAR(50),	
ADD ksiegowosc VARCHAR(50),
ADD magazyn VARCHAR(50);
```
# Zadanie 4

```
INSERT INTO dzial (nazwa_dzialu) VALUES # id to auto_increment
('sprzedaz'),
('księgowość'),
('magazyn');
```

# Zadanie 5
```
alter table pracownik modify stanowisko varchar(50) default 'sprzedawca';
```
# Zadanie 6
# 7 pozycji z czego 2 po przecinku
```
alter table pracownik add column pensja decimal(7,2);
```
# Zadanie 7
```
Alter table dzial RENAME COLUMN nazwa TO nazwa_dzialu;
alter table dzial rename column id TO id_dzialu;
alter table pracownik rename column id to id_pracownika;
```
# Zadanie 8

#delete from pracownik1 where id =(select max(id) from pracownik2); nie działa podwójne zapytanie
#ustawienie zmiennej max_id celem wyszukania najwyższego id bez wcześniejszego sprawdzenia w bazie do którego rekordu należy
```SET @max_id = (SELECT MAX(id_pracownika) FROM pracownik);
SELECT @max_id;

delete from pracownik where id_pracownika = @max_id;

```
# lab1 zadanie 2

# Zadanie 1
```
alter table pracownik add column dzial int;
alter table pracownik add foreign key (dzial) references dzial (id_dzialu) on delete cascade;


delete from dzial where id_dzialu = 1;
select * from dzial;
```
# Zadanie

# Zadanie 2

```
create table stanowisko(
id_stanowiska int primary key,
nazwa_stanowiska varchar(50)
);

insert into stanowisko values
(1, 'sprzedawca'),
(2, 'ksiegowosc'),
(3, 'magazyn');
```

# Zadanie 3
```
alter table pracownik add column stanowisko_temp int;
alter table pracownik add foreign key (stanowisko_temp) references stanowisko (id_stanowiska);

update pracownik set stanowisko_temp = 3 where stanowisko = 'magazynier';
update pracownik set stanowisko_temp = 1 where stanowisko = 'sprzedawca';
update pracownik set stanowisko_temp = 2 where stanowisko = 'ksiegowa';
```
# Zadanie 4
```
alter table pracownik drop foreign key pracownik_ibfk_1;
alter table pracownik add foreign key (dzial) references dzial (id_dzialu) on delete set null;
```


## Lab 2 cz. 1

#Zadanie 1
```
select nazwisko from pracownik
order by nazwisko asc
```
#Zadanie 2

```
select imie, nazwisko, pensja
from pracownik
where year(data_urodzenia) > 1979;
```

#Zadanie 3

```
select *
from pracownik
where pensja between 3500 and 5000;
```

#Zadanie 4

```
select *
from towar
join stan_magazynowy on towar.id_towaru = stan_magazynowy.towar
where stan_magazynowy.ilosc > 10;
```

#Zadanie 5

```
select *
from towar
where nazwa_towaru like 'A%'
	or nazwa_towaru like 'B'
	or nazwa_towaru like 'C';
```
#Zadanie 6

```
select *
from klient
where czy_firma = "0";
```

#Zadanie 7

```
select *
from zamowienie
order by data_zamowienia desc limit 10;
```

#Zadanie 8

```
select *
from pracownik
order by pensja asc limit 5;
```

#Zadanie 9

```
select *
from towar
where nazwa_towaru not like '%a%'
order by cena_zakupu desc limit 10;
```

#Zadanie 10

```
select *
from towar
join stan_magazynowy on towar.kategoria = stan_magazynowy.towar
join jednostka_miary on jednostka_miary.id_jednostki = stan_magazynowy.towar
where jednostka_miary.nazwa = 'szt'
order by towar.nazwa_towaru, towar.cena_zakupu desc;
```

#Zadanie 11

```
CREATE TABLE towary_powyzej_100 AS
SELECT * FROM towary
WHERE cena >= 100;
```

#Zadanie 12

```
CREATE TABLE pracownik_50_plus LIKE pracownik;

INSERT INTO pracownik_50_plus
SELECT * FROM pracownik WHERE wiek >= 50;
```

## Funkcje, agregacja i grupowanie. Zadania.
# Zadanie 1
```
select imie, nazwisko, data_urodzenia from pracownik;
```
# Zadanie 2
```
SELECT imie, nazwisko, year(data_urodzenia) from pracownik;
```

# zadanie 3
```
select dzial.nazwa, count(pracownik.dzial)
from dzial
left join pracownik on dzial.id_dzialu = pracownik.dzial
group by dzial.nazwa
```
# Zadanie 4
```
select kategoria.nazwa_kategori, count(towar.id_towaru)
from kategoria
left join towar on kategoria.id_kategori = towar.kategoria
group by kategoria.nazwa_kategori;
```
# Zadanie 5
```
select k.nazwa_kategori, group_concat(t.nazwa_towaru separator ', ') as towary
from kategoria k
left join towar t on k.id_kategori = t.kategoria
group by k.nazwa_kategori;
```
# Zadanie 6
```
select round(avg(pensja), 2) as serdnia_pensja
from pracownik;
```
# Zadanie 7
```
select round(avg(pensja),2) from pracownik
where year(curdate()) - year(data_zatrudnienia) >=5;
```
# Zadanie 8
```
select t.nazwa_towaru, sum(poz_zam.ilosc) as ilosc_sprzedana
from towar t left join pozycja_zamowienia poz_zam on poz_zam.towar = t.id_towaru
group by t.nazwa_towaru
order by ilosc_sprzedana desc
limit 10;
```
#Zadanie 9
```
select z.numer_zamowienia, sum(poz_zam.ilosc * poz_zam.cena) as wartosc_zam
from zamowienie z join pozycja_zamowienia poz_zam on z.id_zamowienia = poz_zam.zamowienie
where year(z.data_zamowienia) = 2017 and month(z.data_zamowienia) between 1 and 3
group by z.numer_zamowienia;
```
# Zadanie 10
```
select pracownik.imie, pracownik.nazwisko, sum(pozycja_zamowienia.cena * pozycja_zamowienia.ilosc) as wartosc_zam
from pracownik
join zamowienie on pracownik.id_pracownika = zamowienie.pracownik_id_pracownika
join pozycja_zamowienia on zamowienie.id_zamowienia = pozycja_zamowienia.zamowienie
group by pracownik.imie, pracownik.nazwisko
order by wartosc_zam;
```
## Zadania lab3 cz.2
# Zadanie 1
```
select d.nazwa, max(p.pensja) as maks_pensja, avg(p.pensja) as srednia_pensja
from dzial d join pracownik p on d.id_dzialu = p.dzial
group by d.nazwa
order by maks_pensja;
```
# Zadanie 2
```
select k.pelna_nazwa as klient, sum(p_zam.ilosc * p_zam.cena) as wartosc_zamowienia
from klient k
join zamowienie z on k.id_klienta = z.klient
join pozycja_zamowienia p_zam on z.id_zamowienia = p_zam.zamowienie
group by k.pelna_nazwa
order by wartosc_zamowienia desc
limit 10;
```
# Zadanie 3
```
select sum(p_zam.ilosc * p_zam.cena) as wartosc_przychodu, year(z.data_zamowienia)
from pozycja_zamowienia p_zam
join zamowienie z on z.id_zamowienia = p_zam.zamowienie
group by year(z.data_zamowienia);
```
# Zadanie 4
```
select s_zam.nazwa_statusu_zamowienia, sum(p_zam.ilosc * p_zam.cena) as wartosc
from status_zamowienia s_zam
join zamowienie on zamowienie.status_zamowienia = s_zam.id_statusu_zamowienia
join pozycja_zamowienia p_zam on zamowienie.id_zamowienia = p_zam.zamowienie
where s_zam.nazwa_statusu_zamowienia = "anulowane"
group by s_zam.nazwa_statusu_zamowienia;
```
# Zadanie 5
```
select a.miejscowosc, sum(pozycja_zamowienia.ilosc * pozycja_zamowienia.cena) as wartosc
from zamowienie z
join klient on z.klient = klient.id_klienta
join adres_klienta a on klient.id_klienta = a.klient
join pozycja_zamowienia on z.id_zamowienia = pozycja_zamowienia.zamowienie
group by a.miejscowosc;
```
# Zadanie 6
```
select sum(p_zam.ilosc * p_zam.cena) as wartosc
from pozycja_zamowienia p_zam
join zamowienie on p_zam.zamowienie = zamowienie.id_zamowienia
join status_zamowienia on zamowienie.status_zamowienia = status_zamowienia.id_statusu_zamowienia
where status_zamowienia.nazwa_statusu_zamowienia = "zrealizowane";
```
# Zadanie 7
```
select sum(p_zam.ilosc * (p_zam.cena - towar.cena_zakupu)) as suma
from pozycja_zamowienia p_zam
join zamowienie on p_zam.zamowienie = zamowienie.id_zamowienia
join towar on p_zam.towar = towar.id_towaru;
```
# Zadanie 8
```
select s.towar, s.ilosc, s.jm, k.nazwa_kategori
from stan_magazynowy s
join towar on s.towar = towar.id_towaru
join kategoria k on towar.kategoria = k.id_kategori;
```
# Zadanie 9
```
SELECT MONTHNAME(data_urodzenia) AS miesiac, 
       COUNT(*) AS liczba_pracownikow
FROM pracownik
GROUP BY miesiac
```
# Zadanie 10
```
select pracownik.id_pracownika as id,
concat(pracownik.imie, ' ', pracownik.nazwisko) as pracownik,
timestampdiff(month, pracownik.data_zatrudnienia, curdate()) * pracownik.pensja as suma_wyplat
from pracownik
order by suma_wyplat desc
```
