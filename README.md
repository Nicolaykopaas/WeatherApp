# WeatherApp

En værapplikasjon skrevet i Java med JavaFX. Appen henter sanntids værdata fra [MET (YR) sin åpne API](https://api.met.no/), viser prognosen for valgt sted, genererer værvarsler ved gitte forhold, og lar brukeren lagre favorittlokasjoner til fil.

Utviklet som prosjekt i emnet TDT4100 Objektorientert programmering ved NTNU.

## Funksjonalitet

- Søk opp et sted og se værprognose (temperatur, nedbør, vind)
- Henter sanntidsdata direkte fra MET/YR sin API over HTTP
- Automatiske varsler ved sterk vind, storm, kraftig nedbør og kaldt/vått føre
- Lagre og hente favorittlokasjoner (persisteres til CSV-fil)
- Feilhåndtering for nettverksfeil, filfeil og ugyldig input

## Teknologi

- **Java 21**
- **JavaFX 21** – brukergrensesnitt (FXML + CSS)
- **java.net.http** – HTTP-kall mot MET API
- **JUnit 5** – enhetstester
- **Maven** – bygg og avhengigheter

## Arkitektur

Prosjektet er delt i klasser med tydelig ansvar:

| Klasse | Ansvar |
|---|---|
| `Location` | Representerer et sted (navn, koordinater). Implementerer `Comparable` for sortering av favoritter, med validering av input. |
| `WeatherData` | Holder prognosedata og gjør beregninger (gjennomsnittstemperatur, varmeste time, total nedbør). |
| `WeatherClient` | Henter data fra MET API over HTTP. |
| `AlertService` | Genererer værvarsler basert på definerte terskler for vind, nedbør og temperatur. |
| `FavoriteStorage` | Leser og skriver favorittlokasjoner til CSV-fil. |
| `WeatherController` | Kobler brukergrensesnittet mot logikken. |
| `WeatherApp` | Startpunkt for applikasjonen (JavaFX). |

Logikken i modellklassene er dekket av enhetstester (`WeatherAppTest`).

## Kjøre prosjektet

Krever Java 21 og Maven.

```bash
mvn javafx:run
```

Alternativt kan `WeatherApp.java` (`src/main/java/weatherapp/ui/`) kjøres direkte fra IDE — den inneholder `main`-metoden.

## Kjøre tester

```bash
mvn test
```

## Videre arbeid

- Sammenligne vær mellom flere steder samtidig
- Cache av API-svar for å redusere antall kall
- Push-varsler ved endrede værforhold
