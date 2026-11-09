KRISHNA DAIRY MARMI — PWA सेटअप गाइड
======================================

यह PWA wrapper आपकी मौजूदा Google Apps Script ऐप को मोबाइल में इंस्टॉल होने योग्य बनाता है।
Google Sheets, लॉगिन, किसान/ग्राहक/मैनेजर फीचर्स और रिकॉर्ड Apps Script में ही रहेंगे।

जरूरी बातें
-----------
1. आपकी मौजूदा Apps Script Web App पहले से Deploy होनी चाहिए।
2. Web App access/permissions पहले की तरह रखें। इस wrapper में कोई Spreadsheet डेटा कॉपी नहीं होता।
3. PWA shell को HTTPS hosting पर प्रकाशित करना जरूरी है (GitHub Pages / Firebase Hosting / Cloudflare Pages)।
4. यह PWA shell ऑफलाइन खुल सकता है, लेकिन दूध का लाइव हिसाब चलाने के लिए इंटरनेट जरूरी है।
5. ऐप के लाइव iframe/API डेटा को Service Worker cache नहीं करता।

कदम 1 — Apps Script URL
-----------------------
Google Apps Script > Deploy > Manage deployments में Web App URL कॉपी करें।
URL आम तौर पर इस तरह होती है:
https://script.google.com/macros/s/DEPLOYMENT_ID/exec

इस फोल्डर की config.js खोलें और:
PASTE_YOUR_APPS_SCRIPT_WEB_APP_URL_HERE
को अपनी असली /exec URL से बदलें। URL के आगे-पीछे quotes रहने दें।

कदम 2 — HTTPS Hosting
---------------------
इस पूरे फोल्डर की सामग्री (index.html, config.js, manifest.webmanifest,
sw.js, icons/) को किसी HTTPS static host पर प्रकाशित करें।
उदाहरण: GitHub Pages में repository बनाकर इन सभी फाइलों को repository root में upload करें,
फिर Settings > Pages में branch से deploy करें।
Hosting URL खुलने पर PWA का setup page नहीं, डेयरी लॉगिन दिखना चाहिए।

कदम 3 — मोबाइल में इंस्टॉल
-------------------------
Android Chrome:
- Hosting URL खोलें।
- Chrome मेन्यू (⋮) > Install app / Add to Home screen चुनें।
- KRISHNA DAIRY MARMI आइकन Home Screen पर आ जाएगा।

iPhone Safari:
- Hosting URL खोलें।
- Share > Add to Home Screen चुनें।

मैनेजर लॉगिन
------------
इस किट की config.js में दिया गया URL portal=manager के साथ है, इसलिए PWA खुलने पर सीधे मैनेजर पोर्टल खुलेगा।
किसान/ग्राहक पोर्टल को डिफॉल्ट रूप में खोलना हो तो URL के अंत से ?portal=manager हटा दें।
अलग deployment/डेटाबेस की जरूरत नहीं है।

अपडेट
-----
PWA shell बदलने पर sw.js में CACHE का version (जैसे v1 से v2) बदलें।
Apps Script कोड बदलने पर Apps Script deployment में New version deploy करें।

सुरक्षा
-------
- config.js में केवल Web App URL रखें; कोई पासवर्ड/PIN न रखें।
- सार्वजनिक लिंक पर अनधिकृत access रोकने के लिए Apps Script deployment की access policy ध्यान से चुनें।
- PWA wrapper कोई offline login/data storage नहीं करता।
- लाइव इंस्टॉलेशन से पहले एक test copy/backup पर किसान लॉगिन, मैनेजर लॉगिन,
  कलेक्शन, बिक्री, भुगतान, रिपोर्ट, print/download और manager portal जांचें।

सीमा
----
यह Native Android APK नहीं है। यह installable PWA है जो मौजूदा Apps Script वेब ऐप को
standalone mobile window में दिखाती है। लाइव Google Apps Script app के लिए इंटरनेट जरूरी है।
