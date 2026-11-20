# 📚 Gyan App

SSC · Railway · Bank · UP Police जैसी परीक्षाओं की तैयारी के लिए क्विज़, हस्तलिखित-शैली नोट्स, गेम्स और चैट वाला मोबाइल-फ्रेंडली वेब ऐप।
*A mobile-friendly exam-prep web app with quizzes, handwritten-style notes, games and chat (Hindi + English).*

## ✨ Features

- **विषय:** इतिहास (प्राचीन, मध्यकालीन, आधुनिक), भूगोल, हिंदी, English, रिजनिंग, गणित, संविधान, विज्ञान, कंप्यूटर (ICT)
- **Subject Notes:** हर विषय के अध्याय-वार हस्तलिखित-शैली नोट्स
- **Topic-wise Quiz:** हर टॉपिक का अलग क्विज़, साथ में मिक्स क्विज़
- Practice Paper, Monthly Exam, Saved / Revise, Games, Chat
- हिंदी / English toggle, Dark mode
- Offline सपोर्ट (service worker) और PWA manifest

## 📁 Files

| File | काम |
|---|---|
| `index.html` | ऐप का पूरा कोड और UI |
| `d01.js … d18.js` | बड़े क्विज़ सवाल और नोट्स का डेटा (index.html से पहले load होते हैं) |
| `privacy.html`, `terms.html`, `delete-account.html` | Privacy Policy, Terms of Use, खाता हटाने का पेज (Play Store में यही लिंक दें) |
| `sw.js` | Offline cache (network-first, इसलिए अपडेट तुरंत आते हैं) |
| `manifest.json` | PWA जानकारी |

> ⚠️ `d01.js … d18.js` और `index.html` हमेशा एक ही जगह (root) में रखें। फ़ाइलों के नाम या क्रम न बदलें।

## 🚀 GitHub Pages पर डालने के स्टेप्स

1. GitHub पर नया **Public** repo बनाएँ (जैसे `Gyan-App`).
2. `index.html`, `sw.js`, `manifest.json`, `privacy.html`, `terms.html`, `delete-account.html`, `README.md` और `d01.js` से `d18.js` तक सारी फ़ाइलें upload करें (*Add file → Upload files*).
3. **Settings → Pages → Source:** *Deploy from a branch* → Branch `main`, folder `/ (root)` → **Save**.
4. 1–2 मिनट बाद लिंक मिलेगा: `https://sidhhi22680.github.io/Gyan-App/`

## 📱 Kodular में जोड़ना

- WebViewer का **HomeUrl** ऊपर वाला GitHub Pages लिंक रखें।
- ऐप में बदलाव करने पर बस GitHub पर फ़ाइल बदलें; ऐप दोबारा build या Play Store पर update करने की ज़रूरत नहीं।

## 🔐 Firebase सेटअप

1. **Authentication → Sign-in method:** *Email/Password* चालू करें।
2. **Google Cloud Console → APIs & Services → Credentials** में ऐप की API key खोलें:
   - *Application restrictions:* **Websites** चुनकर `https://sidhhi22680.github.io/*` डालें (Kodular WebView में बिना GitHub लिंक के खाली referer जाता है और `Requests from referer <empty> are blocked` error आता है)
   - *API restrictions:* सिर्फ़ **Identity Toolkit API** और **Token Service API**
3. **Realtime Database → Rules:** खुले rules (`".read": true, ".write": true`) न रखें। कम से कम `auth != null` रखें और हर यूज़र को सिर्फ़ अपना डेटा लिखने दें।

> Firebase की web API key secret नहीं होती। असली सुरक्षा Database Rules (और चाहें तो App Check) से आती है, key को छिपाने से नहीं।

## ➕ नया कंटेंट जोड़ना

- **नया क्विज़ सवाल:** `d01–d18.js` की संबंधित फ़ाइल में उसी फ़ॉर्मेट में जोड़ें (`"हिंदी सवाल|English question"` और विकल्प `"हिंदी|English"`).
- **नया नोट:** `NOTES=NOTES.concat([...])` वाली फ़ाइल में जोड़ें।
- भूगोल के नए टॉपिक के लिए `index.html` में `GEOQ` सूची में एक entry जोड़ें।
- बदलाव के बाद `sw.js` में `var C='gyan-v1'` को `gyan-v2` कर दें, ताकि पुराना cache साफ़ हो जाए।

## 🧪 लोकल में चलाना

फ़ाइल को सीधे खोलने पर service worker नहीं चलता; सर्वर से चलाएँ:

```bash
python3 -m http.server 8000
# फिर ब्राउज़र में http://localhost:8000
```

## 📝 Notes

- ऐप ब्राउज़र के `localStorage` में progress रखता है (saved सवाल, streak आदि)। ब्राउज़र/ऐप का डेटा साफ़ होने पर यह मिट जाता है।
- सवाल और नोट्स ऐप के साथ public रहते हैं (पेज का source देखने पर दिखते हैं)।

## 📢 AdMob जोड़ते समय

- Privacy Policy में AdMob पहले से लिखा है ("once ads are switched on")। विज्ञापन चालू करते समय Play Console के **Data safety** फ़ॉर्म में *Advertising ID* और *Device or other IDs* भी चुनें, और **Ads declaration** में "Yes" करें।
- Kodular में AdMob जोड़ने के बाद ऐप फिर से build करना पड़ेगा।

## 🔗 Play Store के लिए लिंक

- Privacy Policy: `https://sidhhi22680.github.io/Gyan-App/privacy.html`
- Account deletion: `https://sidhhi22680.github.io/Gyan-App/delete-account.html`
- Terms: `https://sidhhi22680.github.io/Gyan-App/terms.html`
