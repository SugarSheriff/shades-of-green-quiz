# Shades of Green Quiz 🌱♻️

A beautiful, interactive quiz about waste sorting and recycling. Test your knowledge about proper waste disposal and learn to make a positive environmental impact!

![Quiz Preview](preview.png)

## Features

- **21 Questions** covering composting, recycling, and landfill sorting
- **Image-based questions** for visual learning
- **Instant feedback** with explanations for each answer
- **Progress tracking** with localStorage (resume incomplete quizzes)
- **Score review** to learn from mistakes
- **Mobile responsive** design
- **No backend required** - runs entirely in the browser

## Quick Deploy

### Option 1: GitHub Pages (Free)

1. **Fork or clone this repository**
   ```bash
   git clone https://github.com/YOUR_USERNAME/shades-of-green-quiz.git
   cd shades-of-green-quiz
   ```

2. **Push to GitHub**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/shades-of-green-quiz.git
   git push -u origin main
   ```

3. **Enable GitHub Pages**
   - Go to your repo Settings → Pages
   - Under "Source", select `main` branch
   - Click Save
   - Your site will be live at: `https://YOUR_USERNAME.github.io/shades-of-green-quiz/`

### Option 2: Netlify (Free)

**Drag & Drop Deploy:**
1. Go to [netlify.com/drop](https://app.netlify.com/drop)
2. Drag the project folder onto the page
3. Done! Get your unique URL instantly

**Git-based Deploy:**
1. Push your code to GitHub
2. Log into [Netlify](https://netlify.com)
3. Click "New site from Git"
4. Select your repository
5. Deploy settings are auto-detected
6. Click "Deploy site"

### Option 3: Vercel (Free)

1. Install Vercel CLI: `npm i -g vercel`
2. Run `vercel` in the project directory
3. Follow the prompts

## Customization

### Changing Questions

Edit the `QUESTIONS` array in `index.html`:

```javascript
const QUESTIONS = [
  {
    q: "Your question text here",
    answers: ["Option A", "Option B", "Option C"],
    correct: 0, // Index of correct answer (0-based)
    explanations: [
      "Explanation for Option A",
      "Explanation for Option B",
      "Explanation for Option C"
    ],
    img: "GOOGLE_DRIVE_FILE_ID" // From drive.google.com/file/d/THIS_PART/view
  },
  // ... more questions
];
```

### Changing Images

Images are loaded from Google Drive. To use your own:

1. Upload image to Google Drive
2. Right-click → Share → "Anyone with the link"
3. Copy the file ID from the URL: `drive.google.com/file/d/FILE_ID_HERE/view`
4. Use that ID in the `img` field

Alternatively, host images locally by placing them in an `images/` folder and updating the `img.src` line in the `loadQuestion()` function.

### Branding & Colors

CSS variables are at the top of `<style>`:

```css
:root {
  --color-forest: #1a4d2e;     /* Primary dark green */
  --color-moss: #2d5a3d;       /* Secondary green */
  --color-sage: #4a7c59;       /* Accent green */
  --color-mint: #8fbc8f;       /* Light green */
  --color-cream: #f5f7f2;      /* Background */
  --color-gold: #c9a227;       /* Highlight */
  --color-success: #3d8b40;    /* Correct answer */
  --color-error: #c44536;      /* Wrong answer */
  
  --font-display: 'Fraunces', Georgia, serif;  /* Headings */
  --font-body: 'DM Sans', sans-serif;          /* Body text */
}
```

## Adding Backend Scoring (Optional)

If you want to collect scores, you can add a simple backend:

### Using Google Sheets + Apps Script

1. Create a new Google Sheet
2. Go to Extensions → Apps Script
3. Add this code:

```javascript
function doPost(e) {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  const data = JSON.parse(e.postData.contents);
  
  sheet.appendRow([
    new Date(),
    data.name,
    data.score,
    data.total,
    data.percent + '%',
    data.timeMinutes
  ]);
  
  return ContentService.createTextOutput(JSON.stringify({success: true}));
}
```

4. Deploy as web app (Anyone can access)
5. Add fetch call in the quiz's `saveCompletion()` function

### Using Netlify Functions

Create `netlify/functions/submit-score.js`:

```javascript
exports.handler = async (event) => {
  const data = JSON.parse(event.body);
  // Save to your database of choice
  return { statusCode: 200, body: JSON.stringify({ success: true }) };
};
```

## Browser Support

- Chrome 80+
- Firefox 75+
- Safari 13+
- Edge 80+

## License

MIT License - feel free to use and modify for your organization!

---

Made with 💚 for environmental awareness
