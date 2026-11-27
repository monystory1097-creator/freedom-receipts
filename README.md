<!DOCTYPE html>index.html
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
  <title>Freedom Limousine — نظام إيصالات الحجز</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700;800&display=swap" rel="stylesheet" />
  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
  <style>
    :root {
      --dark: #1E242B;
      --slate: #2F3842;
      --gold: #C5A059;
      --gold-dark: #9B7A34;
      --cream: #FAF6EC;
      --label: #4B5563;
      --bg: #F3F4F6;
      --whatsapp: #16A34A;
      --whatsapp-hover: #15803D;
    }
    * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Cairo', Tahoma, Arial, sans-serif; }
    body { background: var(--bg); color: var(--dark); min-height: 100vh; padding-bottom: 40px; }

    .topbar {
      background: var(--dark); color: #fff; padding: 14px 18px;
      border-bottom: 3px solid var(--gold); display: flex;
      align-items: center; justify-content: space-between;
      position: sticky; top: 0; z-index: 50; box-shadow: 0 2px 10px rgba(0,0,0,0.15);
    }
    .topbar-brand h1 { font-size: 17px; font-weight: 800; color: var(--gold); line-height: 1.2; }
    .topbar-brand span { font-size: 11.5px; color: #D1D5DB; }
    .btn-settings {
      background: rgba(197,160,89,0.16); color: #F3E5C2; border: 1px solid var(--gold);
      padding: 8px 12px; border-radius: 10px; font-size: 12.5px; font-weight: 700; cursor: pointer;
    }

    .container {
      max-width: 1100px; margin: 18px auto; padding: 0 12px;
      display: grid; grid-template-columns: 1fr 430px; gap: 22px; align-items: start;
    }
    @media (max-width: 940px) { .container { grid-template-columns: 1fr; } }

    .panel {
      background: #fff; border-radius: 16px; padding: 18px;
      box-shadow: 0 4px 18px rgba(0,0,0,0.06); border: 1px solid #E5E7EB;
    }
    .panel-title {
      font-size: 16px; font-weight: 800; margin-bottom: 14px; padding-bottom: 10px;
      border-bottom: 2px solid #F3F4F6; display: flex; align-items: center; justify-content: space-between; gap: 8px;
    }
    .title-btns { display: flex; gap: 6px; }
    .btn-mini {
      background: var(--cream); color: var(--gold-dark); border: 1px solid var(--gold);
      padding: 4px 9px; border-radius: 8px; font-size: 11.5px; font-weight: 700; cursor: pointer;
    }

    .form-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 11px; }
    @media (max-width: 520px) { .form-grid { grid-template-columns: 1fr; } }
    .form-group { display: flex; flex-direction: column; gap: 4px; }
    .form-group.full { grid-column: 1 / -1; }
    label { font-size: 12.5px; font-weight: 700; color: var(--label); }
    input, select, textarea {
      width: 100%; padding: 10px 12px; border: 1.5px solid #D1D5DB; border-radius: 10px;
      font-size: 14px; color: var(--dark); background: #FAFAFA; outline: none;
    }
    input:focus, select:focus, textarea:focus {
      border-color: var(--gold); background: #fff; box-shadow: 0 0 0 3px rgba(197,160,89,0.15);
    }
    textarea { resize: vertical; min-height: 68px; line-height: 1.6; }
    .time-row { display: grid; grid-template-columns: 1fr 1fr 1.15fr; gap: 6px; }
    .hidden { display: none !important; }

    .actions-box { margin-top: 15px; display: flex; flex-direction: column; gap: 10px; }
    .btn-primary-wa {
      width: 100%; background: var(--whatsapp); color: #fff; border: none;
      padding: 13px 16px; border-radius: 12px; font-size: 15px; font-weight: 800;
      cursor: pointer; display: flex; align-items: center; justify-content: center; gap: 8px;
      box-shadow: 0 4px 12px rgba(22,163,74,0.28);
    }
    .btn-primary-wa:active { background: var(--whatsapp-hover); }
    .btn-row { display: grid; grid-template-columns: 1fr 1fr; gap: 9px; }
    .btn-secondary {
      background: var(--dark); color: #fff; border: none; padding: 11px 10px;
      border-radius: 10px; font-size: 12.5px; font-weight: 700; cursor: pointer;
    }
    .btn-outline {
      background: #fff; color: var(--dark); border: 1.5px solid #D1D5DB; padding: 10px 12px;
      border-radius: 10px; font-size: 13px; font-weight: 700; cursor: pointer;
    }

    .preview-wrapper { display: flex; flex-direction: column; align-items: center; }
    .receipt-capture-area {
      width: 100%; max-width: 430px; background: #fff; padding: 14px;
      border-radius: 14px; box-shadow: 0 10px 28px rgba(0,0,0,0.1);
    }
    .receipt-frame {
      border: 1.5px solid #D8C59B; border-radius: 10px;
      padding: 20px 18px 16px; background: #fff;
    }
    .receipt-header { text-align: center; margin-bottom: 14px; }
    .receipt-logo-wrap {
      width: 76px; height: 76px; margin: 0 auto 9px; border-radius: 50%;
      overflow: hidden; border: 2px solid var(--gold); background: var(--dark);
      display: flex; align-items: center; justify-content: center;
    }
    .receipt-logo-wrap img { width: 100%; height: 100%; object-fit: cover; }
    .logo-fallback { color: var(--gold); font-weight: 800; font-size: 21px; }
    .receipt-subtitle { font-size: 12.5px; font-weight: 700; color: var(--gold-dark); }
    .receipt-brand { font-size: 21px; font-weight: 800; color: var(--dark); direction: ltr; unicode-bidi: isolate; }
    .gold-divider { display: flex; align-items: center; justify-content: center; gap: 10px; margin: 10px 0 6px; }
    .gold-divider::before, .gold-divider::after {
      content: ""; flex: 1; height: 1px;
      background: linear-gradient(to left, transparent, #D8C59B, transparent);
    }
    .gold-diamond { width: 7px; height: 7px; background: var(--gold); transform: rotate(45deg); }

    .receipt-rows { width: 100%; margin-top: 4px; }
    .r-row {
      display: flex; justify-content: space-between; align-items: flex-start;
      width: 100%; padding: 7.5px 2px; border-bottom: 1px solid #F3F4F6; gap: 14px;
    }
    .r-row:last-child { border-bottom: none; }
    .r-label { font-size: 13px; font-weight: 600; color: var(--label); white-space: nowrap; flex-shrink: 0; }
    .r-value { font-size: 13.5px; font-weight: 700; color: var(--dark); text-align: left; word-break: break-word; }
    .r-value.ltr { direction: ltr; unicode-bidi: embed; }

    .total-bar {
      margin-top: 13px; background: var(--dark); color: #fff; border-radius: 10px;
      padding: 12px 15px; display: flex; justify-content: space-between; align-items: center;
      border-right: 4px solid var(--gold);
    }
    .total-label { font-size: 14px; font-weight: 700; color: #E5E7EB; }
    .total-amount { display: flex; align-items: baseline; gap: 6px; }
    .total-num { font-size: 21px; font-weight: 800; color: #fff; direction: ltr; unicode-bidi: isolate; }
    .total-curr { font-size: 13px; font-weight: 700; color: var(--gold); }

    .notes-box {
      margin-top: 11px; background: var(--cream);
      border-right: 3.5px solid var(--gold); border-radius: 8px; padding: 9px 11px;
    }
    .notes-title { font-size: 11.5px; font-weight: 800; color: var(--gold-dark); margin-bottom: 2px; }
    .notes-text { font-size: 12px; font-weight: 600; color: #374151; line-height: 1.6; white-space: pre-line; }

    .receipt-footer { margin-top: 13px; text-align: center; padding-top: 10px; border-top: 1px dashed #E5E7EB; }
    .closing-msg { font-size: 12.5px; font-weight: 700; color: var(--dark); margin-bottom: 8px; }
    .contact-line {
      display: inline-flex; align-items: center; justify-content: center; gap: 6px;
      font-size: 12px; font-weight: 800; color: var(--dark); background: #F9FAFB;
      padding: 5px 11px; border-radius: 20px; border: 1px solid #E5E7EB;
    }
    .contact-num { direction: ltr; unicode-bidi: isolate; }

    .modal-backdrop {
      position: fixed; inset: 0; background: rgba(15,23,42,0.72); z-index: 100;
      display: flex; align-items: center; justify-content: center; padding: 14px;
    }
    .modal-card {
      background: #fff; width: 100%; max-width: 460px; border-radius: 16px;
      padding: 18px; max-height: 92vh; overflow-y: auto;
    }
    .modal-head {
      display: flex; justify-content: space-between; align-items: center;
      margin-bottom: 14px; padding-bottom: 10px; border-bottom: 1px solid #E5E7EB;
    }
    .modal-head h2 { font-size: 15.5px; font-weight: 800; }
    .btn-close {
      background: #F3F4F6; border: none; width: 32px; height: 32px;
      border-radius: 8px; font-size: 18px; cursor: pointer;
    }
    .logo-upload-preview { display: flex; align-items: center; gap: 12px; margin-top: 6px; }
    .logo-thumb {
      width: 52px; height: 52px; border-radius: 50%; border: 2px solid var(--gold);
      background: var(--dark); display: flex; align-items: center; justify-content: center;
      color: var(--gold); font-weight: 800; overflow: hidden; flex-shrink: 0;
    }
    .logo-thumb img { width: 100%; height: 100%; object-fit: cover; }

    .fullscreen-overlay {
      position: fixed; inset: 0; background: #fff; z-index: 200; overflow-y: auto;
      display: flex; flex-direction: column; align-items: center; padding: 16px 10px 40px;
    }
    .fs-close-float {
      position: fixed; top: 12px; left: 12px; background: rgba(30,36,43,0.88);
      color: #fff; border: none; padding: 7px 14px; border-radius: 20px;
      font-size: 12px; font-weight: 700; cursor: pointer; z-index: 210;
    }
    .toast {
      position: fixed; bottom: 20px; left: 50%; transform: translateX(-50%);
      background: var(--dark); color: #fff; padding: 10px 16px; border-radius: 10px;
      font-size: 13px; font-weight: 700; border-bottom: 3px solid var(--gold);
      box-shadow: 0 8px 20px rgba(0,0,0,0.25); z-index: 300; text-align: center; max-width: 90vw;
    }
  </style>
</head>
<body>
  <header class="topbar">
    <div class="topbar-brand">
      <h1 id="navBrandName">Freedom Limousine</h1>
      <span>مولّد إيصالات الحجز الرسمي</span>
    </div>
    <button class="btn-settings" id="openSettingsBtn" type="button">⚙️ الإعدادات</button>
  </header>

  <main class="container">
    <section class="panel">
      <div class="panel-title">
        <span>بيانات الرحلة والحجز</span>
        <div class="title-btns">
          <button type="button" class="btn-mini" id="newOrderBtn">✨ حجز جديد</button>
          <button type="button" class="btn-mini" id="regenCodeBtn">🔄 كود</button>
        </div>
      </div>

      <div class="form-grid">
        <div class="form-group">
          <label for="fCode">كود الإيصال</label>
          <input type="text" id="fCode" dir="ltr" />
        </div>

        <div class="form-group">
          <label for="fTripType">نوع الرحلة</label>
          <select id="fTripType">
            <option value="اتجاه واحد">اتجاه واحد</option>
            <option value="ذهاب وعودة">ذهاب وعودة</option>
            <option value="إيجار يومي 8 ساعات">إيجار يومي 8 ساعات</option>
            <option value="إيجار يومي 12 ساعة">إيجار يومي 12 ساعة</option>
          </select>
        </div>

        <div class="form-group">
          <label for="fDate">التاريخ</label>
          <input type="date" id="fDate" />
        </div>

        <div class="form-group">
          <label>وقت التحرك</label>
          <div class="time-row">
            <select id="fHour"></select>
            <select id="fMin">
              <option value="00">00</option>
              <option value="15">15</option>
              <option value="30">30</option>
              <option value="45">45</option>
            </select>
            <select id="fPeriod">
              <option value="مساءً">مساءً</option>
              <option value="صباحاً">صباحاً</option>
            </select>
          </div>
        </div>

        <div class="form-group">
          <label for="fFrom">نقطة البداية</label>
          <input type="text" id="fFrom" value="الإسكندرية" />
        </div>

        <div class="form-group">
          <label for="fTo">نقطة النهاية</label>
          <input type="text" id="fTo" value="مطار القاهرة الدولي" />
        </div>

        <div class="form-group">
          <label for="fClientName">اسم العميل</label>
          <input type="text" id="fClientName" placeholder="الاسم الكامل للعميل" />
        </div>

        <div class="form-group">
          <label for="fClientPhone">رقم تواصل العميل</label>
          <input type="tel" id="fClientPhone" dir="ltr" placeholder="01xxxxxxxxx" />
        </div>

        <div class="form-group full">
          <label for="fClientAddr">عنوان العميل / موقع التحرك</label>
          <input type="text" id="fClientAddr" placeholder="مثال: سموحة / محطة الرمل..." />
        </div>

        <div class="form-group">
          <label for="fPax">عدد الأفراد</label>
          <input type="number" id="fPax" min="1" max="20" value="2" />
        </div>

        <div class="form-group">
          <label for="fBags">عدد الشنط</label>
          <input type="number" id="fBags" min="0" max="25" value="2" />
        </div>

        <div class="form-group">
          <label for="fCarSelect">فئة السيارة</label>
          <select id="fCarSelect">
            <option value="سيدان VIP">سيدان VIP</option>
            <option value="SUV VIP">SUV VIP</option>
            <option value="تويوتا هاي إس الشكل الجديد">تويوتا هاي إس الشكل الجديد</option>
            <option value="custom">كتابة يدوية مخصصة...</option>
          </select>
        </div>

        <div class="form-group hidden" id="customCarWrap">
          <label for="fCarCustom">اكتب فئة/نوع السيارة</label>
          <input type="text" id="fCarCustom" placeholder="مثال: سيدان فاخرة" />
        </div>

        <div class="form-group">
          <label for="fPayMethod">طريقة السداد</label>
          <select id="fPayMethod">
            <option value="نقداً عند الوصول">نقداً عند الوصول</option>
            <option value="إنستاباي">إنستاباي</option>
            <option value="تم السداد">تم السداد</option>
          </select>
        </div>

        <div class="form-group">
          <label for="fPrice">إجمالي التحصيل (جنيه)</label>
          <input type="number" id="fPrice" min="0" step="50" value="1800" dir="ltr" />
        </div>

        <div class="form-group full">
          <label for="fNotes">ملاحظات أسفل الإيصال (قابلة للتعديل أو المسح لكل رحلة)</label>
          <textarea id="fNotes"></textarea>
        </div>
      </div>

      <div class="actions-box">
        <button type="button" class="btn-primary-wa" id="btnShareWA">
          <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
            <path d="M12.031 2C6.51 2 2.02 6.49 2.02 12.01c0 1.76.46 3.48 1.33 4.99L2 22l5.15-1.35a9.97 9.97 0 0 0 4.88 1.27h.01c5.52 0 10.01-4.49 10.01-10.01S17.55 2 12.031 2zm5.82 14.15c-.25.7-1.44 1.33-2 1.41-.51.08-1.17.11-1.89-.12-.44-.14-1-.33-1.72-.64-3.03-1.31-5-4.38-5.15-4.58-.15-.2-1.23-1.64-1.23-3.13s.78-2.22 1.06-2.52c.28-.3.61-.38.81-.38.2 0 .41.01.58.01.19.01.44-.07.69.53.25.6.86 2.1.94 2.25.08.15.13.33.03.53-.1.2-.15.33-.3.51-.15.18-.32.4-.46.53-.15.15-.31.31-.13.62.18.3.8 1.32 1.72 2.14 1.18 1.05 2.18 1.38 2.48 1.53.3.15.48.13.66-.08.18-.2.76-.88.96-1.19.2-.3.41-.25.68-.15.28.1 1.77.83 2.07.98.3.15.51.23.58.35.08.13.08.73-.17 1.43z"/>
          </svg>
          إرسال الإيصال إلى واتساب
        </button>

        <div class="btn-row">
          <button type="button" class="btn-secondary" id="btnDownloadPNG">📥 تحميل كصورة</button>
          <button type="button" class="btn-secondary" id="btnCopyText">📋 نسخ الرسالة</button>
        </div>

        <button type="button" class="btn-outline" id="btnFullscreen">🖼️ عرض بشاشة كاملة (للسكرين شوت)</button>
      </div>
    </section>

    <section class="preview-wrapper">
      <div id="receiptCard" class="receipt-capture-area">
        <div class="receipt-frame">
          <div class="receipt-header">
            <div class="receipt-logo-wrap" id="rLogoWrap"><span class="logo-fallback">FL</span></div>
            <div class="receipt-subtitle">تأكيد حجز</div>
            <div class="receipt-brand" id="rBrandName">Freedom Limousine</div>
            <div class="gold-divider"><span class="gold-diamond"></span></div>
          </div>

          <div class="receipt-rows">
            <div class="r-row"><span class="r-label">كود الإيصال</span><span class="r-value ltr" id="rCode">FL-4795</span></div>
            <div class="r-row"><span class="r-label">التاريخ</span><span class="r-value" id="rDate">—</span></div>
            <div class="r-row"><span class="r-label">الوقت</span><span class="r-value" id="rTime">03:00 مساءً</span></div>
            <div class="r-row"><span class="r-label">نوع الرحلة</span><span class="r-value" id="rTripType">اتجاه واحد</span></div>
            <div class="r-row"><span class="r-label">نقطة البداية</span><span class="r-value" id="rFrom">الإسكندرية</span></div>
            <div class="r-row"><span class="r-label">نقطة النهاية</span><span class="r-value" id="rTo">مطار القاهرة الدولي</span></div>
            <div class="r-row"><span class="r-label">اسم العميل</span><span class="r-value" id="rClientName">—</span></div>
            <div class="r-row"><span class="r-label">عنوان العميل</span><span class="r-value" id="rClientAddr">—</span></div>
            <div class="r-row"><span class="r-label">رقم التواصل</span><span class="r-value ltr" id="rClientPhone">—</span></div>
            <div class="r-row"><span class="r-label">عدد الأفراد</span><span class="r-value" id="rPax">2</span></div>
            <div class="r-row"><span class="r-label">عدد الشنط</span><span class="r-value" id="rBags">2</span></div>
            <div class="r-row"><span class="r-label">فئة السيارة</span><span class="r-value" id="rCar">سيدان VIP</span></div>
            <div class="r-row"><span class="r-label">طريقة السداد</span><span class="r-value" id="rPayMethod">نقداً عند الوصول</span></div>
          </div>

          <div class="total-bar">
            <span class="total-label">إجمالي التحصيل</span>
            <span class="total-amount">
              <span class="total-num" id="rPrice">1,800</span>
              <span class="total-curr">جنيه</span>
            </span>
          </div>

          <div class="notes-box" id="rNotesBox">
            <div class="notes-title">ملاحظات</div>
            <div class="notes-text" id="rNotesText"></div>
          </div>

          <div class="receipt-footer">
            <div class="closing-msg" id="rClosing">يسعدنا ثقتكم، ونتمنى لكم رحلة مريحة وآمنة.</div>
            <div class="contact-line">
              <svg width="15" height="15" viewBox="0 0 24 24" fill="#9B7A34">
                <path d="M12.031 2C6.51 2 2.02 6.49 2.02 12.01c0 1.76.46 3.48 1.33 4.99L2 22l5.15-1.35a9.97 9.97 0 0 0 4.88 1.27h.01c5.52 0 10.01-4.49 10.01-10.01S17.55 2 12.031 2zm5.82 14.15c-.25.7-1.44 1.33-2 1.41-.51.08-1.17.11-1.89-.12-.44-.14-1-.33-1.72-.64-3.03-1.31-5-4.38-5.15-4.58-.15-.2-1.23-1.64-1.23-3.13s.78-2.22 1.06-2.52c.28-.3.61-.38.81-.38.2 0 .41.01.58.01.19.01.44-.07.69.53.25.6.86 2.1.94 2.25.08.15.13.33.03.53-.1.2-.15.33-.3.51-.15.18-.32.4-.46.53-.15.15-.31.31-.13.62.18.3.8 1.32 1.72 2.14 1.18 1.05 2.18 1.38 2.48 1.53.3.15.48.13.66-.08.18-.2.76-.88.96-1.19.2-.3.41-.25.68-.15.28.1 1.77.83 2.07.98.3.15.51.23.58.35.08.13.08.73-.17 1.43z"/>
              </svg>
              <span>للتواصل والحجز (واتساب):</span>
              <span class="contact-num" id="rCompanyPhone">01044204747</span>
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>

  <!-- Settings Modal -->
  <div class="modal-backdrop hidden" id="settingsModal">
    <div class="modal-card">
      <div class="modal-head">
        <h2>⚙️ إعدادات الإيصال والصلاحيات</h2>
        <button class="btn-close" id="closeSettingsBtn" type="button">×</button>
      </div>
      <div class="form-grid" style="grid-template-columns:1fr;">
        <div class="form-group">
          <label>شعار الشركة (اللوجو)</label>
          <div class="logo-upload-preview">
            <div class="logo-thumb" id="sLogoPreview">FL</div>
            <div style="flex:1; display:flex; flex-direction:column; gap:6px;">
              <input type="file" id="sLogoFile" accept="image/*" style="padding:6px; font-size:12px;" />
              <button type="button" class="btn-outline" id="removeLogoBtn" style="padding:5px 8px; font-size:12px;">إزالة اللوجو</button>
            </div>
          </div>
        </div>
        <div class="form-group">
          <label for="sBrandName">اسم الشركة</label>
          <input type="text" id="sBrandName" dir="ltr" />
        </div>
        <div class="form-group">
          <label for="sPhone">رقم الهاتف / الواتساب الرسمي</label>
          <input type="text" id="sPhone" dir="ltr" />
        </div>
        <div class="form-group">
          <label for="sDefaultNotes">الملاحظة الثابتة الافتراضية أسفل الإيصال</label>
          <textarea id="sDefaultNotes"></textarea>
        </div>
        <div class="form-group">
          <label for="sClosing">الجملة الختامية الافتراضية</label>
          <input type="text" id="sClosing" />
        </div>
        <button type="button" class="btn-primary-wa" id="saveSettingsBtn" style="background:var(--dark); margin-top:6px;">
          💾 حفظ الإعدادات بشكل دائم
        </button>
      </div>
    </div>
  </div>

  <!-- Fullscreen Modal -->
  <div class="fullscreen-overlay hidden" id="fsOverlay">
    <button type="button" class="fs-close-float" id="closeFsBtn">✕ إغلاق</button>
    <div id="fsContainer" style="width:100%; max-width:430px; margin-top:26px;"></div>
  </div>

  <div class="toast hidden" id="toast"></div>

  <script>
    const STORAGE_KEY = 'freedom_limo_receipt_settings_v1';
    const DEFAULT_SETTINGS = {
      brandName: 'Freedom Limousine',
      phone: '01044204747',
      defaultNotes: 'السعر شامل كارتة الطريق الصحراوي ورسوم دخول المطار، ولا يشمل طريق الضبعة أو كوبري تحيا مصر.',
      closing: 'يسعدنا ثقتكم، ونتمنى لكم رحلة مريحة وآمنة.',
      logoDataUrl: ''
    };

    let settings = loadSettings();
    let tempLogoDataUrl = settings.logoDataUrl;

    function loadSettings() {
      try {
        const s = localStorage.getItem(STORAGE_KEY);
        if (s) return { ...DEFAULT_SETTINGS, ...JSON.parse(s) };
      } catch (e) {}
      return { ...DEFAULT_SETTINGS };
    }

    function saveSettingsToStorage(obj) {
      try { localStorage.setItem(STORAGE_KEY, JSON.stringify(obj)); }
      catch (e) { showToast('تعذّر حفظ الصورة لكبر حجمها، جرّب صورة أصغر'); }
    }

    function generateCode() { return 'FL-' + Math.floor(1000 + Math.random() * 9000); }

    function showToast(msg) {
      const t = document.getElementById('toast');
      t.textContent = msg;
      t.classList.remove('hidden');
      clearTimeout(window._tt);
      window._tt = setTimeout(() => t.classList.add('hidden'), 3200);
    }

    const fHour = document.getElementById('fHour');
    for (let h = 1; h <= 12; h++) {
      const opt = document.createElement('option');
      const v = String(h).padStart(2, '0');
      opt.value = v; opt.textContent = v;
      if (h === 3) opt.selected = true;
      fHour.appendChild(opt);
    }

    const AR_DAYS = ['الأحد','الإثنين','الثلاثاء','الأربعاء','الخميس','الجمعة','السبت'];
    const AR_MONTHS = ['يناير','فبراير','مارس','أبريل','مايو','يونيو','يوليو','أغسطس','سبتمبر','أكتوبر','نوفمبر','ديسمبر'];

    function formatArabicDate(iso) {
      if (!iso) return '—';
      const p = iso.split('-');
      if (p.length !== 3) return iso;
      const d = new Date(Number(p[0]), Number(p[1]) - 1, Number(p[2]));
      return isNaN(d.getTime()) ? iso : `${AR_DAYS[d.getDay()]}، ${d.getDate()} ${AR_MONTHS[d.getMonth()]} ${d.getFullYear()}`;
    }

    function formatPrice(val) {
      const n = Number(val);
      return (isNaN(n) || val === '') ? '0' : n.toLocaleString('en-US');
    }

    function applySettingsUI() {
      document.getElementById('navBrandName').textContent = settings.brandName;
      document.getElementById('rBrandName').textContent = settings.brandName;
      document.getElementById('rCompanyPhone').textContent = settings.phone;
      document.getElementById('rClosing').textContent = settings.closing;
      document.getElementById('rLogoWrap').innerHTML = settings.logoDataUrl
        ? `<img src="${settings.logoDataUrl}" alt="Logo" />`
        : `<span class="logo-fallback">FL</span>`;
    }

    function getSelectedCar() {
      const sel = document.getElementById('fCarSelect').value;
      return sel === 'custom' ? (document.getElementById('fCarCustom').value.trim() || 'سيارة VIP') : sel;
    }

    function updatePreview() {
      document.getElementById('rCode').textContent = document.getElementById('fCode').value.trim() || 'FL-0000';
      document.getElementById('rDate').textContent = formatArabicDate(document.getElementById('fDate').value);
      document.getElementById('rTime').textContent = `${document.getElementById('fHour').value}:${document.getElementById('fMin').value} ${document.getElementById('fPeriod').value}`;
      document.getElementById('rTripType').textContent = document.getElementById('fTripType').value;
      document.getElementById('rFrom').textContent = document.getElementById('fFrom').value.trim() || '—';
      document.getElementById('rTo').textContent = document.getElementById('fTo').value.trim() || '—';
      document.getElementById('rClientName').textContent = document.getElementById('fClientName').value.trim() || '—';
      document.getElementById('rClientAddr').textContent = document.getElementById('fClientAddr').value.trim() || '—';
      document.getElementById('rClientPhone').textContent = document.getElementById('fClientPhone').value.trim() || '—';
      document.getElementById('rPax').textContent = document.getElementById('fPax').value || '1';
      document.getElementById('rBags').textContent = document.getElementById('fBags').value || '0';
      document.getElementById('rCar').textContent = getSelectedCar();
      document.getElementById('rPayMethod').textContent = document.getElementById('fPayMethod').value;
      document.getElementById('rPrice').textContent = formatPrice(document.getElementById('fPrice').value);

      const notes = document.getElementById('fNotes').value.trim();
      const box = document.getElementById('rNotesBox');
      if (notes) { box.classList.remove('hidden'); document.getElementById('rNotesText').textContent = notes; }
      else { box.classList.add('hidden'); }
    }

    // Init
    document.getElementById('fCode').value = generateCode();
    const now = new Date();
    document.getElementById('fDate').value = `${now.getFullYear()}-${String(now.getMonth()+1).padStart(2,'0')}-${String(now.getDate()).padStart(2,'0')}`;
    document.getElementById('fNotes').value = settings.defaultNotes;
    applySettingsUI();
    updatePreview();

    ['fCode','fTripType','fDate','fHour','fMin','fPeriod','fFrom','fTo','fClientName','fClientPhone','fClientAddr','fPax','fBags','fCarSelect','fCarCustom','fPayMethod','fPrice','fNotes']
      .forEach(id => {
        document.getElementById(id).addEventListener('input', updatePreview);
        document.getElementById(id).addEventListener('change', updatePreview);
      });

    document.getElementById('fCarSelect').addEventListener('change', function() {
      const w = document.getElementById('customCarWrap');
      if (this.value === 'custom') { w.classList.remove('hidden'); document.getElementById('fCarCustom').focus(); }
      else { w.classList.add('hidden'); }
      updatePreview();
    });

    document.getElementById('regenCodeBtn').addEventListener('click', () => {
      document.getElementById('fCode').value = generateCode();
      updatePreview();
      showToast('تم إنشاء كود جديد');
    });

    document.getElementById('newOrderBtn').addEventListener('click', () => {
      document.getElementById('fCode').value = generateCode();
      document.getElementById('fClientName').value = '';
      document.getElementById('fClientPhone').value = '';
      document.getElementById('fClientAddr').value = '';
      document.getElementById('fNotes').value = settings.defaultNotes;
      updatePreview();
      showToast('تم تجهيز النموذج لحجز جديد');
    });

    // Settings
    const settingsModal = document.getElementById('settingsModal');
    function updateSettingsLogoPreview(url) {
      document.getElementById('sLogoPreview').innerHTML = url ? `<img src="${url}" alt="Logo" />` : 'FL';
    }
    document.getElementById('openSettingsBtn').addEventListener('click', () => {
      document.getElementById('sBrandName').value = settings.brandName;
      document.getElementById('sPhone').value = settings.phone;
      document.getElementById('sDefaultNotes').value = settings.defaultNotes;
      document.getElementById('sClosing').value = settings.closing;
      tempLogoDataUrl = settings.logoDataUrl;
      updateSettingsLogoPreview(tempLogoDataUrl);
      document.getElementById('sLogoFile').value = '';
      settingsModal.classList.remove('hidden');
    });
    document.getElementById('closeSettingsBtn').addEventListener('click', () => settingsModal.classList.add('hidden'));

    document.getElementById('sLogoFile').addEventListener('change', (e) => {
      const file = e.target.files[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onload = (ev) => {
        const img = new Image();
        img.onload = () => {
          const c = document.createElement('canvas');
          const max = 320;
          let w = img.width, h = img.height;
          if (w > max || h > max) {
            if (w > h) { h = Math.round(h * max / w); w = max; }
            else { w = Math.round(w * max / h); h = max; }
          }
          c.width = w; c.height = h;
          c.getContext('2d').drawImage(img, 0, 0, w, h);
          tempLogoDataUrl = c.toDataURL('image/png');
          updateSettingsLogoPreview(tempLogoDataUrl);
        };
        img.src = ev.target.result;
      };
      reader.readAsDataURL(file);
    });

    document.getElementById('removeLogoBtn').addEventListener('click', () => {
      tempLogoDataUrl = '';
      updateSettingsLogoPreview('');
    });

    document.getElementById('saveSettingsBtn').addEventListener('click', () => {
      const oldNote = settings.defaultNotes;
      settings = {
        brandName: document.getElementById('sBrandName').value.trim() || DEFAULT_SETTINGS.brandName,
        phone: document.getElementById('sPhone').value.trim() || DEFAULT_SETTINGS.phone,
        defaultNotes: document.getElementById('sDefaultNotes').value.trim(),
        closing: document.getElementById('sClosing').value.trim() || DEFAULT_SETTINGS.closing,
        logoDataUrl: tempLogoDataUrl
      };
      saveSettingsToStorage(settings);
      applySettingsUI();
      if (document.getElementById('fNotes').value.trim() === oldNote) {
        document.getElementById('fNotes').value = settings.defaultNotes;
      }
      updatePreview();
      settingsModal.classList.add('hidden');
      showToast('تم حفظ الإعدادات واللوجو بنجاح ✓');
    });

    // Export
    async function renderReceiptBlob() {
      if (typeof html2canvas === 'undefined') throw new Error('تأكد من الاتصال بالإنترنت أو استخدم زر الشاشة الكاملة');
      if (document.fonts && document.fonts.ready) await document.fonts.ready;
      const canvas = await html2canvas(document.getElementById('receiptCard'), {
        scale: 3, useCORS: true, backgroundColor: '#ffffff', logging: false
      });
      return new Promise((res, rej) => canvas.toBlob(b => b ? res(b) : rej(new Error('تعذّر إنشاء الصورة')), 'image/png', 1.0));
    }

    function getFileName() {
      const code = (document.getElementById('fCode').value.trim() || 'Receipt').replace(/[^a-zA-Z0-9_-]/g, '');
      return `Freedom-Receipt-${code}.png`;
    }

    function downloadBlob(blob, filename) {
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url; a.download = filename;
      document.body.appendChild(a); a.click(); document.body.removeChild(a);
      setTimeout(() => URL.revokeObjectURL(url), 1500);
    }

    function formatWaPhone(raw) {
      const d = (raw || '').replace(/\D/g, '');
      return (d.startsWith('01') && d.length === 11) ? '2' + d : d;
    }

    function buildWhatsAppText() {
      const notes = document.getElementById('fNotes').value.trim();
      let txt = `تم تأكيد حجز حضرتك بنجاح في *${settings.brandName}* (مرفق إيصال الحجز الرسمي).\n\n`;
      txt += `• *كود الحجز:* ${document.getElementById('rCode').textContent}\n`;
      txt += `• *الموعد:* ${document.getElementById('rDate').textContent} — ${document.getElementById('rTime').textContent}\n`;
      txt += `• *المسار:* من ${document.getElementById('rFrom').textContent} إلى ${document.getElementById('rTo').textContent} (${document.getElementById('rTripType').textContent})\n`;
      txt += `• *الفئة:* ${document.getElementById('rCar').textContent}\n`;
      txt += `• *إجمالي التحصيل:* ${document.getElementById('rPrice').textContent} جنيه (${document.getElementById('rPayMethod').textContent})\n`;
      if (notes) txt += `\n*ملاحظة:* ${notes}\n`;
      txt += `\nسيتم إرسال بيانات الكابتن والسيارة قبل موعد رحلتك بوقت كافٍ.\n${settings.closing}`;
      return txt;
    }

    document.getElementById('btnShareWA').addEventListener('click', async () => {
      try {
        showToast('جاري تجهيز صورة الإيصال...');
        const blob = await renderReceiptBlob();
        const filename = getFileName();
        const file = new File([blob], filename, { type: 'image/png' });
        if (navigator.canShare && navigator.canShare({ files: [file] })) {
          await navigator.share({ files: [file], title: `إيصال حجز ${settings.brandName}`, text: buildWhatsAppText() });
          return;
        }
        downloadBlob(blob, filename);
        const phone = formatWaPhone(document.getElementById('fClientPhone').value);
        showToast('تم حفظ صورة الإيصال! أرفقها الآن في محادثة العميل');
        if (phone) setTimeout(() => window.open(`https://wa.me/${phone}`, '_blank'), 700);
      } catch (err) {
        if (err && err.name === 'AbortError') return;
        showToast(err.message || 'حدث خطأ أثناء إنشاء الصورة');
      }
    });

    document.getElementById('btnDownloadPNG').addEventListener('click', async () => {
      try {
        showToast('جاري حفظ صورة الإيصال...');
        downloadBlob(await renderReceiptBlob(), getFileName());
        showToast('تم تحميل الإيصال بنجاح ✓');
      } catch (err) { showToast(err.message || 'تعذّر تحميل الصورة'); }
    });

    document.getElementById('btnCopyText').addEventListener('click', async () => {
      const txt = buildWhatsAppText();
      try { await navigator.clipboard.writeText(txt); }
      catch (e) {
        const ta = document.createElement('textarea');
        ta.value = txt; document.body.appendChild(ta); ta.select();
        document.execCommand('copy'); document.body.removeChild(ta);
      }
      showToast('تم نسخ رسالة تأكيد الواتساب ✓');
    });

    const fsOverlay = document.getElementById('fsOverlay');
    const fsContainer = document.getElementById('fsContainer');
    document.getElementById('btnFullscreen').addEventListener('click', () => {
      fsContainer.innerHTML = '';
      const clone = document.getElementById('receiptCard').cloneNode(true);
      clone.removeAttribute('id'); clone.style.boxShadow = 'none';
      fsContainer.appendChild(clone);
      fsOverlay.classList.remove('hidden');
    });
    document.getElementById('closeFsBtn').addEventListener('click', () => fsOverlay.classList.add('hidden'));
  </script>
</body>
</html>

