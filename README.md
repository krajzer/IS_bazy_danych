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
# zadanie 1
create table pracownik (
id int auto_increment primary key,
imie varchar(50) not null,
nazwisko varchar(100) not null,
data_urodzenia date,
stanowisko enum ('sprzedawca', 'magazynier', 'księgowa')
);
```

**Zadanie 2**
# Zadanie 2
INSERT INTO pracownik(id, imie, nazwisko, data_urodzenia, stanowisko) values
(default, 'Jan', 'Kowalski', '1990-10-10', 'magazynier'),
(default, 'Konrad', 'Rajzer', '1987-07-06', 'sprzedawca'),
(default, 'Anna', 'Biernat', '1995-02-08', 'księgowa');

###Stwórz tabelę dzial z kolumnami:

#id - liczba, autonumer, klucz główny
#nazwa - tekst, max. 255 znaków

#Zadanie 3

create table dzial(
id int auto_increment primary key,
nazwa varchar(255)
);

#Zadanie 4

ALTER TABLE dzial
ADD sprzedaz VARCHAR(50),
ADD ksiegowosc VARCHAR(50),
ADD magazyn VARCHAR(50);

#Zadanie 5
alter table pracownik modify stanowisko varchar(50) default 'sprzedawca';


#Zadanie 6
#7 pozycji z czego 2 po przecinku
alter table pracownik add column pensja decimal(7,2);

#Zadanie 7

Alter table dzial RENAME COLUMN nazwa TO nazwa_dzialu;
alter table dzial rename column id TO id_dzialu;
alter table pracownik rename column id to id_pracownika;

#Zadanie 8
Select * from pracownik;

delete from pracownik where id_pracownika = 3;



#Zadanie 1

alter table pracownik
add column dzial int(50),
add constraint fk_dzial
foreign key (dzial) references dzial(id_dzialu)
on delete restrict;


#zadanie 2

create table stanowisko(
id_stanowiska int(100) auto_increment primary key,
nazwa_stanowiska varchar(50)
);

#zadanie 3

#można po value(default, 'kierowca')
insert into stanowisko value(1,'kierowca');
insert into stanowisko value(2, 'montażysta');

select * from stanowisko


