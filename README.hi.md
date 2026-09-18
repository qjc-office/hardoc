# HarDoc

![HarDoc कॉमिक बैनर](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc Claude Code और Codex harness की read-only जाँच करता है। यह दोहराए गए या टकराते निर्देश ढूँढता है, जिनसे सहायक गलत skill चुन सकता है।

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Claude Code के लिए इंस्टॉल करें

इन दोनों कमांड को एक बार चलाएँ:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Claude Code में उपयोग

नया Claude Code session खोलकर चलाएँ:

```text
/skill-governor audit .
```

## Codex में उपयोग

यदि skill Codex में दिखाई दे, तो नया session खोलकर चलाएँ:

```text
$skill-governor audit .
```

## HarDoc क्या जाँचता है

HarDoc पहले project directory जाँचता है, फिर CLI version देखता है और हर runtime का native doctor चलाने का प्रयास करता है।

- `claude doctor`: Claude Code installation की स्थिति जाँचता है।
- `codex doctor`: Codex installation की स्थिति जाँचता है।
- `audit`: skills, MCP, plugins, rules, hooks, agents और वास्तविक उपयोग के प्रमाण जाँचता है।

## सुरक्षा सीमाएँ

HarDoc read-only है। यह harness configuration को हटाता, बंद करता, इंस्टॉल या बदलता नहीं है और doctor परिणामों को अपने-आप ठीक नहीं करता। बदलाव से पहले प्रस्ताव देखें।

पूरी जानकारी और evaluation के लिए [English README](README.md) देखें।
