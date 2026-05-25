# 🎬 ReelzMaker — SaaS Starter Kit

أداة تحويل الصور إلى ريلز احترافي لانستاغرام.

---

## 📁 هيكل المشروع

```
reelzmaker/
├── index.html      ← الصفحة الرئيسية (Landing Page)
├── signup.html     ← صفحة التسجيل
├── app.html        ← أداة صنع الفيديو (انسخ instagram-promo-maker-v2.html)
└── README.md       ← هذا الملف
```

---

## 🚀 النشر على Vercel (مجاناً) — 5 دقائق

### الخطوة 1: رفع الملفات على GitHub
1. اذهب إلى [github.com](https://github.com) وأنشئ مستودعاً جديداً
2. ارفع جميع الملفات (index.html, signup.html, app.html)

### الخطوة 2: ربط Vercel
1. اذهب إلى [vercel.com](https://vercel.com)
2. "Add New Project" → اختر مستودعك من GitHub
3. اضغط Deploy ✅
4. موقعك جاهز على: `your-project.vercel.app`

### الخطوة 3: ربط دومين مخصص (اختياري)
- في Vercel → Settings → Domains
- أضف دومينك مثل: reelzmaker.com

---

## 🔐 إضافة نظام المستخدمين (Supabase)

### 1. إنشاء مشروع Supabase
- اذهب إلى [supabase.com](https://supabase.com)
- أنشئ مشروعاً جديداً مجاناً

### 2. إضافة SDK في HTML
```html
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
<script>
  const supabase = window.supabase.createClient(
    'YOUR_SUPABASE_URL',
    'YOUR_SUPABASE_ANON_KEY'
  );
</script>
```

### 3. تسجيل مستخدم جديد
```javascript
const { data, error } = await supabase.auth.signUp({
  email: 'user@example.com',
  password: 'password123'
});
```

### 4. تسجيل الدخول
```javascript
const { data, error } = await supabase.auth.signInWithPassword({
  email: 'user@example.com',
  password: 'password123'
});
```

### 5. تسجيل الدخول بـ Google
```javascript
await supabase.auth.signInWithOAuth({ provider: 'google' });
```

---

## 💳 إضافة نظام الدفع (Stripe)

### 1. إنشاء حساب Stripe
- اذهب إلى [stripe.com](https://stripe.com)
- أنشئ منتجاً بسعر $12/شهر

### 2. Stripe Checkout (الأسرع)
```javascript
// في زر الاشتراك
async function subscribe() {
  const response = await fetch('/api/create-checkout', {
    method: 'POST',
    body: JSON.stringify({ plan: 'pro' })
  });
  const { url } = await response.json();
  window.location.href = url; // يُحوَّل لصفحة Stripe
}
```

### 3. Vercel Serverless Function
أنشئ ملف `api/create-checkout.js`:
```javascript
const stripe = require('stripe')(process.env.STRIPE_SECRET_KEY);

module.exports = async (req, res) => {
  const session = await stripe.checkout.sessions.create({
    payment_method_types: ['card'],
    line_items: [{ price: 'price_YOUR_PRICE_ID', quantity: 1 }],
    mode: 'subscription',
    success_url: 'https://yoursite.com/app',
    cancel_url: 'https://yoursite.com/pricing',
  });
  res.json({ url: session.url });
};
```

---

## 📊 الخطوات الكاملة للإطلاق

| الأسبوع | المهمة | الأدوات |
|---------|--------|---------|
| 1 | رفع الموقع | GitHub + Vercel |
| 2 | نظام المستخدمين | Supabase Auth |
| 3 | حدود الباقة المجانية | Supabase Database |
| 4 | نظام الدفع | Stripe |
| 5 | الإطلاق والتسويق | Instagram + Twitter |

---

## 🛠 الأدوات المستخدمة (كلها مجانية)

| الأداة | الاستخدام | الرابط |
|--------|----------|--------|
| Vercel | استضافة | vercel.com |
| Supabase | قاعدة بيانات + Auth | supabase.com |
| Stripe | الدفع | stripe.com |
| Pixabay | موسيقى مجانية | pixabay.com |

---

## 💡 نصائح للتسويق

1. **صنع محتوى بالأداة نفسها** — أفضل إعلان هو استخدام المنتج
2. **استهدف أصحاب المتاجر** على انستاغرام وواتساب
3. **أعطِ 10 حسابات مجانية** لمؤثرين صغار مقابل محتوى
4. **نشر في مجموعات الريادة** على تيليغرام وفيسبوك

---

صُنع بـ ❤️ للسوق العربي
