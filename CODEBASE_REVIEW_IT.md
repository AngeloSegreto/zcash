# Revisione del codebase Zcash Docs

## Panoramica del codebase

Questo repository è principalmente un progetto di documentazione basato su **Sphinx + Read the Docs**.

- `README.md` descrive setup e build locale con `make html`.
- `source/conf.py` contiene la configurazione Sphinx (estensioni, tema, path, output).
- `source/index.rst` è la root della documentazione pubblicata.
- `source/rtd_pages/` contiene la gran parte dei contenuti utente/dev (guide, protocolli, troubleshooting).
- `source/_extra/` include contenuti statici aggiuntivi (asset e documentazione esterna incorporata).

## Criticità principali individuate

1. **Debt di aggiornamento tecnologico**
   - Nel `README.md` sono presenti riferimenti a versioni/tool datati (es. Python36/macports e pacchetti legacy), che possono creare frizione di onboarding.

2. **Rischio di incoerenza editoriale**
   - Coesistono `.rst` e `.md` con stili differenti; senza policy di linting forte aumentano refusi, link rotti e terminologia non uniforme.

3. **Superficie contenutistica molto ampia**
   - La directory `source/rtd_pages/` è estesa e tocca temi tecnici/sicurezza: diventa facile introdurre discrepanze tra pagine correlate.

4. **Qualità test/documentation checks non esplicitata**
   - Dal `README.md` emerge il flusso di build, ma non una pipeline minima obbligatoria (es. controllo link, warning-as-errors, spellcheck).

## 4 attività consigliate (mirate)

### 1) Attività refuso (typo)
**Obiettivo:** correggere un refuso evidente in una pagina ad alto traffico (es. `user_guide.rst` o `troubleshooting_guide.rst`).

**Proposta operativa:**
- Cercare stringhe sospette (doppie spaziature, apostrofi errati, parole tronche) con controllo manuale + spellchecker.
- Aprire PR con fix minimale e nota “no semantic change”.

**Definition of Done:**
- Refuso corretto.
- Build docs pulita senza warning nuovi.

### 2) Attività bug (build/docs)
**Obiettivo:** correggere un bug di documentazione trattato come bug funzionale della build (es. riferimento interno non risolto o anchor rotta).

**Proposta operativa:**
- Eseguire build con warning visibili (`make html`), identificare warning riproducibile.
- Correggere target `:ref:`, heading o path asset errato.
- Verificare che warning specifico sparisca.

**Definition of Done:**
- Warning/errore riprodotto e risolto.
- Evidenza nel log di build prima/dopo.

### 3) Attività commento/discrepanza documentazione
**Obiettivo:** allineare una sezione con istruzioni obsolete nel `README.md` rispetto alle dipendenze correnti (es. pacchetti o versioni Python).

**Proposta operativa:**
- Confrontare comandi README con `source/requirements.txt`.
- Aggiornare testo per eliminare mismatch e specificare percorso consigliato unico.

**Definition of Done:**
- Nessuna istruzione contraddittoria tra README e requirements.
- Percorso di setup riproducibile da zero.

### 4) Attività miglioramento test
**Obiettivo:** introdurre un controllo automatico minimo qualità docs in CI locale.

**Proposta operativa:**
- Aggiungere target (o script) per:
  - build Sphinx con warning trattati come errori,
  - controllo link interni,
  - (opzionale) spellcheck su pagine critiche.
- Documentare il comando unico in README.

**Definition of Done:**
- Comando di verifica unico eseguibile localmente.
- Fallimento deterministico in presenza di warning/link rotti.

## Priorità suggerita
1. Discrepanza README/requirements (impatto onboarding immediato)
2. Bug build (stabilità pubblicazione)
3. Test quality gate (prevenzione regressioni)
4. Refusi (igiene continua)
