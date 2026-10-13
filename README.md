# RecMind فارسی: توصیه‌گر عامل‌محور برای تجارت الکترونیک

**پروژه پایان‌نامه کارشناسی ارشد هوش مصنوعی** | Persian Agentic Recommendation from E-commerce Reviews

[فارسی](#فارسی) · [English](#english)

## فارسی

### معرفی

این مخزن نمونه‌ای پژوهشی از سیستم توصیه‌گر عامل‌محور مبتنی بر مدل زبانی بزرگ برای نظرات فارسی تجارت الکترونیک است. عامل از تاریخچه بازخورد کاربر ترجیحات ضمنی مانند حساسیت به دوام، کیفیت ساخت، قیمت یا سهولت استفاده را استنباط می‌کند؛ سپس پنج محصول کاندیدا را بر اساس شواهد موجود رتبه‌بندی و انتخاب خود را توضیح می‌دهد. طراحی از ایده‌های مقاله RecMind الهام گرفته است و بازتولید کامل مقاله نیست.

### معماری سیستم

1. خواندن فایل محلی keifiat.xlsx و نگاشت ستون‌های شناسه کاربر و محصول، دسته‌بندی، توصیه، نظر، مزایا و معایب.
2. پاک‌سازی متن و برچسب‌ها و ساخت تاریخچه تعامل و مجموعه کاندیداها.
3. ارسال تاریخچه و اطلاعات محصولات به یک مدل سازگار با API نوع OpenAI برای استنباط ترجیحات و رتبه‌بندی.
4. اعتبارسنجی خروجی مدل، نگهداری نتایج ارزیابی و محاسبه معیارهای HR@K، MRR و NDCG@5.

### داده‌ها

داده خام Excel و CSV در مخزن Git نگهداری نمی‌شود. فایل keifiat.xlsx، که در پروژه به‌عنوان دارای ۱۰۰٬۰۰۰ رکورد معرفی شده، باید جداگانه از مخزن عمومی [farshadnp/DigiKalaDataSet](https://github.com/farshadnp/DigiKalaDataSet) دریافت و در data/keifiat.xlsx قرار گیرد. برای مسیر دیگر، متغیر DIGIKALA_DATA_PATH را تنظیم کنید.

فایل‌های benchmarks/test_benchmark.json و benchmarks/agent_evaluation_results.json شامل نمونه‌ها و نتایج ارزیابی هستند و متن نظر کاربران را در بر دارند. استفاده از آن‌ها باید تابع شرایط منبع داده و الزامات حریم خصوصی باشد.

### نتایج ارزیابی گزارش‌شده

اعداد زیر نتایج گزارش‌شده پروژه برای ۴۰ کاربر با نمونه‌گیری متوازن بر اساس دسته‌بندی هستند. بیس‌لاین تصادفی از رتبه‌بندی پنج گزینه تشکیل شده است.

| معیار | عامل | بیس‌لاین تصادفی | بهبود نسبی |
|---|---:|---:|---:|
| تعداد نمونه | ۴۰ | ۴۰ | — |
| HR@1 | 0.3750 | 0.2000 | +87.50% |
| HR@3 | 0.8000 | 0.6000 | +33.33% |
| HR@5 | 1.0000 | 1.0000 | — |
| MRR | 0.6058 | 0.4567 | +32.66% |
| NDCG@5 | 0.7042 | 0.5897 | +19.41% |

این نتایج توصیفی‌اند و به نمونه کاربران، مدل، پرامپت و ساخت کاندیداها وابسته‌اند؛ به‌تنهایی معناداری آماری یا تعمیم‌پذیری را اثبات نمی‌کنند.

### نصب و راه‌اندازی

~~~bash
python -m venv .venv
~~~

در Windows PowerShell:

~~~powershell
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
$env:OPENAI_API_KEY = "your-api-key"
$env:OPENAI_BASE_URL = "https://api.gapgpt.app/v1"
$env:DIGIKALA_DATA_PATH = "data/keifiat.xlsx"
jupyter notebook notebooks/recmind_agentic_recommendation.ipynb
~~~

در macOS یا Linux، محیط مجازی را با source .venv/bin/activate فعال و وابستگی‌ها را با pip install -r requirements.txt نصب کنید. OPENAI_API_KEY و OPENAI_BASE_URL را در محیط فرایند تنظیم کنید. کلید API را در کد یا فایل‌های تحت Git قرار ندهید. فراخوانی API ممکن است هزینه داشته باشد. اجرای نوت‌بوک می‌تواند فایل‌های JSON نتایج را بازنویسی کند؛ تغییرات را پیش از ثبت بررسی کنید.

### ساختار مخزن

~~~text
.gitignore
README.md
requirements.txt
benchmarks/
  test_benchmark.json
  agent_evaluation_results.json
notebooks/
  recmind_agentic_recommendation.ipynb
~~~

### ارجاعات

- Wang, Y., Jiang, Z., Chen, Z., Yang, F., Zhou, Y., Cho, E., Fan, X., Huang, X., Lu, Y., & Yang, Y. (2024). “RecMind: Large Language Model Powered Agent For Recommendation.” Findings of the Association for Computational Linguistics: NAACL 2024, pp. 4351–4364. شناسه مقاله در arXiv: **2308.14296**.
- مخزن داده دیجی‌کالا: [farshadnp/DigiKalaDataSet](https://github.com/farshadnp/DigiKalaDataSet).
- شناسه **arXiv:2402.15235v3** مربوط به مقاله دیگری با عنوان “MACRec: A Multi-Agent Collaboration Framework for Recommendation” است، نه مقاله RecMind.

## English

### Overview

This repository is a research prototype of an LLM-powered agentic recommender for Persian e-commerce reviews. It infers latent user preferences from review history, ranks five candidate products using the supplied evidence, and explains its choice. The design is inspired by RecMind; this project is not a full reproduction of that paper.

### Architecture

The notebook loads a local DigiKala review workbook, cleans recommendation labels and Persian text fields, forms user histories and candidate sets, queries an OpenAI-compatible chat completion endpoint, validates the ranking, and computes HR@K, MRR, and NDCG@5.

### Data

Raw Excel and CSV files are excluded from Git. Obtain keifiat.xlsx separately from [farshadnp/DigiKalaDataSet](https://github.com/farshadnp/DigiKalaDataSet), place it at data/keifiat.xlsx, or set DIGIKALA_DATA_PATH. The two JSON files under benchmarks contain review text and should be handled under the source dataset's terms and applicable privacy requirements.

### Reported evaluation

The supplied project results use 40 category-balanced users. These are descriptive results and depend on the sampled users, model, prompt, and candidate construction.

| Metric | Agent | Random baseline | Relative lift |
|---|---:|---:|---:|
| Samples | 40 | 40 | — |
| HR@1 | 0.3750 | 0.2000 | +87.50% |
| HR@3 | 0.8000 | 0.6000 | +33.33% |
| HR@5 | 1.0000 | 1.0000 | — |
| MRR | 0.6058 | 0.4567 | +32.66% |
| NDCG@5 | 0.7042 | 0.5897 | +19.41% |

### Setup

Install dependencies with pip install -r requirements.txt. Set OPENAI_API_KEY and OPENAI_BASE_URL=https://api.gapgpt.app/v1, optionally set DIGIKALA_DATA_PATH, then run the notebook at notebooks/recmind_agentic_recommendation.ipynb. API calls may incur provider charges.

### References

Wang et al. (2024), “RecMind: Large Language Model Powered Agent For Recommendation,” Findings of NAACL 2024, pp. 4351–4364, arXiv:2308.14296. The identifier arXiv:2402.15235v3 is MACRec, a separate paper. Dataset repository: farshadnp/DigiKalaDataSet.
