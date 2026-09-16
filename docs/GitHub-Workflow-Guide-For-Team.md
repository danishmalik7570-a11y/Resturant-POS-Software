# TezPOS Pro — GitHub Workflow Guide (For Team/Juniors)
### Repo: github.com/danishmalik7570-a11y/Resturant-POS-Software

Yeh guide un sab developers ke liye hai jo is project pe kaam karenge. Step by step follow karo.

---

## 1. Repo Access Lena

1. Danish/Lead se GitHub invite lo (email pe accept karo)
2. GitHub account nahi hai to pehle banao: https://github.com/signup
3. Access milne ke baad, apne computer pe **Git install** karo: https://git-scm.com/downloads

---

## 2. Pehli Baar Repo Setup Karna (Sirf Ek Baar)

```bash
# Apna naam/email Git mein set karo (sirf ek baar, poore system ke liye)
git config --global user.name "Apna Naam"
git config --global user.email "apna-email@example.com"

# Repo clone karo (apne computer pe download)
git clone https://github.com/danishmalik7570-a11y/Resturant-POS-Software.git

# Project folder mein jao
cd Resturant-POS-Software
```

---

## 3. Har Din Kaam Shuru Karne Se Pehle

```bash
git checkout develop        # develop branch pe jao
git pull origin develop     # latest changes le lo (taake purana code na ho)
```

**Yeh step kabhi mat bhoolna** — nahi to purane code pe kaam karoge aur baad mein conflicts hongi.

---

## 4. Apna Kaam Shuru Karna (Naya Branch Banao)

Har naye kaam/module ke liye **apna alag branch** banao — kabhi bhi `main` ya `develop` pe direct kaam mat karo.

```bash
git checkout -b feature/tumhara-module-naam
```

Example names:
- `feature/kitchen-display`
- `feature/billing-module`
- `feature/inventory-system`
- `feature/waiter-app`

---

## 5. Code Likhne Ke Baad — Save Karna

```bash
git status                          # dekho kya-kya change hua
git add .                           # sab changes stage karo
git commit -m "kya kaam kiya likho" # save karo (short, clear message)
```

**Achi commit message ki example:**
- ✅ `"Add order creation API endpoint"`
- ✅ `"Fix cashier billing calculation bug"`
- ❌ `"update"` / `"changes"` / `"fix"` (bohot vague hai)

---

## 6. GitHub Pe Bhejna (Push)

```bash
git push origin feature/tumhara-module-naam
```

---

## 7. Pull Request (PR) Banana

1. GitHub website pe repo kholo
2. Upar ek yellow box dikhega: **"Compare & pull request"** — usko click karo
3. Base branch: `develop`, Compare branch: apna `feature/...` branch (already set hoga)
4. Title + description likho ke kya kaam kiya
5. **"Create pull request"** click karo
6. Lead/Danish review karega, agar sab thik hai to **Merge** kar dega

⚠️ **Kabhi bhi khud apna PR `main` branch mein merge mat karo.** Sirf `develop` mein.

---

## 8. Agle Din Phir Se Start Karna

```bash
git checkout develop
git pull origin develop
git checkout -b feature/naya-kaam
```

(Purana feature branch complete ho gaya aur merge ho gaya, to naya banao)

---

## 9. Agar Conflict Aa Jaye (Ghabrana Nahi)

Conflict tab hota hai jab do logon ne **same line** pe alag-alag change kiya ho. Terminal mein file ke andar aisa dikhega:

```
<<<<<<< HEAD
tumhara code
=======
doosre ka code
>>>>>>> develop
```

- Dono versions dekho, decide karo kaunsa rakhna hai (ya dono combine karo)
- `<<<<<<<`, `=======`, `>>>>>>>` lines delete kar do
- File save karo, phir:
```bash
git add .
git commit -m "Resolved merge conflict"
git push origin feature/tumhara-module-naam
```

Agar samajh na aaye, **lead se pooch lo** — force push ya random commands mat chalao.

---

## 10. Golden Rules (Yaad Rakhne Wali Baatein)

| ✅ Karo | ❌ Mat Karo |
|---|---|
| Roz `git pull` karke start karo | Purane code pe kaam shuru na karo |
| Apna alag `feature/*` branch banao | `main` ya `develop` pe direct commit na karo |
| Chhote, clear commits karo | Ek hi commit mein sara kaam na daalo |
| PR banao review ke liye | Khud apna kaam khud merge na karo |
| Apna module apni app folder mein rakho | Doosre ke module ki file edit na karo |
| Conflict pe lead se pooch lo | Confuse ho ke random commands na chalao |

---

## 11. Sab Commands Ek Jagah (Cheat Sheet)

```bash
git clone <repo-url>              # Repo download karo
git checkout develop              # develop branch pe jao
git pull origin develop           # Latest code lo
git checkout -b feature/naam      # Naya branch banao
git status                        # Kya change hua dekho
git add .                         # Changes stage karo
git commit -m "message"           # Save karo
git push origin feature/naam      # GitHub pe bhejo
git log                           # History dekho
```

---

Koi bhi command samajh na aaye ya error aaye, screenshot le kar Danish/Lead ko bhejo — khud se guess kar ke random commands mat chalao, isse repo kharab ho sakti hai.
