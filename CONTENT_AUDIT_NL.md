# Kritische inhoudscontrole — Minesweeper Idle privacybeleid
Datum: 21 oktober 2026

## Scope

De openbare website is vergeleken met de op 21 oktober beschikbare
broncode in `davidvdw02/PuzzleIdle`, met name:
`project.godot`, `scripts/telemetry/TelemetryService.gd`,
`scripts/telemetry/MonetizationTelemetryService.gd`,
`scripts/telemetry/NullAnalyticsProvider.gd`,
`scripts/monetization/AdConsentService.gd`,
`scripts/monetization/RewardedAdService.gd`,
`scripts/config/PurchaseProductConfig.gd`,
`scripts/commerce/GooglePlayBillingProvider.gd` en
`scripts/ui/controllers/SettingsController.gd`.

Dit is een **broncode- en beleidsreview**, geen volledige inspectie van een
daadwerkelijke ondertekende APK/AAB of juridisch advies.

## Gecorrigeerde feitelijke problemen

| Oude website | Bevinding | Nieuwe tekst |
|---|---|---|
| Naam `Puzzle Idle` | Play Store-naam en Godot-appnaam zijn `Minesweeper Idle` | Alle zichtbare paginatitels en beleidsteksten hernoemd |
| "Limited interstitial ads" | Er bestaat een interstitial in het AdMob-account, maar de game gebruikt deze niet | Uitsluitend vrijwillige rewarded advertenties; geen geforceerde interstitial |
| Eén product "Puzzle Idle Supporter" | Drie éénmalige producten in de code, waaronder Premium 2× offline zonder video | Premium Miner, Supporter Pack, Deep Miner Cosmetics met correcte functies |
| "Settings → Privacy & ad choices" werkt | Native AdMob-plugin mist `show_privacy_options_form`; live-ad-gate is afgesloten | Status wordt eerlijk vermeld, geen valse belofte |
| "Geen analytics" zonder nuance | Er is lokale gameplay- en monetisatietelemetrie, maar huidige externe provider is `NullAnalyticsProvider` | Lokale statistieken concreet benoemd en van Google SDK-verwerking onderscheiden |
| Oude vaste claim "13+" | Actuele leeftijdsdoelgroep en contentclassificatie in Play Console nog niet bevestigd | Geen ongefundeerde leeftijdsgrens genoemd; Play-doelgroep blijft te bepalen |
| Absolute verwijder- of gegevensclaims | Progressie-reset kan rechten of losse statistiekbestanden bewaren; Android-back-ups bestaan | Android-appopslag wissen en beperkingen van reset/back-up verduidelijkt |
| Privacykeuzes bij Google niet gespecificeerd | AdMob kan IP, identificatoren, interacties en diagnoses verwerken | Concreet in beide talen beschreven |
| Nederlands eerst | Play Store wordt Engelstalig | Engels standaard, toegankelijke EN/NL-slider, geen cookies of tracking |

## Wat nog moet gebeuren voordat de app gepubliceerd wordt

1. **Privacybeleid bereikbaar vanuit de game (blokker).** In de onderzochte
   Godot-UI is geen duidelijke link naar deze privacywebsite gevonden.
   Google Play vereist een beleid zowel in Play Console **als binnen de app**.
   Voeg een zichtbare, werkende "Privacy Policy"-link aan Settings toe.
   Mogelijk kan een native browser of `OS.shell_open` hiervoor gebruikt
   worden, maar controleer de Android-functionaliteit eerst.

2. **UMP privacykeuzes (blokker voor live advertenties).**
   `addons/AdmobPlugin/Admob.gd` ondersteunt de vereiste native knop om
   privacykeuzes opnieuw te openen nog niet. Dit probleem wordt in het
   hoofdproject bewust met een fail-closed live-advertentiegate behandeld.
   Upgrade de gekoppelde GDScript-wrapper én native AAR; controleer alle
   scenario's op een Android-toestel en pas de policytekst daarna aan.

3. **Data safety (blokker tot verificatie).** Laat de definitieve Google Play
   Data safety-vragen overeenkomen met het gebouwde AAB. Beoordeel
   AdMob/UMP/Billing SDK-versies en permissies, waaronder Advertising ID,
   diagnostiek, advertentie-interacties, IP/benaderde locatie en eventueel
   ingeschakelde Android-back-up. Beantwoord niet automatisch "no data
   collected" omdat game-telemetrie zelf lokaal is.

4. **Leeftijd / doelgroep.** Kies werkelijk bedoelde leeftijdsgroepen en
   content rating in Play Console. Alleen dan kunnen leeftijdsclaims
   en eventueel Google's Families-richtlijnen worden beoordeeld.

5. **Geldige identiteit en supportadres.** De developernaam
   `David van der Wulp` en `puzzleidlegame@gmail.com` zijn overgenomen
   uit de vorige openbare site. De eigenaar moet controleren dat het
   contactadres bereikbaar is en overeenkomt met de publicatie-identiteit.

6. **Betaalde aankopen.** Play-producten moeten nog worden aangemaakt en
   geactiveerd. Het huidige aankoopproces gebruikt on-device aankoopstatus
   en acknowledgements maar geen eigen servercontrole op tokens/refunds.
   Dit is een beveiligings- en publicatiepunt voor de game, niet iets
   dat alleen met een privacytekst opgelost wordt.

7. **Website bij nieuwe release actualiseren.** De huidige privacytekst
   zegt terecht dat live AdMob-advertenties nog geblokkeerd zijn.
   Als die later wel live gaan, vervalt dat deel en moet het beleid
   inhoudelijk tegelijk met de daadwerkelijke SDK-werking worden aangepast.

## Toegankelijkheid en website

- `lang="en"` en Engelse zichtbare inhoud zonder JavaScript.
- Een EN/NL-schuifschakelaar is toetsenbordbedienbaar via een native checkbox.
- Verborgen NL-artikel staat met `hidden` uit, zodat het niet dubbel wordt
  voorgelezen; na schakelen verandert ook de HTML-taal.
- `?lang=nl` is een deelbare Nederlandse link.
- Geen tracking-/cookiecode of externe scripts/lettertypen.

## Gecontroleerde officiële richtlijnen

- Google Play User data / Privacy Policy:
  https://support.google.com/googleplay/android-developer/answer/10144311
- Google Mobile Ads (Android) Google Play Data safety disclosure:
  https://developers.google.com/admob/android/privacy/play-data-disclosure
- Google UMP / EU consent and revocation:
  https://developers.google.com/admob/android/privacy/gdpr

**Conclusie:** De openbare beleidstekst is inhoudelijk aanzienlijk
correcter en transparanter, maar **de Android-app is nog niet klaar om als
privacy-compliant productiebuild te worden aangemerkt**. De nog openstaande
punten staan expliciet hierboven en worden niet stilzwijgend goedgekeurd.
