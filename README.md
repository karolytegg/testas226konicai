# bizhub 226: statinės analizės aplinka

Tai tyrimo įrankiai, ne veikiantis spausdintuvo ar skenerio draiveris.

## Kas paruošta

GitHub Actions rankiniu būdu paleidžia Ghidra 11.3.2 Linux serveryje ir eksportuoja funkcijų pseudokodą bei simbolių adresus. Ghidra archyvo SHA-256 tikrinamas pagal oficialų leidimą. Analizuojami failai nepaleidžiami. REA šiame workflow neįdiegtas: naudojamas tiesiogiai jo palaikomas Ghidra variklis.

## Savitikra

Actions → Static driver analysis → Run workflow. Palikite pažymėtą self_test. Analizuojama serverio /bin/true kopija; printerio ir gamintojo failų nereikia. Sėkminga savitikra nepatvirtina suderinamumo su bizhub 226.

## Draiverių analizė

Tik jeigu leidžiama šiuos failus viešinti, įkelkite analizuotinus failus į samples/ ir paleiskite workflow išjungę self_test. Šis repo viešas. Nekelkite įmonės konfigūracijų, IP adresų, žurnalų ar dokumentų. Prieš keliant gamintojo failus reikia išspręsti jų platinimo klausimą; alternatyva yra atskiras leidžiamas saugojimo ir atsisiuntimo mechanizmas.

Leidžiami failai: AR226.DS, ARWT.dll, WSD226.dll, ARG.dll, ARGe.dll, ARGmon.dll, ARGppr.dll, SetupScan.dll. Vieno failo limitas 20 MiB.

Rezultatai: Actions paleidimo Artifacts → static-analysis-<run_id>. Manifestas turi failų SHA-256. Kiekvienam moduliui kuriami decompiled.c ir symbols.tsv. Artefaktai laikomi 7 dienas. Dalinė analizė ir funkcijų dekompiliavimo klaidos galimos net sėkmingame job; tikrinkite žurnalą ir DECOMPILATION FAILED žymas.

## Tyrimo prioritetai

1. AR226.DS: DAT_CAPS klaidos kelias, IP konfigūracijos skaitymas ir rašymas.
2. WSD226.dll: tinklo skenavimo sąsajos.
3. ARGe.dll, ARGmon.dll ir ARGppr.dll: atvaizdavimo formatas, ryšio ir spausdinimo eilės logika.

Pseudokodas nėra originalus išeities kodas ar paruoštas atvirojo kodo pakaitalas. Paketų savybės nepatvirtina konkretaus aparato funkcijų. Naują realizaciją reikės atskirai projektuoti ir bandyti su aparatu leistinoje aplinkoje.
