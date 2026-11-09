function sendInvoiceToWhatsApp() {
    // 1. تحديد بيانات العميل والفاتورة الأساسية
    const invoiceNumber = "1024";
    const customerName = "عميل نقدي";
    const date = new Date().toLocaleDateString('ar-EG');
    const phoneNumber = "9677XXXXXXXX"; // اكتب هنا رقم الواتساب المستلم (مسبوقاً بمفتاح الدوله بدون أصفار أو +)

    // 2. تجميع المنتجات من الفاتورة وتسطيرها
    // يمكنك تعديل هذه البيانات لتأتي ديناميكياً من سلة التسوق لديك
    const items = [
        { name: "منتج رقم 1", qty: 2, price: 50, total: 100 },
        { name: "منتج رقم 2", qty: 1, price: 150, total: 150 }
    ];

    let itemsText = "";
    items.forEach(item => {
        // تنسيق السطر ليظهر بشكل مسطر ومنظم في الواتساب
        itemsText += `${item.name.padEnd(15)} |  ${item.qty}  | ${item.price} ر.ي  | ${item.total} ر.ي\n`;
    });

    const subTotal = 250;
    const tax = 12.5;
    const grandTotal = 262.5;

    // 3. بناء نص الرسالة المنسق والمسطر للواتساب باستخدام الرموز
    const message = 
`*🧾 فاتورة مبيعات - نظام الأمير*
---------------------------------------
*رقم الفاتورة:* #${invoiceNumber}
*التاريخ:* ${date}
*العميل:* ${customerName}
---------------------------------------
*البيان*          | *الكمية* | *السعر*   | *الإجمالي*
---------------------------------------
${itemsText}---------------------------------------
*📊 الملخص الرياضي:*
▪️ *الإجمالي الفرعي:* ${subTotal} ر.ي
▪️ *الضريبة (5%):* ${tax} ر.ي
---------------------------------------
*💰 الصافي الإجمالي: ${grandTotal} ر.ي*
---------------------------------------
_شكراً لتسوقكم من الأمير 🙏_`;

    // 4. تشفير النص وتحويله إلى رابط الواتساب المباشر
    const encodedMessage = encodeURIComponent(message);
    const whatsappURL = `https://whatsapp.com{phoneNumber}&text=${encodedMessage}`;

    // 5. فتح الرابط في نافذة جديدة لإرسال الفاتورة فوراً
    window.open(whatsappURL, '_blank');
}<button onclick="sendInvoiceToWhatsApp()" style="background-color: #25D366; color: white; padding: 10px 20px; border: none; border-radius: 5px; cursor: pointer; font-size: 16px;">
    📱 إرسال الفاتورة عبر الواتساب
</button>


