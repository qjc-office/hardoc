# HarDoc

![Κόμικ banner του HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

Το HarDoc ελέγχει το harness του Claude Code και του Codex. Πρώτα αναφέρει και αλλάζει ρυθμίσεις μόνο αφού το εγκρίνεις.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Εγκατάσταση για Claude Code

Εκτελέστε αυτές τις δύο εντολές μία φορά:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Τοπική εγκατάσταση στο Codex

Για να εγκαταστήσετε απευθείας το skill στο Codex, κλωνοποιήστε το αποθετήριο και δημιουργήστε έναν σύνδεσμο στον τοπικό φάκελο skills:

```bash
git clone https://github.com/qjc-office/hardoc.git
cd hardoc
CODEX_SKILLS_DIR="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$CODEX_SKILLS_DIR"
ln -sfn "$PWD/plugin/skills/skill-governor" "$CODEX_SKILLS_DIR/skill-governor"
ln -sfn "$PWD/plugin/skills/trim" "$CODEX_SKILLS_DIR/trim"
```

## Χρήση στο Claude Code

Ανοίξτε νέα συνεδρία Claude Code και εκτελέστε:

```text
/skill-governor audit .
```

Για να δράσεις βάσει της αναφοράς, δες μια προεπισκόπηση του καθαρισμού:

```text
/trim --dry-run
```

## Χρήση με Codex

Αν το skill εμφανίζεται στο Codex, ανοίξτε νέα συνεδρία και εκτελέστε:

```text
$skill-governor audit .
```

## Τι ελέγχει το HarDoc

Το HarDoc ελέγχει πρώτα τον φάκελο του έργου, μετά την έκδοση CLI και επιχειρεί το native doctor κάθε runtime.

- `claude doctor`: Ελέγχει την υγεία της εγκατάστασης Claude Code.
- `codex doctor`: Ελέγχει την υγεία της εγκατάστασης Codex.
- `audit`: Ελέγχει skills, MCP, plugins, rules, hooks, agents και στοιχεία πραγματικής χρήσης.

## Όρια ασφάλειας

Το HarDoc δεν αλλάζει τίποτα χωρίς την έγκρισή σου. Η δεξιότητα `skill-governor` είναι μόνο για ανάγνωση. Η `trim` εφαρμόζει μια αλλαγή μόνο αφού εγκρίνεις μια προεπισκόπηση, κρατά πρώτα στιγμιότυπο και τυπώνει μία εντολή για αναίρεση.

Για τον πλήρη οδηγό και την αξιολόγηση δείτε το [English README](README.md).
