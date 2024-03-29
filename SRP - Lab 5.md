# SRP - Lab 5

**Brze vs spore kriptografske *hash* funkcije**

Kod koji smo unijeli u .py datoteku smo imali unaprijed zadan. Datoteku

```
requirements.txt
```

koja ima popis paketa potrebnih za kod smo instalirali s naredbom

```
pip install -r requirements.txt
```

.
Izvršeni kod nam je u terminalu prikazao tablice s vremenima izvršavanja nekoliko algoritama (AES, HASH_MD5, HASH_SHA256, HASH_SHA512). AES je česta funkcija i izvršava se vrlo brzo, dok su od nje brže SHA funkcije i MD5. Kasnije smo isprobali i Linux CRYPT koja je dosta sporija funkcija od prethodno navedenih. Zaporke provlačimo kroz hash funkcije zbog svojstva jednosmjernosti (one-wayness), napadači otežano dolaze do lozinki.

 I**mplementacija jednostavnog sustava autentikacije korisnika**

Pomoću funkcije Argon2 smo implementirali proces inicijalne registracije i login korisnika. Napisan je bio kod koji generira 3 opcije: registraciju, prijavu i izlaz iz programa. Odabirom željene opcije, program bi dalje postupao onako kako treba. Za pohranu informacija o korisniku, koristili smo

*SQLite* bazu. Funkcija

```
register_user()
```

bi kreirala tablicu i u nju unijela korisničko ime i lozinku (hashirana pomoću Argon2). Za primjer smo unosili neke korisnike s istom zaporkom te smo mogli vidjeti pomoću

*SQLite Viewer*

- a da njihove hash vrijednosti zaporki nisu iste. To je tako zbog korištenja soli. Ukoliko su im imena bila ista, kreiranje drugog korisničkog računa nije bilo moguće. Dakle, zaporka ne mora biti jedinstvena, ali korisničko ime mora.
Nadalje, slijedi prijava. Upisuju se korisničko ime i zaporka pomoću kojih je izvršena registracija. Argon2 treba i zaporku i njenu hash vrijednost da bi izvršio usporedbu unesenih i točnih podataka. Tek nakon unosa i imena i zaporke, provjerava se valjanost podataka. Da bi napadaču otežali posao, ukoliko ime ne postoji u bazi ili je zaporka netočna, ispisuje se poruka „Invalid username or password“.