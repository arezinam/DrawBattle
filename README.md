# DrawBattle – Real-time takmičenje u crtanju

**Ocena:** 10 (potencijalno diplomski rad)

## Opis igre / Gameplay

DrawBattle je real-time igra crtanja u kojoj se svi igrači takmiče na istu temu.  

- Svakom igraču je dodeljena ista tema crteža za određeni vremenski period.  
- Igrači crtaju koristeći online Canvas alat u realnom vremenu.  
- Nakon isteka vremena za crtanje, sledi **faza rangiranja**:  
  - Svi igrači ocenjaju crteže drugih igrača.  
  - Crteži su anonimni – igrači ne znaju ko je nacrtao koji rad.  
- Na osnovu datih ocena formira se rang lista za rundu.  
- Igra podržava **team battles** (timovi crtaju zajedno protiv drugih timova), galeriju crteža, achievements i notifikacije.  

Cilj igre je kombinacija kreativnosti, brzine i strategije u ocenjivanju crteža drugih igrača.

## Opis problema

Postojeće online igre crtanja (npr. Skribbl.io) imaju ograničenu funkcionalnost, loš UX i minimalnu socijalnu interakciju. Cilj projekta je razvoj **real-time platforme za crtanje i takmičenje**, sa naglaskom na interaktivnost, timske mečeve, rangiranje korisnika i gamifikaciju.

Projekat rešava sledeće probleme:  
- Nedostatak real-time performansi i skalabilnosti u postojećim igrama.  
- Ograničena socijalna interakcija i povratna informacija od publike.  
- Nema trajnog praćenja postignuća i najboljih crteža.  
- Nedostatak timskog takmičenja i periodičnih turnira.

## Cilj projekta

- Omogućiti korisnicima da crtaju i takmiče se u realnom vremenu.  
- Timski mečevi i takmičenja između korisnika i timova.  
- Evidencija rang lista, achievements i najboljih crteža.  
- Administrator ima kontrolu nad korisnicima, turnirima i moderacijom sadržaja.  

## Uloge korisnika

**Neulogovani korisnici:**  
- Mogu da učestvuju u javnim mečevima, ali:  
  - Nemaju pristup istoriji mečeva.  
  - Nemaju mogućnost čuvanja svojih crteža.  
  - Ne učestvuju u rang listama.
- Mogu da pregledaju forum, ali ne mogu da postavljaju niti komentarišu sadržaj.  
- Mogu da pregledaju javnu galeriju crteža drugih korisnika.  

**Registrovani korisnici:**  
- Mogu da kreiraju i učestvuju u mečevima i timovima.  
- Deo su **nedeljne rang liste** i dobijaju achievements za svoja postignuća.  
- Imaju sopstveni profil gde mogu da postave do **5 svojih najboljih crteža**.  
- Mogu da postavljaju i komentarišu sadržaj na forumu.  
- Imaju pristup **turnirima** i specijalnim događajima.  
- Primaju notifikacije i podsetnike za zakazane mečeve, turnire i osvojene nagrade.  

**Administrator:**  
- Moderacija sadržaja i korisnika (banovanje, uklanjanje uvredljivog sadržaja).  
- Kreiranje i upravljanje turnirima.  
- Kontrola rang listi i rezultata.  
- Pregled statistika i aktivnosti korisnika.  


## Funkcionalnosti MVP-a

1. **Registracija i login korisnika** – kreiranje naloga sa osnovnim podacima i login sistem.  
2. **Kreiranje i učestvovanje u mečevima**  
   - Registrovani korisnici mogu da kreiraju privatne ili timske mečeve, pozivaju druge igrače i organizuju timske duele.  
   - Neregistrovani korisnici mogu da se priključe samo javnim mečevima, bez mogućnosti kreiranja i organizovanja.  
3. **Real-time crtanje** – WebSocket server omogućava sinhrono crtanje svih igrača u okviru meča.  
4. **Rang liste i achievements** – registrovani korisnici se nalaze na nedeljnim rang listama i osvajaju nagrade/bedževe.  
5. **Galerija korisnika** – svaki registrovani korisnik može da postavi do 5 svojih najboljih crteža na profil.  
6. **Forum** – pregled dostupan svima, ali postavljanje i komentarisanje samo registrovanim korisnicima.  
7. **Report/Commend sistem** – korisnici mogu da prijave uvredljiv sadržaj ili ponašanje (chat, crteže, forume). Administratori imaju uvid u prijave i istoriju aktivnosti, i mogu da sankcionišu korisnike. Takođe, korisnici mogu da pohvale (commend) druge, što utiče na njihov ugled u zajednici.
8. **Notifikacije i reminderi** – sistem obaveštava korisnike o predstojećim mečevima, turnirima i osvojenim nagradama.  
9. **Administracija i moderacija** – administratori imaju alate za upravljanje korisnicima, turnirima i forumom.  

## Funkcionalnosti za diplomski rad

- Spectator mode i spectator voting. U specijalnim turnirima, radove korisnika ocenjuju spectatori tog turnira, a ne oni koji su crtali.  
- Skalabilna multi-server arhitektura za veliki broj igrača.  
- Napredni alati za crtanje (layers, undo/redo, različite boje i debljine linije).  
- Periodični turniri sa nagradama i leaderboard-ima.  
- Push notifikacije i reminderi unapređeni za spectator događaje.  

## Arhitektura

### Backend (Rust)
- **Actix Web / Axum** za REST API i WebSocket server.  
- **Tokio runtime** za asinhroni rad i low-latency komunikaciju.  
- **Event-driven system** za crtanje, notifikacije i leaderboard update.  

### Baze podataka
- **PostgreSQL** za korisnike, rang liste, mečeve i galeriju.  
- **Redis / MongoDB** za real-time chat, forum i notifikacije.  

### Frontend
- **React / Vue / Svelte** za interaktivni web UI.  
- **Canvas API** za crtanje.  
- WebSocket konekcija za real-time crtanje i update.

### Storage
- Cloud (S3 ili slično) za čuvanje crteža.  