# HarDoc

![HarDoc कॉमिक बैनर](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

HarDoc आपके Claude Code और Codex हार्नेस की जाँच करता है। यह पहले रिपोर्ट देता है और सेटिंग तभी बदलता है जब आप मंज़ूरी देते हैं।

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Claude Code के लिए इंस्टॉल करें

इन दोनों कमांड को एक बार चलाएँ:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Codex में लोकल इंस्टॉल

Codex में skill सीधे इंस्टॉल करने के लिए रिपॉज़िटरी क्लोन करें और अपने लोकल skills फ़ोल्डर में लिंक बनाएँ:

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
ln -sfn "$PWD/plugin/skills/trim" "$CODEX_SKILLS_DIR/trim"
```

## Claude Code में उपयोग

नया Claude Code session खोलकर चलाएँ:

```text
/skill-governor audit .
```

रिपोर्ट पर कार्रवाई करने के लिए, सफ़ाई का पूर्वावलोकन देखें:

```text
/trim --dry-run
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

आपकी मंज़ूरी के बिना HarDoc कुछ नहीं बदलता। `skill-governor` स्किल केवल पढ़ती है। `trim` स्किल बदलाव तभी लागू करती है जब आप पूर्वावलोकन को मंज़ूरी देते हैं; वह पहले स्नैपशॉट लेती है और वापस लौटने के लिए एक कमांड दिखाती है।

पूरी जानकारी और evaluation के लिए [English README](README.md) देखें।
