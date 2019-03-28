# Projekt: Bank
## Datenbankname: Bank

###verwendete Software:

XAMPP Version xyz

XAMPP dient in erster Linie hierfür, um schnell und problemlos einen Testserver zum laufen zu bringen.

Es sollte vermieden werden dieses für einen öffentlichen Server zu verwenden, da er bezüglich der Sicherheit bewusst abgespeckt ist und für solche Zwecke nicht gedacht wurde. 

Beinhaltet: 
* Apache 2.4.38
* MariaDB 10.1.38
* PHP 7.1.27
* phpMyAdmin 4.8.5
* OpenSSL 1.1.1
* XAMPP Control Panel 3.2.2
* Webalizer 2.23-04
* Mercury Mail Transport System 4.63
* FileZilla FTP Server 0.9.41
* Tomcat 7.0.92 (with mod_proxy_ajp as connector)
* Strawberry Perl 5.16.3.1 Portable

MySQL Workbench
Version xyz
MySQL Workbench ist ein Datenbank-Modellierungswerkzeug, das Datenbankdesign, Modellierung, Erstellung und Bearbeitung (Instandhaltung) von MySQL-Datenbanken in eine Umgebung integriert.

PhpStorm 18.03.01 Testversion

PhpStorm ist unsere Wahl. Dabei ist es viel mehr als ein einfacher Text-Editor – PhpStorm hilft bei wiederkehrenden Aufgaben, hat alle Zusammenhänge im Blick und korrigiert unsere Schreibfehler. Ein starkes Werkzeug, das das Entwickeln und Debuggen von Webseiten mit vielen Funktionen unterstützt.

### Testfälle

```sql
select ban_name as Bankname,
       fil_name as Filiale
from bank
left join filialen f on bank.ban_id = f.ban_id
order by Bankname

select * from personen;

select concat_ws(' ', per_fname, per_llname) as "Kunde",
       ban_name as Bank,
       kon_nr as Kontonummer,
       kon_betrag as "Guthaben",
       kre_betrag as Kreditbetrag,
       kre_from as "Kredit von",
       kre_laufzeit as Laufzeit
from person
left join person_has_konto phk on person.per_id = phk.per_id
left join konto k on phk.kon_id = k.kon_id
left join bank b on k.ban_id = b.ban_id
left join person_has_kredit p on person.per_id = p.per_id
left join kredit k2 on p.kre_id = k2.kre_id
order by Kunde;

```

#### Testfall

anlegen einer Bank inkl. Filialen
wenn Bank gelöscht wird werden Filialen mitgelöscht.

```sql
insert into bank (ban_id, ban_name, ban_plz) VALUES (4,'Kreditbank', 1010);

insert into filialen (fil_id, fil_name, fil_plz, fil_telnr, ban_id) VALUES (6,'Filiale Pichl', 5567, '06453', 4);

delete from bank where ban_name like 'Kreditbank';
```

