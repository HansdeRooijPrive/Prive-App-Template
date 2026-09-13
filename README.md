# Prive-App-Template

Sjabloon (GitHub *template repository*) voor een **privé** web-app op het
OTAP-platform. Een nieuwe app maak je door van deze repo een nieuwe repo te
genereren (`Prive-<App>`). De CI/CD én de bouwstap komen centraal uit
[`OTAP-CI`](https://github.com/HansdeRooijPrive/OTAP-CI) (versie `v2`); zie daar
de platformafspraken en alle placeholders.

## Snel starten
```bash
python build.py            # bouwt index.html (productie); haalt eenmalig OTAP-CI op in .otap/
python build.py --env=test # testvariant (andere naam, icoon en opslagsleutel)
python build.py --check    # platformafspraken + index.html controleren
# lokaal bekijken: open index.html of serveer de map
pip install -r requirements-test.txt && python -m playwright install chromium && pytest
```

## Wat pas je aan per app
- **`app.json`** — naam, `short_name`, `storage_key` en de kleuren per omgeving (prod/acc/test). De kleuren kies je zelf.
- **`src/icons/icon.<prod|acc|test>.png`** — je eigen app-icoon per omgeving. Vorm en kleur kies je zelf; de drie moeten wél van elkaar verschillen, bij voorkeur in kleur. De meegeleverde iconen zijn alleen een startpunt.
- **`src/`** — de app zelf: `index.template.html`, `styles.css`, `app/NN-*.js`, optioneel `src/vendor/*.js`.
- **`tests/`** — je eigen tests (optioneel; deze demo bevat een build- en smoke-test).

`build.py` is een dunne ingang naar de centrale bouwstap; die pas je niet aan.
De naam per omgeving (" acc", " test") en de opslagsleutels regelt het platform.

## OTAP
| Branch | Omgeving | URL |
|--------|----------|-----|
| `main` | Productie | `…github.io/<repo>/` |
| `acceptatie` | Acceptatie | `…github.io/<repo>/acceptatie/` |
| `development` | Test | `…github.io/<repo>/test/` |

`index.html` (productie-build) staat ingecheckt; `CI` bewaakt dat die overeenkomt
met `src/`. Push naar een branch → `OTAP-CI` bouwt en publiceert de bijbehorende
omgeving.
