# Politi Tablet — dokumentation

Dokumentationssite for **Politi Tablet** (`va_policemdt`), en politi-MDT til
FiveM-servere på ESX. Bygget på [Mintlify](https://mintlify.com).

Indholdet er skrevet til **serverejere og scriptudviklere** der skal integrere
med ressourcen — ikke til betjentene der bruger tabletten i spillet.

## Struktur

| Sti | Indhold |
| --- | --- |
| `index.mdx` | Forside |
| `quickstart.mdx` | Fra ingenting til første export-kald |
| `api-reference/` | Alle exports, opdelt pr. domæne |
| `guides/recipes.mdx` | Færdige integrationseksempler |
| `docs.json` | Konfiguration og navigation |
| `AGENTS.md` | Skrivekonventioner — læs den før du tilføjer sider |

En ny side skal tilføjes i `docs.json` under `navigation`, ellers vises den ikke.

## Lokal udvikling

```bash
npm i -g mint
mint dev
```

Kør kommandoen i mappen med `docs.json`. Forhåndsvisningen ligger på
`http://localhost:3000`.

## Udgivelse

Ændringer udgives automatisk, når de pushes til standardgrenen, forudsat at
Mintlifys GitHub-app er installeret fra
[dashboardet](https://dashboard.mintlify.com/settings/organization/github-app).

## Fejlfinding

- Siden loader som 404 — tjek at du kører i mappen med `docs.json`, og at siden
  er registreret i `navigation`
- Dev-serveren vil ikke starte — kør `mint update` for nyeste CLI
