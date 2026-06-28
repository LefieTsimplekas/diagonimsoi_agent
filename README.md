# 📋 Αναλυτής Δημόσιων Διαγωνισμών

Εργαλείο ανάλυσης διακηρύξεων δημόσιων διαγωνισμών με AI. Ανεβάζεις τη διακήρυξη σε PDF και παίρνεις αυτόματα δικαιολογητικά, ημερομηνίες, προϋπολογισμό και έτοιμες υπεύθυνες δηλώσεις.

---

## ✨ Λειτουργίες

- 📄 **Ανάλυση PDF διακήρυξης** — αυτόματη εξαγωγή όλων των στοιχείων
- 📁 **Δικαιολογητικά συμμετοχής** — κατηγοριοποιημένα σε κρίσιμα και τυπικά
- 📅 **Σημαντικές ημερομηνίες** — καταληκτική, αποσφράγιση και άλλες
- 💰 **Προϋπολογισμός** — εκτιμώμενη αξία και στοιχεία αναθέτουσας
- ✍️ **Υπεύθυνες δηλώσεις** — έτοιμες με το standard κείμενο Ν. 1599/1986
- 📅 **Outlook Calendar** — κατέβασε .ics με υπενθυμίσεις 2 μέρες και 1 μέρα πριν
- 💾 **Αποθήκευση Report** — HTML αρχείο με πλήρη μορφοποίηση
- 🖨️ **Εκτύπωση / PDF** — απευθείας από τον browser
- 📊 **Google Sheets** — αυτόματη αποθήκευση κάθε ανάλυσης
- 📧 **Αποστολή Email** — report με emojis και καθαρή δομή

---

## 🏗️ Αρχιτεκτονική

```
Browser (GitHub Pages)
        ↓
Cloudflare Worker (κρύβει το API key)
        ↓
Gemini API (AI ανάλυση)
        ↓
Google Sheets (αποθήκευση)
```

**Fallback λογική στον Worker:**
1. `gemini-2.5-flash-lite` — πρώτη επιλογή (δωρεάν)
2. `gemini-2.5-flash` — αν το πρώτο είναι υπερφορτωμένο
3. `gemini-3-flash` — τελευταία επιλογή

---

## 🚀 Εγκατάσταση

### 1. Cloudflare Worker

1. Πήγαινε στο [dash.cloudflare.com](https://dash.cloudflare.com)
2. Workers & Pages → Create → Worker → Start with Hello World
3. Αντικατάστησε τον κώδικα με τον κώδικα του `worker.js`
4. Settings → Variables and Secrets → Add Secret:
   - Name: `GEMINI_KEY`
   - Value: το Gemini API key σου
5. Deploy

### 2. Gemini API Key

1. Πήγαινε στο [aistudio.google.com/apikey](https://aistudio.google.com/apikey)
2. Create API key → αντίγραψε το key
3. Βάλε το ως Secret στον Cloudflare Worker

### 3. Google Sheets (προαιρετικό)

1. Φτιάξε νέο Google Sheet με επικεφαλίδες:
   `Ημερομηνία | Τίτλος | Αναθέτουσα | Ποσό | Καταληκτική | Δικαιολογητικά | Παρατηρήσεις`
2. Επεκτάσεις → Apps Script → επικόλλησε τον κώδικα του `sheets-script.gs`
3. Deploy → Web app → Anyone → αντίγραψε το URL
4. Βάλε το URL στη μεταβλητή `SHEETS_URL` στο `index.html`

### 4. GitHub Pages

1. Fork ή δημιούργησε νέο repository
2. Ανέβασε το `index.html` ως `index.html`
3. Settings → Pages → Deploy from branch: main
4. Σε 2 λεπτά είναι διαθέσιμο στο `https://username.github.io/repo-name`

---

## 📁 Αρχεία

| Αρχείο | Περιγραφή |
|--------|-----------|
| `index.html` | Η κύρια εφαρμογή |
| `worker.js` | Κώδικας Cloudflare Worker |
| `sheets-script.gs` | Google Apps Script για Sheets |
| `README.md` | Αυτό το αρχείο |

---

## 💰 Κόστος

| Υπηρεσία | Κόστος |
|----------|--------|
| GitHub Pages | Δωρεάν |
| Cloudflare Worker | Δωρεάν (100K requests/μήνα) |
| Gemini API (free tier) | Δωρεάν |
| Google Sheets | Δωρεάν |
| **Σύνολο** | **$0/μήνα** |

> Αν το free tier του Gemini είναι υπερφορτωμένο, το κόστος του paid tier είναι ~$0.50-1/μήνα για 10-15 αναλύσεις.

---

## 🔒 Ασφάλεια

- Το Gemini API key **δεν αποθηκεύεται** στον κώδικα — βρίσκεται μόνο στον Cloudflare Worker ως Secret
- Τα PDF που ανεβάζεις **δεν αποθηκεύονται** πουθενά — πηγαίνουν απευθείας στο API και επιστρέφει το αποτέλεσμα
- Το Google Sheets URL είναι ορατό στον κώδικα αλλά δέχεται μόνο εγγραφές — δεν εκθέτει ευαίσθητα δεδομένα

---

## 📖 Χρήση

1. Άνοιξε την εφαρμογή
2. Συμπλήρωσε τα στοιχεία εταιρείας (για τις υπεύθυνες δηλώσεις)
3. Ανέβασε τη διακήρυξη σε PDF
4. Πάτα **Ανάλυση διαγωνισμού**
5. Από το report μπορείς να:
   - 🖨️ Εκτυπώσεις / αποθηκεύσεις ως PDF
   - 📅 Κατεβάσεις .ics για το Outlook Calendar
   - 💾 Αποθηκεύσεις το report ως HTML
   - 📊 Αποθηκεύσεις στο Google Sheets
   - 📧 Στείλεις με email
   - 📋 Αντιγράψεις τις υπεύθυνες δηλώσεις

---

## 🛠️ Τεχνολογίες

- **Frontend:** Vanilla HTML/CSS/JavaScript
- **AI:** Google Gemini API
- **Proxy:** Cloudflare Workers
- **Αποθήκευση:** Google Sheets via Apps Script
- **Hosting:** GitHub Pages

---

*Αναπτύχθηκε για την αυτοματοποίηση της διαδικασίας συμμετοχής σε δημόσιους διαγωνισμούς υπηρεσιών στην Ελλάδα (Ν. 4412/2016, ΕΣΗΔΗΣ).*
