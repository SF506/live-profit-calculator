# Live Profit Calculator — a Claude skill

**English** · [العربية](#العربية)

A skill for Claude that builds a live profit calculator page for any product or service. You answer a few questions about your price and costs, and Claude builds a page where every number can be changed and the results update right away.

**What the page shows**
- Profit per sale, after every cost
- Monthly profit, after monthly costs and ads
- How many sales a month you need to break even
- A whole batch over a set number of months
- Which number affects your profit most
- An ad planner and Worst / Base / Best scenarios
- Arabic and English, dark and light

## How to add it to Claude

1. Download **`live-profit-calculator.zip`** from this page (click the file, then **Download**).
2. Open **claude.ai** and go to **Customize → Skills**.
3. Upload the ZIP and turn the skill on.
4. Start a new chat and use one of the prompts below.

Skills need code execution turned on in your Claude settings. Uploading may need a computer the first time; after that the skill works on your phone too.

## Starting prompt

Answering the setup questions up front means fewer back-and-forth questions. Copy this, fill in the blanks, and delete any line that doesn't apply:

```
Use /live-profit-calculator for my business.

Product: [what you sell] — one unit is called a [unit]
Price: [price] [currency], VAT included? [yes/no]
Unit cost: item [price] + shipping [per unit, or per kg + min weight + weight per unit] + customs/taxes [amount]
Batch: [units] units for [total cost]
Per-order costs:
- Payment fee: [fixed] + [%] charged on [what]
- Discount code: [%] off, used by [%] of orders
- Packaging: [amount]
- Shipping: customer pays [amount], I pay [amount]
- Commission: [% or none / add later]
Deduct in this order: [discount → fee → ...]
Monthly costs: [platform], [software], [other]
Ad budget: [amount] per month
Sales guess: [units] per month
Batch period: sell one batch in [months] months
Goal: [monthly revenue / profit target]
Bundles: [none / list them]
Returns: [none / % and cost]
Language: [Arabic / English / both]
```

**Short version, for a quick start:**

```
Use /live-profit-calculator for [product]. Price [X], unit cost [Y], monthly costs [Z]. Ask me for the rest.
```

Claude repeats every number back and waits for your "yes" before building, so you can fix anything then.

---

<div dir="rtl">

## العربية

# حاسبة الأرباح المباشرة — مهارة لـ Claude

مهارة تخلّي Claude يسوّي لك صفحة تحسب أرباحك لأي منتج أو خدمة. تجاوب على كم سؤال عن سعرك وتكاليفك، ويطلع لك Claude صفحة كل رقم فيها تقدر تغيّره، والنتايج تتحدث على طول.

**وش تعطيك الصفحة؟**
- ربحك من كل بيعة، بعد ما تنخصم كل التكاليف
- ربحك بالشهر، بعد المصاريف الشهرية والإعلانات
- كم بيعة تحتاج بالشهر عشان ما تخسر (نقطة التعادل)
- حسبة الدفعة كاملة على عدد شهور تحدده أنت
- أي رقم يأثر على ربحك أكثر من غيره
- مخطط للإعلانات، وثلاث حالات: الأسوأ، الأساس، الأفضل
- عربي وإنجليزي، وثيم داكن وفاتح

## كيف تضيفها لـ Claude

1. نزّل ملف **`live-profit-calculator.zip`** من هالصفحة (اضغط على الملف، بعدين **Download**).
2. افتح **claude.ai** وروح لـ **Customize ← Skills**.
3. ارفع الملف وفعّل المهارة.
4. افتح محادثة جديدة واستخدم وحدة من الأوامر اللي تحت.

ترا المهارات تحتاج خاصية تشغيل الأكواد (Code execution) تكون مفعّلة في إعدادات Claude. أول مرة ترفع فيها المهارة يمكن تحتاج كمبيوتر، وبعدها تشتغل معك من الجوال عادي.

## أمر البداية

إذا عطيت Claude المعلومات من أول رسالة، بيقلّ عليك السؤال والجواب. انسخ هذا، عبّي الفراغات، واحذف أي سطر ما يخصك:

```
Use /live-profit-calculator لمشروعي.

المنتج: [وش تبيع] — الوحدة اسمها [حبة / قطعة / جلسة...]
السعر: [السعر] [العملة]، شامل الضريبة؟ [إيه / لا]
تكلفة الوحدة: سعر المنتج [المبلغ] + الشحن [للحبة، أو للكيلو + أقل وزن + وزن الحبة] + الجمارك/الضرايب [المبلغ]
الدفعة: [العدد] حبة بـ [التكلفة الكاملة]
تكاليف كل طلب:
- رسوم الدفع: [مبلغ ثابت] + [%] على [وش]
- كود الخصم: [%] خصم، يستخدمه [%] من الطلبات
- التغليف: [المبلغ]
- الشحن: العميل يدفع [المبلغ]، وأنا أدفع [المبلغ]
- العمولة: [% أو ما فيه / بضيفها بعدين]
ترتيب الخصم: [الخصم ← الرسوم ← ...]
المصاريف الشهرية: [المنصة]، [البرامج]، [غيرها]
ميزانية الإعلانات: [المبلغ] بالشهر
توقع المبيعات: [العدد] بالشهر
مدة الدفعة: أبي أخلّص الدفعة في [عدد] شهور
الهدف: [إيراد / ربح شهري]
الباقات: [ما فيه / اكتبها]
المرتجعات: [ما فيه / النسبة والتكلفة]
اللغة: [عربي / إنجليزي / الثنين]
```

**نسخة مختصرة، إذا تبي تبدأ بسرعة:**

```
Use /live-profit-calculator لـ [المنتج]. السعر [X]، تكلفة الحبة [Y]، المصاريف الشهرية [Z]. واسألني عن الباقي.
```

Claude بيرجع لك كل الأرقام ويستنى تقول "إيه" قبل ما يبني الصفحة، فتقدر تعدّل أي شي وقتها.

</div>

---
Made by Sattam Al-Hussain · سوّاها سطام الحسين
