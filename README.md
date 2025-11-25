# pengeflyt-pdfgen
`pengeflyt-pdfgen` er en applikasjon som genererer PDF-filer for applikasjoner til team pengeflyt.
Per nå er det kun `sokos-oppgjorsrapporter` som benytte seg av det.
I forbindelse med `sokos-oppgjorsrapporter`, PDF-filene kommer til å bli brukt i Altinn, i en arbeidsflate i Utbetalingsportalen og i nav.no i en side for arbeidsgivere.


## Overordnet bilde av applikasjonen

Applikasjonen støtter kun `POST`-kall til spesifikke endepunkter. For bruk i teamet er dette endepunktet
`/api/v1/genpdf/oppgjorsrapporter/<rapporttype>`. Applikasjonen leter da etter `rapporttype.hbs` inne i
`templates/oppgjorsrapporter/`. Dette er en [Handlebars](https://handlebarsjs.com/)-malfil som brukes til å generere HTML
som deretter brukes for å generere en PDF. For effektiv bruk av applikasjonen må `POST`-kallet ha en JSON-payload
som har feltene som brukes i malen.

Ved lokal utvikling kan hjelpeskriptet `run_development.sh` kjøres. Det er forutsatt at maskinen du kjører det på
har Docker installert. I en typisk utviklingssituasjon vil man endre på malfiler i `templates` og mockdata i `data`,
effekten av endringer der kan ses ved å gjøre et GET-kall til URL-en som man i produksjon vil gjøre `POST`-kall til.

Når man har kjørt `run_development.sh` kan man for eksempel gå til
[http://localhost:8080/api/v1/genpdf/oppgjorsrapporter/refusjon_arbeidsgiver](http://localhost:8080/api/v1/genpdf/oppgjorsrapporter/refusjon_arbeidsgiver) for å se hva kombinasjonen av
`templates/oppgjorsrapporter/refusjon_arbeidsgiver.hbs` og `data/oppgjorsrapporter/refusjon_arbeidsgiver.json` resulterer i. Man trenger ikke å
restarte `run_development.sh` når man har gjort endringer, en enkel refresh av siden vil vise resultatet av endringene.
