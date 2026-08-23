# চুইঘর · Chuighor

খুলনার চুই ঝাল বিক্রির একটি সম্পূর্ণ ওয়েবসাইট — এক ফাইলে, কোনো সার্ভার বা বিল্ড টুল ছাড়াই চলে।
পণ্যের তালিকা, ওজনভেদে দাম, কার্ট, ডেলিভারি চার্জ, অর্ডার ফর্ম এবং WhatsApp / Messenger–এ অর্ডার পাঠানোর ব্যবস্থা আছে।

A single-file storefront for selling chui jhal (Piper chaba). Pure HTML/CSS/JS — no build step, no backend.

---

## ফাইলগুলো কী কী

| ফাইল | কাজ |
|---|---|
| `index.html` | পুরো সাইট — HTML, CSS, JavaScript সব এই এক ফাইলে |
| `404.html` | ভুল লিংকে গেলে যে পাতাটি দেখাবে |
| `robots.txt` | সার্চ ইঞ্জিনের জন্য |
| `.nojekyll` | GitHub Pages যেন ফাইল প্রসেস না করে |
| `.gitignore` | অপ্রয়োজনীয় ফাইল git-এ যাবে না |

---

## ১. প্রথম কাজ — নিজের তথ্য বসান

`index.html` যেকোনো টেক্সট এডিটরে (VS Code, Notepad++, এমনকি Notepad) খুলুন।
নিচের দিকে `<script>` অংশের একেবারে শুরুতে এই ব্লকটা পাবেন:

```js
const SHOP = {
  name: "চুইঘর",
  phone: "01XXXXXXXXX",                     // আপনার নম্বর
  whatsapp: "8801XXXXXXXXX",                // দেশের কোড সহ, + বা স্পেস ছাড়া
  facebook: "https://facebook.com/",        // আপনার পেজের লিংক
  delivery: { dhaka: 80, outside: 130, freeAbove: 2000 }
};
```

- `phone` — যে নম্বরে কল আসবে
- `whatsapp` — অবশ্যই `880` দিয়ে শুরু, কোনো `+`, স্পেস বা ড্যাশ নয়। যেমন `8801712345678`
- `facebook` — আপনার পেজের পুরো লিংক
- `delivery` — ঢাকার ভিতরে, ঢাকার বাইরে চার্জ, আর কত টাকার উপরে ডেলিভারি ফ্রি

### পণ্য ও দাম বদলানো

ঠিক নিচেই `PRODUCTS` তালিকা:

```js
{ id:"mota", bn:"চুই ঝাল — মোটা গোছা", en:"Thick Stem", seed:7, kind:"stem",
  tag:"সবচেয়ে জনপ্রিয়",
  desc:"পুরনো লতার মোটা কাণ্ড। ঝাঁঝ সবচেয়ে বেশি...",
  variants:[{w:"২৫০ গ্রাম",p:320},{w:"৫০০ গ্রাম",p:610},{w:"১ কেজি",p:1180}] },
```

- `bn` / `en` — পণ্যের নাম
- `desc` — বর্ণনা
- `tag` — কোণায় ছোট লেবেল (না চাইলে পুরো লাইনটা মুছে দিন)
- `variants` — `w` মানে ওজন, `p` মানে দাম (শুধু সংখ্যা, `৳` লিখবেন না)
- `id` — প্রতিটি পণ্যের আলাদা হতে হবে
- `kind` — ছবির ধরন: `stem`, `vine`, `root`, `cut`, `powder`, `combo`
- `seed` — যেকোনো সংখ্যা; বদলালে ছবির টুকরোগুলোর সাজ বদলে যায়

সেভ করে ব্রাউজারে `index.html` ডাবল-ক্লিক করলেই দেখতে পাবেন।

---

## ২. কম্পিউটার থেকে GitHub-এ পুশ করা

### যা লাগবে

- **Git** — https://git-scm.com/downloads থেকে ইনস্টল করুন
- একটি **GitHub** অ্যাকাউন্ট — https://github.com

### ধাপ ১ — GitHub-এ খালি রিপো বানান

1. https://github.com/new এ যান
2. **Repository name**: `chuighor` (বা যা ইচ্ছা)
3. **Public** রাখুন (GitHub Pages ফ্রিতে পেতে হলে পাবলিক দরকার)
4. **README, .gitignore, license — কিছুই টিক দেবেন না** (এগুলো আমাদের ফোল্ডারেই আছে)
5. **Create repository** চাপুন

### ধাপ ২ — কম্পিউটারে টার্মিনাল খুলুন

- **Windows**: ফোল্ডারের ভিতরে ডান-ক্লিক → *Git Bash Here* (বা *Open in Terminal*)
- **Mac**: ফোল্ডারে ডান-ক্লিক → *New Terminal at Folder*

### ধাপ ৩ — কমান্ডগুলো একে একে চালান

```bash
# প্রথমবার হলে নিজের পরিচয় সেট করুন (একবারই লাগবে)
git config --global user.name "আপনার নাম"
git config --global user.email "your@email.com"

# এই ফোল্ডারটিকে git রিপো বানান
git init
git add .
git commit -m "চুইঘর ওয়েবসাইট"
git branch -M main

# GitHub-এর রিপোর সঙ্গে যুক্ত করুন — USERNAME আর REPO বদলে দিন
git remote add origin https://github.com/USERNAME/REPO.git
git push -u origin main
```

> **পাসওয়ার্ড চাইলে:** GitHub সাধারণ পাসওয়ার্ড নেয় না। https://github.com/settings/tokens →
> *Generate new token (classic)* → `repo` স্কোপ টিক দিন → টোকেনটি কপি করে পাসওয়ার্ডের জায়গায় পেস্ট করুন।
> সহজ বিকল্প: [GitHub CLI](https://cli.github.com) ইনস্টল করে একবার `gh auth login` চালান।

### টার্মিনাল পছন্দ না হলে

[GitHub Desktop](https://desktop.github.com) ইনস্টল করুন →
*File → Add local repository* → এই ফোল্ডারটি বেছে নিন → *Publish repository*। ব্যস।

---

## ৩. সাইটটি লাইভ করা (ফ্রি হোস্টিং)

পুশ করার পর:

1. রিপোর **Settings** → বাঁ পাশে **Pages**
2. **Source**: `Deploy from a branch`
3. **Branch**: `main`, ফোল্ডার `/ (root)` → **Save**
4. ১–২ মিনিট পর সাইট লাইভ হবে এখানে:
   `https://USERNAME.github.io/REPO/`

### নিজের ডোমেইন যোগ করতে চাইলে (যেমন `chuighor.com`)

1. Settings → Pages → **Custom domain** এ ডোমেইনটি লিখে Save করুন
2. ডোমেইন যেখান থেকে কিনেছেন সেখানে DNS-এ যোগ করুন:
   - `A` রেকর্ড → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - অথবা `www` এর জন্য `CNAME` → `USERNAME.github.io`
3. DNS ছড়াতে কয়েক ঘণ্টা লাগতে পারে, এরপর **Enforce HTTPS** টিক দিন

---

## ৪. পরে কিছু বদলালে

```bash
git add .
git commit -m "দাম হালনাগাদ"
git push
```

পুশ করার ১ মিনিটের মধ্যেই লাইভ সাইট আপডেট হয়ে যাবে।

---

## যা এই সাইট পারে না

- **অর্ডার জমা রাখতে পারে না।** সার্ভার নেই, তাই অর্ডার আপনার কাছে WhatsApp বা Messenger বার্তা হিসেবে আসে। কোনো ডেটাবেজ নেই।
- **অনলাইন পেমেন্ট নেই।** বিকাশ/নগদ/কার্ড গেটওয়ে লাগলে আলাদা সার্ভিস (যেমন SSLCommerz, aamarPay) যোগ করতে হবে।
- কার্টের তথ্য শুধু ক্রেতার নিজের ব্রাউজারে থাকে — আপনি সেটা দেখতে পান না।

---

## টুকিটাকি

- **ফন্ট**: Tiro Bangla + Hind Siliguri (Google Fonts থেকে আসে, ইন্টারনেট লাগে)
- **ছবি**: কোনো ছবি ফাইল নেই — চুইয়ের সব ছবি কোড দিয়ে আঁকা SVG, তাই সাইট খুব হালকা ও দ্রুত
- **ডার্ক মোড**: ক্রেতার ফোন/কম্পিউটারের সেটিং অনুযায়ী নিজে থেকেই বদলায়
