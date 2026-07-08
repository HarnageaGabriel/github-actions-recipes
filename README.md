# GitHub Actions Recipes

Piccola raccolta di workflow GitHub Actions a supporto di post LinkedIn su CI/CD e FinOps.

Ogni cartella/coppia di workflow isola **una** differenza alla volta, così il confronto si vede nei log di Actions, non solo a parole.

## Demo disponibili

### 1. Dependency caching — quanto costa NON usare la cache

- [`.github/workflows/without-cache.yml`](.github/workflows/without-cache.yml) — installa le dipendenze da zero a ogni run
- [`.github/workflows/with-cache.yml`](.github/workflows/with-cache.yml) — usa `actions/setup-node` con `cache: 'npm'`

Entrambi loggano il tempo di install come annotazione nel job, così il confronto si vede direttamente nei log di Actions.

**Perché conta:** GitHub Actions fattura i minuti di esecuzione. Ogni minuto risparmiato in cache è un minuto di runner non pagato, oltre a un feedback loop più veloce per chi sviluppa.

Numeri di riferimento (fonti in fondo):
- Caching corretto riduce tipicamente i tempi di build del **40-80%**, a seconda dello stack
- Un caso reale documentato: pipeline Node.js passata da **14 minuti a ~1:45**, con una **riduzione dell'87% dei minuti di CI/CD consumati** a parità di push giornalieri
- Attenzione al limite di storage: **10GB di cache per repository**, con eviction automatica dopo **7 giorni** di inattività — su progetti piccoli con install sotto i 30 secondi, la cache può anche non convenire (overhead di save/restore)

**Come riprodurlo:**
1. Vai su **Actions** → esegui manualmente entrambi i workflow (`workflow_dispatch`)
2. Confronta il tempo di install nei log dei due run
3. Rilancia il workflow "con cache" una seconda volta: la differenza si vede meglio dal secondo run in poi (il primo run popola la cache)

Cosa cambia in pratica tra i due file:

```diff
  - name: Setup Node.js
    uses: actions/setup-node@v4
    with:
      node-version: '20'
+     cache: 'npm'
+     cache-dependency-path: package.json
```

Una riga (due, per il path della cache key). È spesso tutto quello che serve per iniziare.

---

Altre demo verranno aggiunte qui nel tempo, ognuna con la propria coppia di workflow "prima/dopo".

## Fonti

- [actions/cache — repository ufficiale](https://github.com/actions/cache)
- [GitHub Docs — Dependency caching reference](https://docs.github.com/en/actions/reference/workflows-and-actions/dependency-caching)
- [CICube — GitHub Actions Cache: A Complete Guide](https://cicube.io/blog/github-actions-cache/)
- [ZeonEdge — Why your GitHub Actions CI/CD is 10x slower than it should be](https://zeonedge.com/blog/github-actions-slow-cicd-caching-strategies)

---
Gabriel Harnagea · [linkedin.com/in/gabriel-harnagea](https://www.linkedin.com/in/gabriel-harnagea)
