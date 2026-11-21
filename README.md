# AITCO Fix — قناة التحديث العامة / public update channel

هذا المستودع هو القناة التي تجد منها أجهزة شركة AITCO الإصدارات الجديدة من **AITCO Fix** (أداة الصيانة الداخلية) وقائمة مؤشرات البرامج الضارة. لا يحتاج الجهاز حساب GitHub ولا مفتاحاً: يقرأ آخر إصدار من العنوان

```
https://github.com/belalpark/aitco-fix-updates/releases/latest/download/AITCOFix.update.ini
```

## ما في كل إصدار (Release)

| الملف | ما هو |
|---|---|
| `AITCOFix-Setup-<version>.exe` | المثبّت، موقَّع رقمياً (Authenticode) بشهادة AITCO |
| `AITCOFix.update.ini` | رقم الإصدار، واسم المثبّت وبصمته SHA-256، وعلامة الإصدار، واسم قائمة المؤشرات وبصمتها |
| `AITCOFix.update.ini.p7s` | توقيع CMS منفصل لملف التحديث بالشهادة نفسها |
| `indicators.json` | قائمة المؤشرات: أسماء وبصمات SHA-256 ومواضع التشغيل — **لا عيّنات** |

## كيف يتحقق الجهاز قبل أي شيء

- لا يُشغَّل مثبّت إلا إذا طابقت بصمته SHA-256 ما في `AITCOFix.update.ini`، وكان توقيعه الرقمي سليماً، والجهة الموقِّعة هي المعتمدة على الجهاز (بصمة الشهادة).
- لا تُستعمل قائمة مؤشرات إلا إذا كان توقيع `AITCOFix.update.ini.p7s` سليماً ومن الجهة المعتمدة، وطابقت بصمة القائمة ما في ملف التحديث، ولم تكن أقدم من القائمة المستخدمة.
- أي فشل (الشبكة، GitHub، ملف ناقص) يُكتب سطراً في السجل ويبقي ما على الجهاز كما هو، ولا يوقف الفحص.

## لا أسرار هنا

المستودع عام عن قصد: لا كلمات مرور، ولا أسرار تطبيقات، ولا مفاتيح، ولا بيانات أجهزة أو موظفين. التقارير تذهب بالبريد إلى قسم تقنية المعلومات، لا إلى هنا.

## النشر (لقسم تقنية المعلومات)

على جهاز قسم التقنية الذي يوقّع البرنامج: `Signing\3-Publish-Update.bat` واترك المجلد فارغاً. يجهّز السكربت الملفات الأربعة في `Publish-Output\GitHub-v<version>` ويفتح صفحة «إصدار جديد»؛ اسحب الملفات إليها واضغط **Publish release**. لنشر قائمة مؤشرات جديدة بالمثبّت نفسه: `Publish-Update.ps1 -ListOnly` (ارفع `version` في القائمة أولاً).

---

This repository is the channel the AITCO PCs read new versions of **AITCO Fix** (the company's internal maintenance tool) and the malware indicator list from — no GitHub account or key on the PCs; they read the latest release at the address above.

**Each release:** the Authenticode-signed installer; `AITCOFix.update.ini` (version, installer name and SHA-256, release tag, indicator list name and SHA-256); `AITCOFix.update.ini.p7s` (a detached CMS signature of the update file with the same certificate); `indicators.json` (names, SHA-256 hashes and start-up places — **no samples**).

**What a PC checks:** an installer runs only if its SHA-256 matches the update file, its signature is valid and its signer is the one allowed on the PC (certificate thumbprint). An indicator list is used only if the update file's CMS signature is valid and by the allowed signer, the list's SHA-256 matches, and it is not older than the list in use. Any failure is one log line and keeps what the PC has; it never stops a scan.

**No secrets here:** no passwords, app secrets, keys, device or employee data. Reports go to the IT department by e-mail, never here.

**Publishing (IT):** on the IT PC that signs the program, run `Signing\3-Publish-Update.bat` and leave the folder empty; drag the four files from `Publish-Output\GitHub-v<version>` onto the "new release" page that opens and press **Publish release**. For a new indicator list with the same installer: `Publish-Update.ps1 -ListOnly` (raise the list's `version` first).
