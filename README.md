# ONU-Pro-Tool
Setting up ONU Pro Tool on Orange Pi (Flask &amp; HTTP API)
# 🚀 ONU Pro Tool v2.0 - FTTH Automation Tool

أداة ميدانية احترافية وخفيفة الوزن مصممة لفنيي الشبكات (FTTH) لأتمتة عملية برمجة ورفع إعدادات أجهزة الـ ONU (Huawei) بمجرد ربط الكابل، وبسرعة فائقة دون الحاجة الى راوتر المشترك وبسرعه تصل الى 4 ثانية

تعتمد الأداة على بيئة **Flask (Python)** وتقوم بإرسال طلبات **HTTP Requests** مباشرة والتعامل مع الـ Tokens والـ Sessions ديناميكياً، مع دعم كامل لإشعارات تليجرام الفورية فور نجاح العملية.

---

## 📌 مميزات الإصدار الثاني (v2.0)
- **سرعة فائقة:** التخلي عن Selenium والاعتماد على Pure HTTP Requests مما جعل البرمجة تستغرق ثوانٍ معدودة.
- **خفيف جداً:** يعمل بكفاءة عالية على الأجهزة المصغرة مثل **Orange Pi Zero 3** دون استهلاك للرام أو المعالج.
- **مراقبة حية (Live Stream):** واجهة ويب تفاعلية تعرض خطوات العمل بالميدان (Ping، دمج الآيبي، جلب التوكن، الرفع) سطرًا بسطر باستخدام تقنية الـ SSE.
- **خيارين للعمل:** رفع ملف كونفك جاهز (`XML`) أو برمجة سريعة ويدوية (VLAN + PPPoE).

---

## 🛠️ خارطة الطريق (Roadmap) وإعداد البيئة من الصفر

### 1️⃣ تحديث النظام وتجهيز البيئة الأساسية
بعد تثبيت نظام اللينكس (Armbian / Orange Pi OS) على الأورانج باي، افتح التيرمينال ونفذ:

```bash
# تحديث مستودعات النظام
sudo apt update && sudo apt upgrade -y

# تنصيب بايثون وأداة إدارة الحزم pip
sudo apt install python3 python3-pip python3-venv -y

# تنصيب أدوات الشبكة لإدارة الواي فاي والـ LAN
sudo apt install network-manager wireless-tools -y
````
###2️⃣ تعريف قطعة الواي فاي وبث الـ Hotspot
​لجعل الأورانج باي يبث شبكة لاسلكية تكنك عليها من موبايلك بالميدان بآيبي ثابت (10.42.0.1):

# إنشاء اتصال الهوت سبوت وتحديد الاسم والرمز
```bash
sudo nmcli device wifi hotspot ifname wlan0 ssid "ONU-Tool-Pro" password "ahmed1234"
```

# تعديل الآيبي الافتراضي للشبكة ليكون ثابتاً ومستقراً
```bash
sudo nmcli connection modify Hotspot ipv4.addresses 10.42.0.1/24 ipv4.method manual
```
# إعادة تشغيل الشبكة لتطبيق الإعدادات
```bash
sudo nmcli connection up Hotspot
```
