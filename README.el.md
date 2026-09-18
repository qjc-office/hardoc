# HarDoc

![Κόμικ banner του HarDoc](assets/hardoc-hero.png)

> HarDoc! Your harness is dumb right now. Fix it now!

Το HarDoc ελέγχει μόνο για ανάγνωση το harness των Claude Code και Codex. Εντοπίζει διπλές ή αντικρουόμενες οδηγίες που κάνουν τον βοηθό να επιλέγει λάθος skill.

[English](README.md) · [한국어](README.ko.md) · [All language pages](README.md#read-hardoc-in-your-language)

## Εγκατάσταση για Claude Code

Εκτελέστε αυτές τις δύο εντολές μία φορά:

```bash
claude plugin marketplace add https://github.com/qjc-office/hardoc
claude plugin install hardoc@hardoc-marketplace
```

## Χρήση στο Claude Code

Ανοίξτε νέα συνεδρία Claude Code και εκτελέστε:

```text
/skill-governor audit .
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

Το HarDoc λειτουργεί μόνο για ανάγνωση. Δεν διαγράφει, απενεργοποιεί, εγκαθιστά ή τροποποιεί ρυθμίσεις harness και δεν διορθώνει αυτόματα αποτελέσματα doctor. Ελέγξτε τις προτάσεις πριν από κάθε αλλαγή.

Για τον πλήρη οδηγό και την αξιολόγηση δείτε το [English README](README.md).
