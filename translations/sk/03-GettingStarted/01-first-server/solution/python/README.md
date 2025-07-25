<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "d0f0d7012325b286e4a717791b23ae7e",
  "translation_date": "2025-07-09T23:14:43+00:00",
  "source_file": "03-GettingStarted/01-first-server/solution/python/README.md",
  "language_code": "sk"
}
-->
# Spustenie tohto príkladu

Odporúča sa nainštalovať `uv`, ale nie je to povinné, pozrite si [návod](https://docs.astral.sh/uv/#highlights)

## -0- Vytvorte virtuálne prostredie

```bash
python -m venv venv
```

## -1- Aktivujte virtuálne prostredie

```bash
venv\Scrips\activate
```

## -2- Nainštalujte závislosti

```bash
pip install "mcp[cli]"
```

## -3- Spustite príklad

```bash
mcp run server.py
```

## -4- Otestujte príklad

Keď máte server spustený v jednom termináli, otvorte ďalší terminál a spustite nasledujúci príkaz:

```bash
mcp dev server.py
```

Týmto by sa mal spustiť webový server s vizuálnym rozhraním, ktoré vám umožní otestovať príklad.

Keď je server pripojený:

- skúste zobraziť zoznam nástrojov a spustiť `add` s argumentmi 2 a 4, výsledok by mal byť 6.

- prejdite na resources a resource template a zavolajte get_greeting, zadajte meno a mali by ste vidieť pozdrav s menom, ktoré ste zadali.

### Testovanie v CLI režime

Inspector, ktorý ste spustili, je vlastne Node.js aplikácia a `mcp dev` je jej obal.

Môžete ho spustiť priamo v CLI režime pomocou nasledujúceho príkazu:

```bash
npx @modelcontextprotocol/inspector --cli mcp run server.py --method tools/list
```

Týmto sa zobrazia všetky nástroje dostupné na serveri. Mali by ste vidieť nasledujúci výstup:

```text
{
  "tools": [
    {
      "name": "add",
      "description": "Add two numbers",
      "inputSchema": {
        "type": "object",
        "properties": {
          "a": {
            "title": "A",
            "type": "integer"
          },
          "b": {
            "title": "B",
            "type": "integer"
          }
        },
        "required": [
          "a",
          "b"
        ],
        "title": "addArguments"
      }
    }
  ]
}
```

Na vyvolanie nástroja zadajte:

```bash
npx @modelcontextprotocol/inspector --cli mcp run server.py --method tools/call --tool-name add --tool-arg a=1 --tool-arg b=2
```

Mali by ste vidieť nasledujúci výstup:

```text
{
  "content": [
    {
      "type": "text",
      "text": "3"
    }
  ],
  "isError": false
}
```

> ![!TIP]
> Zvyčajne je oveľa rýchlejšie spustiť inspector v CLI režime než v prehliadači.
> Viac o inspectore si prečítate [tu](https://github.com/modelcontextprotocol/inspector).

**Vyhlásenie o zodpovednosti**:  
Tento dokument bol preložený pomocou AI prekladateľskej služby [Co-op Translator](https://github.com/Azure/co-op-translator). Aj keď sa snažíme o presnosť, prosím, majte na pamäti, že automatizované preklady môžu obsahovať chyby alebo nepresnosti. Originálny dokument v jeho pôvodnom jazyku by mal byť považovaný za autoritatívny zdroj. Pre kritické informácie sa odporúča profesionálny ľudský preklad. Nie sme zodpovední za akékoľvek nedorozumenia alebo nesprávne interpretácie vyplývajúce z použitia tohto prekladu.