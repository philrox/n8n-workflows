# ⚡ Quick Start Guide - SEO Intelligence Autopilot

Get your first SEO analysis running in **under 10 minutes**!

---

## 🎯 Pre-requisites Checklist

Before you start, make sure you have:

- [ ] n8n instance running (cloud or self-hosted)
- [ ] DataForSEO account with credits ([Sign up here](https://dataforseo.com/))
- [ ] Anthropic Claude API key ([Get it here](https://console.anthropic.com/))
- [ ] Google account for Docs/Sheets access

---

## 🚀 5-Step Setup

### Step 1: Import Workflow (2 minutes)

1. Download `SEO_Intelligence_Autopilot.json`
2. In n8n, click **Workflows** → **Import from File**
3. Select the JSON file
4. Click **Import**

✅ You should see the workflow with ~20 nodes

---

### Step 2: Configure DataForSEO (2 minutes)

1. **Get your credentials:**
   - Login to [DataForSEO](https://my.dataforseo.com/)
   - Copy your **Login** (email)
   - Copy your **Password** (not account password, API password!)

2. **Add to n8n:**
   - Click on node: "DataForSEO: Keywords For Site"
   - Click **Create New Credential**
   - Select: **Basic Auth**
   - **Username:** Your DataForSEO login
   - **Password:** Your DataForSEO API password
   - Click **Save**

3. **Apply to all DataForSEO nodes:**
   - Click on each HTTP Request node with "DataForSEO" in the name
   - Select the credential you just created
   - Nodes to update:
     - ✅ DataForSEO: Keywords For Site
     - ✅ DataForSEO: SERP Analysis
     - ✅ DataForSEO: Competitor Keywords

---

### Step 3: Configure Claude API (1 minute)

1. **Get your API key:**
   - Go to [Anthropic Console](https://console.anthropic.com/)
   - Navigate to **API Keys**
   - Click **Create Key**
   - Copy the key (it won't be shown again!)

2. **Add to n8n:**
   - Click on node: "Claude: Strategic Analysis"
   - In the **Model** section, you'll see it's set to use Chat Anthropic
   - Click **Credential to connect with**
   - Click **Create New Credential**
   - Paste your API key
   - Click **Save**

**Note:** Make sure the model is set to `claude-sonnet-4-20250514` or latest Sonnet version.

---

### Step 4: Configure Google Drive (3 minutes)

#### Google Docs Setup:

1. **Enable Google Docs API:**
   - Go to [Google Cloud Console](https://console.cloud.google.com/)
   - Create new project or select existing
   - Enable **Google Docs API**
   - Create **OAuth 2.0 Client ID** (Application type: Web application)
   - Add authorized redirect URI: `https://your-n8n-instance.com/rest/oauth2-credential/callback`

2. **Add to n8n:**
   - Click on node: "Google Docs: Create Report"
   - Click **Create New Credential**
   - Select: **Google Docs OAuth2 API**
   - Enter **Client ID** and **Client Secret** from Google Cloud
   - Click **Connect my account**
   - Follow OAuth flow
   - Click **Save**

#### Google Sheets Setup:

1. **Enable Google Sheets API:**
   - In same Google Cloud project
   - Enable **Google Sheets API**

2. **Add to n8n:**
   - Click on node: "Google Sheets: Update Tracker"
   - Click **Create New Credential**
   - Select: **Google Sheets OAuth2 API**
   - Use same Client ID/Secret OR create new one
   - Click **Connect my account**
   - Follow OAuth flow
   - Click **Save**

3. **Create Tracker Spreadsheet:**
   - Go to [Google Sheets](https://sheets.google.com/)
   - Create new spreadsheet: "SEO Intelligence Tracker"
   - Copy the Spreadsheet ID from URL:
     ```
     https://docs.google.com/spreadsheets/d/SPREADSHEET_ID_HERE/edit
     ```
   - In n8n, paste this ID in the "Google Sheets: Update Tracker" node
   - Set **Sheet Name** to "Sheet1" (or create custom tabs)

---

### Step 5: Activate & Test (2 minutes)

1. **Activate Workflow:**
   - Click the **Active** toggle at top-right
   - Should turn green ✅

2. **Get Webhook URL:**
   - Click on "Webhook: URL Input" node
   - Copy the **Production Webhook URL**
   - Should look like: `https://your-n8n.com/webhook/seo-autopilot`

3. **Test with curl:**
   ```bash
   curl -X POST https://your-n8n.com/webhook/seo-autopilot \
     -H "Content-Type: application/json" \
     -d '{"url": "https://hyroxtrainingplans.com"}'
   ```

4. **Expected Response:**
   ```
   🚀 SEO Analysis started for https://hyroxtrainingplans.com

   You'll receive a notification when the analysis is complete!
   ```

5. **Monitor Execution:**
   - Go to **Executions** in n8n
   - You should see a running execution
   - Watch it progress through each node
   - Estimated time: **2-4 minutes**

6. **Check Results:**
   - After completion, check your Google Drive
   - New document: "SEO Strategy Report - hyroxtrainingplans.com - [date]"
   - Open and review!

---

## 🎉 Success! You're Ready!

### What happens now?

Every time you POST to the webhook with a URL, the workflow will:

1. ✅ Find all keywords the site ranks for
2. ✅ Identify top competitors automatically
3. ✅ Analyze SERP features and opportunities
4. ✅ Generate AI-powered strategy with Claude
5. ✅ Create formatted Google Doc report
6. ✅ Update Google Sheets tracker
7. ✅ Send notification (if Slack configured)

---

## 🔧 Optional Enhancements

### Add Slack Notifications (Optional)

1. Create Slack App at [api.slack.com/apps](https://api.slack.com/apps)
2. Add **Bot Token** to n8n "Slack: Completion Notification" node
3. Select channel for notifications
4. Receive alerts when analysis completes!

### Create Simple Web Form

Create `index.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>SEO Autopilot</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 600px;
            margin: 50px auto;
            padding: 20px;
        }
        input {
            width: 100%;
            padding: 12px;
            font-size: 16px;
            border: 2px solid #ddd;
            border-radius: 4px;
            margin: 10px 0;
        }
        button {
            width: 100%;
            padding: 12px;
            font-size: 18px;
            background: #4CAF50;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        button:hover {
            background: #45a049;
        }
        .result {
            margin-top: 20px;
            padding: 15px;
            background: #e8f5e9;
            border-radius: 4px;
            display: none;
        }
    </style>
</head>
<body>
    <h1>🚀 SEO Intelligence Autopilot</h1>
    <p>Enter any website URL for instant SEO analysis</p>

    <form id="seoForm">
        <input
            type="url"
            id="urlInput"
            placeholder="https://example.com"
            required
        >
        <button type="submit">Analyze My Site 🔍</button>
    </form>

    <div id="result" class="result"></div>

    <script>
        document.getElementById('seoForm').addEventListener('submit', async (e) => {
            e.preventDefault();
            const url = document.getElementById('urlInput').value;
            const resultDiv = document.getElementById('result');

            resultDiv.style.display = 'block';
            resultDiv.innerHTML = '⏳ Analyzing... Please wait 2-3 minutes...';

            try {
                const response = await fetch('https://your-n8n.com/webhook/seo-autopilot', {
                    method: 'POST',
                    headers: {'Content-Type': 'application/json'},
                    body: JSON.stringify({url: url})
                });

                const text = await response.text();
                resultDiv.innerHTML = `✅ ${text}<br><br>Check your Google Drive for the report!`;
            } catch (error) {
                resultDiv.innerHTML = `❌ Error: ${error.message}`;
            }
        });
    </script>
</body>
</html>
```

Host this on:
- GitHub Pages (free)
- Netlify (free)
- Vercel (free)
- Or your own server

---

## 🐛 Common Issues

### Issue: "Authentication failed" for DataForSEO
**Solution:** Make sure you're using the **API password** from DataForSEO dashboard, not your account login password.

### Issue: Claude returns error
**Solution:** Check API key is valid and has credits. Verify model name is correct.

### Issue: No Google Doc created
**Solution:**
- Re-authenticate OAuth
- Check Docs API is enabled
- Verify permissions granted

### Issue: Execution fails at SERP Analysis
**Solution:**
- Check DataForSEO credits
- Verify keywords exist (try different test domain)
- Check location_code is valid

---

## 📊 Understanding the Output

### Google Doc Report Structure:

1. **Executive Summary**
   - Quick overview of findings
   - Main opportunity identified

2. **Current Performance**
   - Keywords you rank for
   - Average position
   - Traffic estimates

3. **Competitor Analysis**
   - Who your competitors are
   - What they rank for
   - How to compete

4. **Opportunity Keywords**
   - Keywords with high potential
   - Why they matter
   - How to target them

5. **Content Recommendations**
   - Specific article ideas
   - Complete outlines
   - Target keywords

6. **Action Checklist**
   - Step-by-step tasks
   - Prioritized list
   - Clear instructions

### Google Sheets Tracker:

Will be populated with:
- All keywords with metrics
- Opportunity scores
- Competitor comparisons
- Historical tracking (if run monthly)

---

## 📈 Next Steps

### Run Your First Real Analysis:

1. **Choose a website** (yours or client's)
2. **Submit via webhook** or web form
3. **Wait 2-4 minutes** for completion
4. **Open Google Doc** report
5. **Review recommendations**
6. **Start with High Priority items**

### Optimize Your Setup:

1. **Adjust keyword limits** based on your needs
2. **Customize Claude prompts** for your niche
3. **Set up monthly tracking** schedule
4. **Create client-facing form** if agency
5. **Add white-label branding** to outputs

---

## 🎓 Learning Resources

### Understand the Data:

- **Search Volume**: Monthly searches for keyword
- **Keyword Difficulty**: How hard to rank (0-100)
- **CPC**: Cost-per-click in Google Ads (indicates commercial value)
- **Position**: Your current ranking (1 = #1 in Google)
- **Opportunity Score**: Custom metric (Volume / Competition)

### SEO Best Practices:

1. **Quick Wins**: Target keywords with volume 100-1000 and difficulty < 30
2. **Content Length**: Match or exceed top-ranking content
3. **SERP Features**: Optimize for Featured Snippets when available
4. **People Also Ask**: Answer these questions in your content
5. **Regular Updates**: Run analysis monthly to track progress

---

## 🤝 Need Help?

### Troubleshooting:
1. Check n8n execution logs
2. Verify all credentials are valid
3. Test with known-working domain first
4. Review API usage limits

### Get Support:
- Open an issue on GitHub
- Check n8n community forum
- Review DataForSEO documentation
- Contact for custom modifications

---

## ✅ Checklist: You're Done When...

- [ ] Workflow imported successfully
- [ ] All credentials configured (DataForSEO, Claude, Google)
- [ ] Workflow activated
- [ ] Test run completed successfully
- [ ] Google Doc report generated
- [ ] Can submit new URLs via webhook
- [ ] Understanding the output reports

**Congratulations! You now have automated SEO intelligence! 🎉**

---

**Time to analyze:** Your first site → `hyroxtrainingplans.com`

Run the test and see the magic happen! 🚀
