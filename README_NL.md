# Puzzle Idle-privacybeleid publiceren met GitHub Pages

Deze map is direct publiceerbaar. Er staan geen trackers, externe scripts of externe lettertypen in.

## Snelste werkwijze

1. Maak op GitHub een **openbare** repository, bijvoorbeeld `puzzle-idle-privacy`.
2. Upload de inhoud van deze map naar de hoofdmap van de repository:
   - `index.html`
   - `styles.css`
   - `.nojekyll`
3. Open in de repository **Settings → Pages**.
4. Kies bij **Build and deployment**: `Deploy from a branch`.
5. Kies branch `main` en map `/(root)` en klik op **Save**.
6. Wacht tot GitHub de pagina heeft gepubliceerd.
7. De URL wordt normaal:

   `https://JOUW-GITHUB-NAAM.github.io/puzzle-idle-privacy/`

8. Open de URL in een privévenster en controleer dat hij zonder inloggen werkt.
9. Vul exact die HTTPS-URL in:
   - `project.godot` bij `monetization/privacy_policy_url`;
   - Google Play Console bij **App content → Privacy policy**;
   - AdMob bij de privacyberichten voor de app.
10. Voer daarna uit: `python tools/validate_google_play_release.py .`

Verander de tekst wanneer je later analytics, crashrapportage, accounts, cloudsave of andere SDK's toevoegt.
