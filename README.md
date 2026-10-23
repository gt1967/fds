# FdS Adesso Vicino

Una pagina web da usare sul telefono durante FdS 2026 a Genova (22 ottobre – 1 novembre):
premi un tasto e vedi gli eventi che iniziano **nei prossimi minuti**, ordinati per
**tempo a piedi** da dove sei.

**Apri l'app:** https://gt1967.github.io/fds/

## Cosa fa

- Mostra conferenze, laboratori, mostre, spettacoli ed eventi speciali in partenza nei prossimi 15–120 minuti.
- Li ordina per minuti a piedi dalla tua posizione (GPS) o da una sede scelta dall'elenco.
- Dice se arrivi in tempo: verde con margine, giallo al limite, rosso in ritardo.
- Filtra per **interessi** (13 aree, da Robotica e IA a Scienze sociali), **età**, **tipo di evento** e parola cercata.
- Per i laboratori calcola il prossimo turno disponibile.
- Per ogni evento: orari, relatori, ingresso e prenotazione, temi, indirizzo, "Portami lì" (Google Maps a piedi) e il link alla descrizione completa sul sito ufficiale.
- Vista **Mappa** (OpenStreetMap): la tua posizione e le sedi con eventi nei prossimi minuti; tocca un pallino per vedere gli eventi di quella sede e aprirne i dettagli. La mappa richiede la connessione internet.
- Le preferenze restano salvate sul telefono; i dati sono inclusi nella pagina, quindi funziona anche con poca rete.

## Come usarla dal telefono

1. Apri https://gt1967.github.io/fds/ con il browser del telefono.
2. Consenti la posizione quando richiesto (oppure scegli la sede più vicina in "Dove sono").
3. Dal menu del browser scegli **Aggiungi a schermata Home**: si apre come un'app.

Puoi anche scaricare `index.html` e aprirlo direttamente: funziona senza server, ma in quel caso
il GPS di solito non è disponibile e la posizione si sceglie dall'elenco.

## Dati in diretta (facoltativo, su un tuo server)

La pagina contiene una copia dei dati. Se la pubblichi su un tuo server, può leggere gli orari
aggiornati dal sito ufficiale tramite un inoltro Nginx sullo stesso dominio
(il sito non consente chiamate dirette da altri domini):

```nginx
location /fds/ {
    proxy_pass https://www.festivalscienza.it/;
    proxy_set_header Host www.festivalscienza.it;
    proxy_ssl_server_name on;
}
```

All'avvio la pagina prova `./fds/api/search`; se risponde usa i dati in diretta, altrimenti la copia inclusa.

## Note

- I tempi a piedi sono stime: distanza in linea d'aria × 1,35 a 4,5 km/h.
- I turni dei laboratori vengono dal programma stampato e possono cambiare: in caso di dubbio vale il sito ufficiale.
- Progetto personale e non ufficiale, senza legami con l'organizzazione dell'evento.

## Licenza e dati

Il **codice** è rilasciato con licenza [MIT](LICENSE). La mappa usa [Leaflet](https://leafletjs.com) e i dati © [OpenStreetMap contributors](https://www.openstreetmap.org/copyright).

I **dati** inclusi nella pagina (titoli, orari, sedi, coordinate, fasce d'età) sono pubblicati
dall'organizzazione dell'evento e restano di sua titolarità: questo repository non concede
alcun diritto su di essi. Le descrizioni degli eventi non sono incluse: si leggono sul sito ufficiale
tramite il link di ogni evento.
