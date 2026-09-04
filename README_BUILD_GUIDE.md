# MUDARAKA - Multi-Platform Build Guide
# دليل بناء MUDARAKA متعدد المنصات

## 🚀 الطريقة 1: PWA (أسرع طريقة - تعمل فوراً)

### الخطوات:
1. انسخ الملفات التالية إلى مجلد على استضافة ويب (GitHub Pages مجاني):
   - `MUDARAKA_MultiPlatform.html` ← أعدله لـ `index.html`
   - `manifest.json`
   - أيقونة باسم `icon-512.png` (512×512 بكسل)

2. افتح الرابط على الهاتف ← اختر "Add to Home Screen"
3. ✅ يعمل على Android و iPhone و Windows فوراً!

---

## 🤖 الطريقة 2: Android (Google Play Store)

### المتطلبات:
- Node.js 18+
- Android Studio
- JDK 17

### الأوامر:
```bash
# 1. تثبيت الحزم
npm install

# 2. بناء المشروع
npm run build

# 3. إضافة Android
npx cap add android

# 4. مزامنة الملفات
npx cap sync

# 5. فتح Android Studio
npx cap open android

# 6. من Android Studio: Build → Generate Signed Bundle
```

---

## 🍎 الطريقة 3: iOS (App Store)

### المتطلبات:
- macOS
- Xcode 15+
- حساب Apple Developer

### الأوامر:
```bash
npm install
npm run build
npx cap add ios
npx cap sync
npx cap open ios
# من Xcode: Product → Archive → Distribute App
```

---

## 🖥️ الطريقة 4: Windows (.exe / .msi)

### المتطلبات:
- Rust (من https://rustup.rs)
- Node.js 18+

### الأوامر:
```bash
# 1. تثبيت Tauri CLI
cargo install tauri-cli

# 2. بناء المشروع
npm run build

# 3. بناء المثبت (Installer)
cargo tauri build

# الملف النهائي:
# src-tauri/target/release/bundle/msi/MUDARAKA_1.0.0_x64_en-US.msi
# src-tauri/target/release/bundle/nsis/MUDARAKA_1.0.0_x64-setup.exe
```

---

## 📋 ملخص الملفات

| الملف | الغرض |
|-------|-------|
| `MUDARAKA_MultiPlatform.html` | ملف التطبيق الرئيسي (استخدمه كـ index.html) |
| `manifest.json` | إعدادات PWA |
| `package.json` | إعدادات Node.js / Capacitor |
| `capacitor.config.json` | إعدادات Capacitor (Android/iOS) |
| `src-tauri/tauri.conf.json` | إعدادات Tauri (Windows) |
| `src-tauri/Cargo.toml` | إعدادات Rust (Windows) |

---

## ⚠️ ملاحظات مهمة

1. **localStorage**: في Capacitor، localStorage يعمل بشكل طبيعي. لكن إذا واجهت مشاكل، استخدم `@capacitor/preferences`.
2. **الأيقونات**: يجب إضافة أيقونات PNG بأحجام: 72, 96, 128, 144, 152, 192, 384, 512 بكسل.
3. **الشهادات**: لنشر على Google Play / App Store، تحتاج شهادات توقيع (Signing Certificates).
4. **الأمان**: في Tauri، localStorage يعمل بشكل طبيعي دون تعديلات.

---

## 🎯 الحل الأسرع (الموصى به)

ارفع الملف `MUDARAKA_MultiPlatform.html` كـ `index.html` على **GitHub Pages** أو **Netlify** أو **Vercel** في 5 دقائق، وسيعمل كـ PWA على كل الأجهزة دون متاجر!
