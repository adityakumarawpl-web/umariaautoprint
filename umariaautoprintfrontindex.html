<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Auto-Print Kiosk</title>
  
  <!-- PDF page count automatic karne ke liye lightweight PDF.js library -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
  <!-- Razorpay Checkout library payment popup ke liye -->
  <script src="https://checkout.razorpay.com/v1/checkout.js"></script>

  <style>
    /* Mobile-first UI layout jo 1 second ke andar load hoga */
    * { box-sizing: border-box; }
    body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; margin: 0; padding: 12px; background: #f0f2f5; color: #222; }
    .container { max-width: 440px; margin: auto; background: #fff; border-radius: 14px; padding: 18px; box-shadow: 0 4px 15px rgba(0,0,0,0.06); }
    
    /* Bhasha chunne ka section (Hindi/English) */
    .lang-switcher { display: flex; justify-content: flex-end; gap: 8px; margin-bottom: 12px; }
    .lang-btn { border: 1px solid #1a73e8; background: #fff; color: #1a73e8; border-radius: 16px; padding: 4px 12px; font-size: 0.82rem; font-weight: bold; cursor: pointer; }
    .lang-btn.active { background: #1a73e8; color: #fff; }

    h2 { font-size: 1.25rem; color: #0d47a1; text-align: center; margin: 0 0 16px 0; }
    .form-group { margin-bottom: 14px; }
    label { display: block; font-size: 0.86rem; font-weight: 600; margin-bottom: 5px; }
    input[type="file"], select { width: 100%; padding: 10px; border: 1px solid #ccc; border-radius: 8px; font-size: 0.92rem; }
    
    /* Paper jam warning box: 5 page se jyada hone par user ko instruction */
    .warning-box { display: none; background: #fff3cd; border: 1px solid #ffeeba; color: #856404; padding: 10px; border-radius: 8px; font-size: 0.85rem; margin-top: 10px; line-height: 1.4; }
    
    /* Billing calculation box */
    .price-box { background: #e8f0fe; border: 1px solid #b3d1ff; padding: 12px; border-radius: 8px; text-align: center; margin: 15px 0; }
    .price-text { font-size: 1.25rem; font-weight: bold; color: #0d47a1; }
    
    /* Main payment button */
    .pay-btn { width: 100%; padding: 14px; background: #28a745; color: white; border: none; border-radius: 8px; font-size: 1.05rem; font-weight: bold; cursor: pointer; }
    .pay-btn:disabled { background: #94d3a2; cursor: not-allowed; }

    /* Queue & printing status screen */
    .status-panel { display: none; background: #fdfdfd; border: 1.5px solid #28a745; border-radius: 10px; padding: 16px; text-align: center; margin-top: 14px; }
    .token-display { font-size: 1.2rem; font-weight: bold; background: #28a745; color: white; padding: 6px 14px; border-radius: 20px; display: inline-block; margin: 8px 0; }
    .queue-info { font-size: 0.92rem; color: #333; line-height: 1.5; }
    .countdown-timer { font-size: 1.1rem; font-weight: bold; color: #d93025; margin-top: 6px; }

    /* Footer links: Contact, Refund, Terms */
    .footer-links { text-align: center; margin-top: 20px; border-top: 1px solid #eee; padding-top: 12px; font-size: 0.78rem; color: #666; }
    .footer-links a { color: #1a73e8; text-decoration: none; margin: 0 5px; }

    /* Modal / Popups for rules and support */
    .modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); justify-content: center; align-items: center; padding: 15px; }
    .modal-content { background: white; padding: 18px; border-radius: 10px; max-width: 400px; width: 100%; font-size: 0.85rem; line-height: 1.5; }
    .modal-close { background: #0d47a1; color: white; border: none; border-radius: 6px; padding: 6px 14px; cursor: pointer; float: right; margin-top: 10px; }
  </style>
</head>
<body>

<div class="container">
  <!-- Bhasha chunne ke buttons -->
  <div class="lang-switcher">
    <button class="lang-btn active" onclick="changeLanguage('hi')">हिंदी</button>
    <button class="lang-btn" onclick="changeLanguage('en')">English</button>
  </div>

  <h2 id="ui-title">उमरिया कलेक्ट्रेट ऑटो-प्रिंटिंग</h2>

  <div id="upload-screen">
    <!-- File Select Input (Direct phone gallery ya document storage access) -->
    <div class="form-group">
      <label id="lbl-file">फ़ाइल चुनें जिसे प्रिंट करना चाहते हैं (PDF/Image):</label>
      <input type="file" id="fileInput" accept=".pdf,image/png,image/jpeg" onchange="handleFileSelect(event)">
    </div>

    <!-- Print Type -->
    <div class="form-group">
      <label id="lbl-color">प्रिंट का प्रकार (Print Type):</label>
      <select id="colorOption" onchange="recalculatePrice()">
        <option value="bw">ब्लैक एंड व्हाइट (B&W)</option>
        <option value="color">कलर (Color)</option>
      </select>
    </div>

    <!-- Side Type -->
    <div class="form-group">
      <label id="lbl-side">प्रिंटिंग साइड (Sides):</label>
      <select id="sideOption" onchange="recalculatePrice()">
        <option value="single">एक तरफ (Single Side)</option>
        <option value="duplex">दोनों तरफ (Duplex / Two-Sided)</option>
      </select>
    </div>

    <!-- Machine jam se bachne ke liye Alert Note -->
    <div id="jamWarning" class="warning-box">
      ⚠️ <b>महत्वपूर्ण निर्देश:</b> आपकी फ़ाइल में 5 से अधिक पृष्ठ हैं। प्रिंटर में पेपर फंसने से बचाने के लिए जैसे ही 5 पेज बाहर निकलें, उन्हें ट्रे से हटा लें और शेष पेज निकलने का इंतज़ार करें।
    </div>

    <!-- Page count and billing summary -->
    <div class="price-box">
      <span id="pageCountDisplay" style="font-size: 0.88rem; display: block; color: #555;">कुल पृष्ठ: 0</span>
      <div class="price-text" id="priceDisplay">कुल शुल्क: ₹0.00</div>
    </div>

    <!-- Payment Trigger Button -->
    <button type="button" class="pay-btn" id="payBtn" disabled onclick="initiateRazorpayPayment()">
      UPI / कार्ड से भुगतान करें
    </button>
  </div>

  <!-- Real-time Queue & Print Status Panel -->
  <div id="statusPanel" class="status-panel">
    <h3 style="margin: 0; color: #28a745; font-size: 1.1rem;" id="q-status-title">भुगतान सफल रहा!</h3>
    <div class="token-display" id="tokenDisplay">टोकन #--</div>
    
    <div class="queue-info" id="queueInfo">
      कतार प्रणाली: आपके आगे <b id="pendingCount">0</b> प्रिंट लंबित हैं।
    </div>
    
    <div class="countdown-timer" id="countdownTimer">
      अनुमानित समय: <span id="timeRemaining">--</span> सेकंड
    </div>

    <p style="font-size: 0.8rem; color: #666; margin-top: 10px;" id="q-subtext">
      कृपया प्रिंटर के पास रहें। प्रिंट होते ही कलेक्ट कर लें।
    </p>
  </div>

  <!-- Footer Links: Contact Details, Refund, Terms -->
  <div class="footer-links">
    <a href="javascript:void(0)" onclick="openModal('contactModal')" id="lnk-contact">संपर्क (Contact)</a> | 
    <a href="javascript:void(0)" onclick="openModal('refundModal')" id="lnk-refund">रिफंड नीति (Refund)</a> | 
    <a href="javascript:void(0)" onclick="openModal('termsModal')" id="lnk-terms">नियम व शर्तें (Terms)</a>
  </div>
</div>

<!-- ================== MODAL POPUPS ================== -->

<!-- 1. Contact Us Popup: Yahan apna number, address aur email badal sakte hain -->
<div id="contactModal" class="modal">
  <div class="modal-content">
    <h4 style="margin-top:0;">संपर्क सूत्र (Contact Us)</h4>
    <p>
      <!-- YAHAN APNA MOBILE NUMBER AUR EMAIL EDIT KAREIN -->
      <b>हेल्पलाइन नंबर:</b> +91 9876543210<br>
      <b>ईमेल आईडी:</b> support@autoprintkiosk.in<br>
      <b>कियोस्क पता:</b> कलेक्ट्रेट परिसर, उमरिया, मध्य प्रदेश
    </p>
    <button class="modal-close" onclick="closeModal('contactModal')">बंद करें</button>
  </div>
</div>

<!-- 2. Refund Policy Popup -->
<div id="refundModal" class="modal">
  <div class="modal-content">
    <h4 style="margin-top:0;">रिफंड नीति (Refund Policy)</h4>
    <p>
      1. यदि प्रिंट सफलतापूर्वक निकल जाता है, तो कोई रिफंड नहीं दिया जाएगा।<br>
      2. पेपर जाम होने, स्याही/पेज समाप्त होने या तकनीकी खराबी के कारण प्रिंट न निकलने पर आपके द्वारा दर्ज यूपीआई (UPI) पर <b>5 मिनट के भीतर ऑटो-रिफंड</b> कर दिया जाएगा।
    </p>
    <button class="modal-close" onclick="closeModal('refundModal')">बंद करें</button>
  </div>
</div>

<!-- 3. Terms & Privacy Policy Popup -->
<div id="termsModal" class="modal">
  <div class="modal-content">
    <h4 style="margin-top:0;">नियम व शर्तें (Terms & Conditions)</h4>
    <p>
      1. गोपनीयता सुरक्षा: प्रिंटिंग पूर्ण होने के <b>5 मिनट के भीतर आपकी फ़ाइल सर्वर से हमेशा के लिए डिलीट (Auto-Delete)</b> कर दी जाएगी।<br>
      2. किसी भी प्रकार की आपत्तिजनक या गैर-कानूनी सामग्री को प्रिंट करना सख्त वर्जित है।
    </p>
    <button class="modal-close" onclick="closeModal('termsModal')">बंद करें</button>
  </div>
</div>

<script>
  // Global variables
  let currentLanguage = 'hi';
  let detectedPages = 0;
  let totalCalculatedAmount = 0;
  let selectedFileObject = null;

  // Bilingual UI dictionary
  const i18n = {
    hi: {
      title: "उमरिया कलेक्ट्रेट ऑटो-प्रिंटिंग",
      fileLabel: "फ़ाइल चुनें जिसे प्रिंट करना चाहते हैं (PDF/Image):",
      colorLabel: "प्रिंट का प्रकार (Print Type):",
      sideLabel: "प्रिंटिंग साइड (Sides):",
      payBtnText: "UPI / कार्ड से भुगतान करें",
      payPrefix: "कुल शुल्क: ₹",
      pagePrefix: "कुल पृष्ठ: ",
      warning: "⚠️ <b>महत्वपूर्ण निर्देश:</b> आपकी फ़ाइल में 5 से अधिक पृष्ठ हैं। प्रिंटर में पेपर फंसने से बचाने के लिए जैसे ही 5 पेज बाहर निकलें, उन्हें ट्रे से हटा लें और शेष पेज निकलने का इंतज़ार करें।",
      successTitle: "भुगतान सफल रहा!",
      tokenPrefix: "टोकन #",
      queuePrefix: "कतार प्रणाली: आपके आगे ",
      queueSuffix: " प्रिंट लंबित हैं।",
      estTime: "अनुमानित समय: ",
      seconds: " सेकंड",
      printComplete: "प्रिंटिंग पूर्ण हुई! धन्यवाद।",
      contact: "संपर्क (Contact)",
      refund: "रिफंड नीति (Refund)",
      terms: "नियम व शर्तें (Terms)"
    },
    en: {
      title: "Umaria Collectorate Auto-Printing",
      fileLabel: "Select file you want to print (PDF/Image):",
      colorLabel: "Print Type:",
      sideLabel: "Printing Sides:",
      payBtnText: "Pay with UPI / Card",
      payPrefix: "Total Amount: ₹",
      pagePrefix: "Total Pages: ",
      warning: "⚠️ <b>Important Note:</b> Your file has more than 5 pages. To prevent paper jamming, remove pages from the tray once 5 pages are printed and wait for the rest.",
      successTitle: "Payment Successful!",
      tokenPrefix: "Token #",
      queuePrefix: "Queue System: There are ",
      queueSuffix: " prints pending ahead of you.",
      estTime: "Estimated Time: ",
      seconds: " seconds",
      printComplete: "Printing Completed! Thank you.",
      contact: "Contact Us",
      refund: "Refund Policy",
      terms: "Terms & Conditions"
    }
  };

  // Language change function
  function changeLanguage(lang) {
    currentLanguage = lang;
    document.querySelectorAll('.lang-btn').forEach(b => b.classList.remove('active'));
    event.target.classList.add('active');

    const text = i18n[lang];
    document.getElementById('ui-title').innerText = text.title;
    document.getElementById('lbl-file').innerText = text.fileLabel;
    document.getElementById('lbl-color').innerText = text.colorLabel;
    document.getElementById('lbl-side').innerText = text.sideLabel;
    document.getElementById('jamWarning').innerHTML = text.warning;
    document.getElementById('lnk-contact').innerText = text.contact;
    document.getElementById('lnk-refund').innerText = text.refund;
    document.getElementById('lnk-terms').innerText = text.terms;
    recalculatePrice();
  }

  // Automatic PDF page reader using PDF.js
  async function handleFileSelect(event) {
    const file = event.target.files[0];
    if (!file) return;

    selectedFileObject = file;

    // Security: File size check (Max 25MB allowed)
    if (file.size > 25 * 1024 * 1024) {
      alert(currentLanguage === 'hi' ? "फ़ाइल का साइज़ 25MB से कम होना चाहिए।" : "File size must be under 25MB.");
      event.target.value = "";
      return;
    }

    if (file.type === "application/pdf") {
      const fileReader = new FileReader();
      fileReader.onload = async function() {
        try {
          const typedArray = new Uint8Array(this.result);
          pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';
          const pdf = await pdfjsLib.getDocument(typedArray).promise;
          detectedPages = pdf.numPages;
          evaluatePageRules();
        } catch (error) {
          alert(currentLanguage === 'hi' ? "PDF पढ़ने में त्रुटि। कृपया सामान्य PDF फ़ाइल चुनें।" : "Corrupt PDF file. Please select a valid document.");
        }
      };
      fileReader.readAsArrayBuffer(file);
    } else if (file.type.startsWith("image/")) {
      // Image is counted as 1 page
      detectedPages = 1;
      evaluatePageRules();
    }
  }

  // Evaluate rules like 5-page warning & pricing
  function evaluatePageRules() {
    // 5 Page jam warning condition
    const warningElement = document.getElementById('jamWarning');
    if (detectedPages > 5) {
      warningElement.style.display = 'block';
    } else {
      warningElement.style.display = 'none';
    }

    recalculatePrice();
  }

  // Rate calculator based on requirements
  function recalculatePrice() {
    if (detectedPages === 0) return;

    const isColor = document.getElementById('colorOption').value === 'color';
    const isDuplex = document.getElementById('sideOption').value === 'duplex';

    // Pricing Matrix:
    // B&W: Single = ₹2.00, Duplex = ₹4.00
    // Color: Single = ₹5.00, Duplex = ₹10.00
    let ratePerPage = 0;
    if (!isColor) {
      ratePerPage = isDuplex ? 4.00 : 2.00;
    } else {
      ratePerPage = isDuplex ? 10.00 : 5.00;
    }

    totalCalculatedAmount = detectedPages * ratePerPage;

    const text = i18n[currentLanguage];
    document.getElementById('pageCountDisplay').innerText = `${text.pagePrefix}${detectedPages}`;
    document.getElementById('priceDisplay').innerText = `${text.payPrefix}${totalCalculatedAmount.toFixed(2)}`;

    // Enable payment button
    const payBtn = document.getElementById('payBtn');
    payBtn.disabled = false;
    payBtn.innerText = `${text.payBtnText} (₹${totalCalculatedAmount.toFixed(2)})`;
  }

  // Razorpay Gateway Trigger
  function initiateRazorpayPayment() {
    if (!selectedFileObject || totalCalculatedAmount <= 0) return;

    /*
      =======================================================
      RAZORPAY INTEGRATION SPOT:
      Neeche 'key' me apni Razorpay Key ID paste karein.
      Test Mode me: 'rzp_test_XXXXXXXXXXXXXX'
      Live Mode me: 'rzp_live_XXXXXXXXXXXXXX'
      =======================================================
    */
    const razorpayOptions = {
      "key": "rzp_test_YOUR_ACTUAL_KEY_HERE", // <-- YAHAN APNI KEY PASTE KAREIN
      "amount": totalCalculatedAmount * 100, // Amount in Paise (e.g. ₹4.00 = 400 paise)
      "currency": "INR",
      "name": "Umaria Collectorate Kiosk",
      "description": `Print Charge (${detectedPages} Pages)`,
      "handler": function (response) {
        // Payment successful callback
        const paymentId = response.razorpay_payment_id;
        uploadFileAndTriggerQueue(paymentId);
      },
      "prefill": {
        "contact": "",
        "email": ""
      },
      "theme": {
        "color": "#0d47a1"
      }
    };

    const rzpInstance = new Razorpay(razorpayOptions);
    rzpInstance.open();
  }

  // Upload to Pi Server & Show Live Queue Countdown
  function uploadFileAndTriggerQueue(paymentId) {
    document.getElementById('upload-screen').style.display = 'none';
    document.getElementById('statusPanel').style.display = 'block';

    const token = Math.floor(Math.random() * 80) + 10;
    const text = i18n[currentLanguage];

    document.getElementById('tokenDisplay').innerText = `${text.tokenPrefix}${token}`;

    // Pi Controller queue reading simulation
    let pendingPrints = 2; // Real-world: Fetched from Pi backend
    let secondsRemaining = pendingPrints * 15 + (detectedPages * 3); // Dynamic queue time calculation

    function updateQueueUI() {
      document.getElementById('queueInfo').innerHTML = 
        `${text.queuePrefix}<b>${pendingPrints}</b>${text.queueSuffix}`;
      document.getElementById('timeRemaining').innerText = secondsRemaining;
    }
    updateQueueUI();

    // 1-Second Tick Countdown Interval
    const timerInterval = setInterval(() => {
      secondsRemaining--;
      if (secondsRemaining <= 10 && pendingPrints > 0) {
        pendingPrints = 0;
      }
      updateQueueUI();

      if (secondsRemaining <= 0) {
        clearInterval(timerInterval);
        document.getElementById('countdownTimer').innerHTML = 
          `<b style="color: #28a745;">✅ ${text.printComplete}</b>`;
      }
    }, 1000);

    /*
      Raspberry Pi API ko file bhejna (Backend sync):
      const formData = new FormData();
      formData.append("file", selectedFileObject);
      formData.append("payment_id", paymentId);
      formData.append("pages", detectedPages);
      fetch("http://YOUR_PI_IP_OR_DOMAIN:5000/api/print-job", { method: "POST", body: formData });
    */
  }

  // Modal handler functions
  function openModal(id) { document.getElementById(id).style.display = 'flex'; }
  function closeModal(id) { document.getElementById(id).style.display = 'none'; }
</script>

</body>
</html>
