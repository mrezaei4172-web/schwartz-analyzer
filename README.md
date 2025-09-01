[ارزش های فردی شوارتز.html](https://github.com/user-attachments/files/22079067/default.html)
<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>تحلیل ارزش‌های شوارتز</title>
  <style>
    body {
      font-family: Tahoma, Arial, sans-serif;
      max-width: 800px;
      margin: 40px auto;
      padding: 20px;
      background-color: #f7f9fc;
      color: #333;
      line-height: 2;
    }
    h1 {
      text-align: center;
      color: #2c3e50;
    }
    .form-group {
      margin: 15px 0;
    }
    label {
      display: block;
      margin-bottom: 8px;
      font-weight: bold;
      color: #2c3e50;
    }
    input {
      width: 70px;
      padding: 8px;
      border: 1px solid #ccc;
      border-radius: 4px;
      font-size: 16px;
    }
    button {
      display: block;
      margin: 30px auto;
      padding: 12px 30px;
      font-size: 18px;
      background-color: #3498db;
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
    }
    button:hover {
      background-color: #2980b9;
    }
    #result {
      margin-top: 30px;
      padding: 20px;
      background: white;
      border: 1px solid #ddd;
      border-radius: 8px;
      white-space: pre-wrap;
      font-size: 17px;
      line-height: 2;
    }
  </style>
</head>
<body>
  <h1>تحلیل ارزش‌های شوارتز</h1>
  <p>لطفاً نمرات خود را از 1 تا 100 وارد کنید:</p>

  <form id="schwartzForm">
    <div class="form-group">
      <label>🌍 جهان‌گرایی: <input type="number" name="universalism" min="1" max="100" required /></label>
    </div>
    <div class="form-group">
      <label>🤝 خیرخواهی: <input type="number" name="benevolence" min="1" max="100" required /></label>
    </div>
    <div class="form-group">
      <label>🛡️ امنیت: <input type="number" name="security" min="1" max="100" required /></label>
    </div>
    <div class="form-group">
      <label>📜 سنت: <input type="number" name="tradition" min="1" max="100" required /></label>
    </div>
    <div class="form-group">
      <label>👥 هماهنگی: <input type="number" name="conformity" min="1" max="100" required /></label>
    </div>
    <div class="form-group">
      <label>🏆 موفقیت: <input type="number" name="achievement" min="1" max="100" required /></label>
    </div>
    <div class="form-group">
      <label>⚡ قدرت: <input type="number" name="power" min="1" max="100" required /></label>
    </div>
    <div class="form-group">
      <label>🔥 انگیزش: <input type="number" name="stimulation" min="1" max="100" required /></label>
    </div>
    <div class="form-group">
      <label>🎉 لذت‌جویی: <input type="number" name="hedonism" min="1" max="100" required /></label>
    </div>
    <div class="form-group">
      <label>🧭 خوداتکایی: <input type="number" name="self_direction" min="1" max="100" required /></label>
    </div>

    <button type="submit">تحلیل کن</button>
  </form>

  <div id="result"></div>

  <script>
    // دیتابیس بلوک‌های سه‌سطحی
    const blocks = {
      universalism: {
        strong: { summary: "دنیا رو جای بهتری کنی، به عدالت و صلح فکر کنی", emoji: "🌍" },
        moderate: { summary: "به مسائل جهانی و عدالت اهمیت می‌دی، اما نه خیلی پیوسته", emoji: "🌐" },
        low: { summary: "شاید موضوعات جهانی زیاد برات اولویت نباشن و بیشتر به محیط نزدیک‌ات فکر کنی", emoji: "🌆" }
      },
      benevolence: {
        strong: { summary: "به دیگران کمک کنی و مراقب باشی", emoji: "❤️" },
        moderate: { summary: "دوست داری مهربان باشی، اما نه خیلی فعال یا پیوسته", emoji: "🤝" },
        low: { summary: "شاید کمتر به دیگران فکر کنی و بیشتر به نیازهای خودت توجه کنی", emoji: "🧍‍♂️" }
      },
      security: {
        strong: { summary: "در محیطی امن و پایدار زندگی کنی", emoji: "🛡️" },
        moderate: { summary: "به ثبات و نظم اهمیت می‌دی، اما نه خیلی سفت و سخت", emoji: "🏠" },
        low: { summary: "شاید نظم و امنیت برات اولویت نباشه و بیشتر دوست داشته باشی ریسک کنی", emoji: "🌪️" }
      },
      tradition: {
        strong: { summary: "با احترام به سنت، خانواده و ارزش‌ها پیش ببری", emoji: "🏡" },
        moderate: { summary: "به سنت و خانواده اهمیت می‌دی، اما نه خیلی کورکورانه", emoji: "🕯️" },
        low: { summary: "شاید سنت‌ها برات اولویت نباشن و بیشتر به آینده فکر کنی", emoji: "🚀" }
      },
      conformity: {
        strong: { summary: "به قوانین و نظم احترام بذاری", emoji: "⚖️" },
        moderate: { summary: "گاهی قوانین رو رعایت می‌کنی، اما گاهی هم ازشون عبور می‌کنی", emoji: "📌" },
        low: { summary: "شاید قوانین برات محدودیت‌زا باشن و ترجیح بدهی آزاد باشی", emoji: "🚫" }
      },
      achievement: {
        strong: { summary: "اهداف بزرگی داشته باشی و بهشون برسی", emoji: "🎯" },
        moderate: { summary: "دوست داری پیشرفت کنی، اما نه تحت فشار زیاد", emoji: "📈" },
        low: { summary: "شاید موفقیت به خودی خود برات اولویت نباشه و بیشتر به تعادل فکر کنی", emoji: "⚖️" }
      },
      power: {
        strong: { summary: "تأثیر بگذاری و کنترل داشته باشی", emoji: "👑" },
        moderate: { summary: "گاهی دوست داری تأثیر بذاری، اما نه خیلی فعال", emoji: "🤝" },
        low: { summary: "شاید کنترل یا رهبری برات اولویت نباشه و ترجیح بدهی از پس‌پرده باشی", emoji: "🌿" }
      },
      stimulation: {
        strong: { summary: "هیجان و تغییر رو دنبال کنی", emoji: "🌀" },
        moderate: { summary: "دوست داری چیزهای جدید امتحان کنی، اما نه خیلی پیوسته", emoji: "🔍" },
        low: { summary: "شاید هیجان و ریسک زیاد برات جذاب نباشه و ترجیح بدهی با آرامش پیش ببری", emoji: "🧘‍♂️" }
      },
      hedonism: {
        strong: { summary: "از لحظه لذت ببری و شادی رو بخوای", emoji: "🎉" },
        moderate: { summary: "گاهی از لحظه لذت می‌بری، اما نه به عنوان اولویت", emoji: "😊" },
        low: { summary: "شاید لذت‌های لحظه‌ای برات معنا نداشته باشن و بیشتر به دنبال معنای عمیق باشی", emoji: "🕯️" }
      },
      self_direction: {
        strong: { summary: "مستقل فکر کنی و ایده‌هات رو بسازی", emoji: "💡" },
        moderate: { summary: "دوست داری خلاق باشی، اما نه خیلی پیوسته", emoji: "✨" },
        low: { summary: "شاید ترجیح بدهی از راه‌های آشنا پیش ببری و کمتر به دنبال ایده‌های جدید باشی", emoji: "🛑" }
      }
    };

    // تابع تشخیص سطح
    function getLevel(score) {
      if (score >= 80) return "strong";
      if (score >= 60) return "moderate";
      return "low";
    }

    // تابع ترکیب فارسی
    function joinPersian(list) {
      if (list.length === 0) return "";
      if (list.length === 1) return list[0];
      return list.slice(0, -1).join("، ") + " و " + list[list.length - 1];
    }

    // رویداد فرم
    document.getElementById("schwartzForm").addEventListener("submit", function(e) {
      e.preventDefault();
      const form = e.target;
      const data = new FormData(form);

      // جمع‌آوری نمرات
      const scores = {};
      for (let [key, value] of data) {
        scores[key] = parseInt(value);
      }

      // دسته‌بندی ارزش‌ها
      const strong = [], moderate = [], low = [];
      const strongSummaries = [], moderateSummaries = [];
      let strongEmojis = "", moderateEmojis = "", lowEmojis = "";

      for (let key in scores) {
        const score = scores[key];
        const level = getLevel(score);
        const block = blocks[key];
        const persianName = {
          universalism: "جهان‌گرایی",
          benevolence: "خیرخواهی",
          security: "امنیت",
          tradition: "سنت",
          conformity: "هماهنگی",
          achievement: "موفقیت",
          power: "قدرت",
          stimulation: "انگیزش",
          hedonism: "لذت‌جویی",
          self_direction: "خوداتکایی"
        }[key];

        if (level === "strong") {
          strong.push(persianName);
          strongSummaries.push(block.strong.summary);
          strongEmojis += block.strong.emoji;
        } else if (level === "moderate") {
          moderate.push(persianName);
          moderateSummaries.push(block.moderate.summary);
          moderateEmojis += block.moderate.emoji;
        } else {
          low.push(persianName);
          lowEmojis += block.low.emoji;
        }
      }

      // تولید خروجی
      let result = "";

      if (strong.length > 0) {
        result += `تو فردی هستی که ارزش‌های ${joinPersian(strong)}‌ات خیلی قویه و نشون می‌ده دوست داری ${joinPersian(strongSummaries)}. ${strongEmojis}
این ویژگی‌ها بهت کمک می‌کنن که در تصمیم‌گیری‌هات هم به خودت فکر کنی، هم به جامعه و آینده. شاید دوست داری به سوالای بزرگ زندگی مثل "چطور می‌تونم تأثیر مثبت بذارم؟" یا "چطور می‌تونیم با هم زندگی کنیم؟" جواب پیدا کنی.

`;
      }

      if (moderate.length > 0) {
        result += `علاوه بر این، ارزش‌های ${joinPersian(moderate)}‌ات نشون می‌ده که تو دوست داری ${joinPersian(moderateSummaries)}. ${moderateEmojis}
اما شاید این حوزه‌ها اون‌قدرها هم که فکر می‌کنی فعال نیستن و گاهی بین تمایل به نوآوری و رعایت سنت‌ها درگیر یه کش‌و‌خم درونی باشی.

`;
      }

      if (low.length > 0) {
        result += `اما شاید ارزش‌های ${joinPersian(low)}‌ات نسبت به بقیه ارزش‌هایت کمتر برجسته باشن. شاید کنترل، رهبری یا تأثیرگذاری مستقیم برات اولویت نباشه و بیشتر دوست داشته باشی از پس‌پرده و با آرامش تغییر ایجاد کنی. همچنین، هیجان، ریسک یا تغییرِ سریع زیاد برات جذاب نباشه و ترجیح بدهی با برنامه و ثبات پیش ببری. همین‌طور، لذت‌های لحظه‌ای یا شادی‌های بی‌دلیل ممکنه زیاد برات معنا نداشته باشن و بیشتر به دنبال معنای عمیق و پایدار در زندگی باشی. ${lowEmojis}`;
      }

      document.getElementById("result").textContent = result;
    });
  </script>
</body>
</html>
