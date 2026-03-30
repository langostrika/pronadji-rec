# Pronađi Reč

Embeddable word search igra za portale i CMS platforme.  
Napravljena za [021.rs](https://021.rs) i slične portale.

---

## 📁 Struktura fajlova

```
wordsearch/
├── index.html     ← glavna igra (GitHub Pages stranica)
├── embed.html     ← snippet za ugradnju u CMS
└── README.md      ← ovo što čitaš
```

---

## 🚀 Deploy na GitHub Pages (korak po korak)

### Korak 1 — Napravi GitHub repozitorijum

1. Idi na [github.com/new](https://github.com/new)
2. Naziv repozitorijuma: `wordsearch`
3. Odaberi **Public**
4. Klikni **Create repository**

### Korak 2 — Uploaduj fajlove

**Opcija A — Direktno na GitHub (bez terminala):**
1. Otvori repozitorijum
2. Klikni **Add file → Upload files**
3. Prevuci `index.html` i `embed.html`
4. Klikni **Commit changes**

**Opcija B — Git terminal:**
```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/TVOJ-USERNAME/wordsearch.git
git push -u origin main
```

### Korak 3 — Uključi GitHub Pages

1. Idi na **Settings** (u repozitorijumu)
2. Levi meni → **Pages**
3. Source: **Deploy from a branch**
4. Branch: `main` / `/ (root)`
5. Klikni **Save**

✅ Za nekoliko minuta igra je dostupna na:  
`https://TVOJ-USERNAME.github.io/wordsearch/`

---

## 🔑 Admin pristup

Admin opcija "Uredi reči" **nije vidljiva** normalnim posetiocima.  
Vidljiva je samo kada URL sadrži tajni parametar:

```
https://TVOJ-USERNAME.github.io/wordsearch/?admin=redakcija2025
```

### Promena lozinke

Otvori `index.html`, pronađi liniju:
```javascript
const ADMIN_KEY = 'redakcija2025';
```
Zameni `redakcija2025` sa sopstvenom lozinkom i re-uploaduj fajl.

---

## 📋 Ugradnja u CMS (021.rs i ostali)

### Najjednostavniji način — iframe u HTML bloku

```html
<iframe
  id="wordsearch-frame"
  src="https://TVOJ-USERNAME.github.io/wordsearch/"
  width="100%" height="700" frameborder="0"
  style="border:none; border-radius:12px;"
></iframe>

<script>
window.addEventListener('message', function(e) {
  if (e.data && e.data.type === 'wordsearch-resize') {
    document.getElementById('wordsearch-frame').height = e.data.height;
  }
});
</script>
```

Zameni `TVOJ-USERNAME` sa tvojim GitHub korisničkim imenom.

### Embed sa specifičnim rečima (u URL-u)

```
https://TVOJ-USERNAME.github.io/wordsearch/?words=SRBIJA,NOVOSADSKI,FESTIVAL
```

Reči se mogu menjati direktno u URL-u — bez edita koda.

### Admin embed (za uredničku stranicu u CMS-u)

```
https://TVOJ-USERNAME.github.io/wordsearch/?admin=redakcija2025
```

Ovo prikazuje dugme "Uredi reči". Admin unosi reči, klikne  
"Primeni i generiši" — URL se automatski ažurira sa novim rečima.  
Taj URL možeš kopirati i staviti kao `src` u javni embed.

---

## 📐 Auto-resize (visina iframe-a)

Widget automatski šalje `postMessage` roditeljskoj strani:

```javascript
{ type: 'wordsearch-resize', height: 720 }
```

Listener u `embed.html` hvata tu poruku i podešava visinu iframe-a.  
Ovo funkcioniše u svim modernim browserima i CMS-ovima koji  
dopuštaju HTML blokove sa `<script>`.

---

## 🎮 Funkcionalnosti igre

- ✅ Reči horizontalno, vertikalno, dijagonalno — u oba smera  
- ✅ Prevlačenje mišem i touch (mobilni/tablet)  
- ✅ Timer koji startuje prvim potezom  
- ✅ Animacija pri pronalasku reči  
- ✅ Responzivno (računar / tablet / mobitel)  
- ✅ Admin mode putem `?admin=KEY` URL parametra  
- ✅ Reči u URL-u (`?words=...`) — lako menjanje seta  
- ✅ Auto-resize iframe visine

---

## ⚙️ Prilagođavanja

Sve opcije su na vrhu `index.html`:

```javascript
const ADMIN_KEY    = 'redakcija2025';         // lozinka za admin
const DEFAULT_WORDS = ['INDIJA','PROVOD',...]; // podrazumevane reči
```
