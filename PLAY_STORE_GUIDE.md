# शिव खाता बुक (Shiv Khata Book) — मोबाइल से Android APK / Play Store AAB गाइड

यह प्रोजेक्ट बिना लैपटॉप या कंप्यूटर के—सीधे **मोबाइल फोन से**—Google Play Store पर अपलोड करने योग्य **`.aab` (Android App Bundle)** और **`.apk`** बनाने के लिए तैयार है।

---

## तरीका 1: PWABuilder (मोबाइल ब्राउज़र से 2 मिनट में `.aab` और `.apk`)
1. ऐप को लाइव पब्लिश करें (जैसे: `https://ais-pre-a67e6uancb7xgkoiyp6v43-926888069936.asia-southeast1.run.app` या आपका कस्टम डोमेन)।
2. मोबाइल Chrome में **`https://www.pwabuilder.com`** खोलें और अपना ऐप URL डालें।
3. **Package for stores → Android → Generate Package** चुनें।
   - **Package ID**: `com.shivkhatabook.app`
   - **App Name**: `शिव खाता बुक`
   - **Signing Key**: New Keystore चुनें (Play Store के लिए `.jks` व पासवर्ड सुरक्षित डाउनलोड होगा)।
4. डाउनलोड ज़िप में आपको **`.aab`** (Play Store के लिए), **`.apk`** (फोन टेस्टिंग के लिए) और **`assetlinks.json`** मिलेगा।

---

## तरीका 2: GitHub Actions क्लाउड बिल्ड (मोबाइल से पूर्ण नेटिव Android APK/AAB)
1. पूरा प्रोजेक्ट अपने GitHub रिपॉजिटरी में अपलोड/पुश करें (`.github/workflows/android-build.yml` पहले से शामिल है)।
2. Play Store के लिए **GitHub → Settings → Secrets and variables → Actions** में यह Secrets जोड़ें:
   - `ANDROID_KEYSTORE_BASE64`
   - `ANDROID_KEYSTORE_PASSWORD`
   - `ANDROID_KEY_ALIAS`
   - `ANDROID_KEY_PASSWORD`
3. **Actions → Build Shiv Khata Book Android APK & Play Store AAB → Run workflow** दबाएं।
4. कुछ मिनट में **Artifacts** से तैयार **`.apk`** और **`.aab`** मोबाइल पर डाउनलोड करें।

---

## Play Console अपलोड चरण
1. **Privacy Policy URL**: अपने ऐप का `https://YOUR_DOMAIN/?view=privacy` लिंक Play Console के App Content → Privacy Policy में डालें।
2. **Store Listing टेक्स्ट**: ऐप के **Play Store** टैब में मौजूद **हिंदी / English कॉपी किट** से App Title, Short Description और Full Description सीधे कॉपी-पेस्ट करें।
3. **SHA-256 Asset Links**: Play Console → Setup → App Integrity से SHA-256 कॉपी करें, ऐप के **चरण 5** में डालें और प्राप्त कोड को `public/.well-known/assetlinks.json` में अपडेट करें।
4. **SMS Policy**: Play Store सुरक्षित मोड (`ACTION_SENDTO`) डिफ़ॉल्ट है, इसलिए कोई प्रतिबंधित `SEND_SMS` परमिशन नहीं माँगी जाती।
