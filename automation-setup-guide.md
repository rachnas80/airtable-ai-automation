# 🔄 Automation Setup Guide

This guide explains how the Airtable AI Workflow Automation Dashboard runs end-to-end — from record updates to AI summaries and Slack/Confluence notifications.

---

## ⚙️ 1. Automation Triggers in Airtable

**Trigger:** When a record is updated  
**Conditions:**
- “Migration Status” or “Learning Status” changes
- “Owner” or “Complexity Score” changes
- “Last Updated” is modified

**Action Steps:**
1. **Generate AI Summary**  
   - Field: `AI Summary`  
   - Uses a custom prompt (see `ai-field-prompts.md`)
2. **Send Slack Notification**  
   - Message includes Repo/Project name, Owner, and AI summary  
   - Example:  
     `Repo ABC transitioned from Pending → In Progress (Owner: Jane). AI Summary: Migration 40% complete, low risk.`
3. **Post to Confluence / Google Sheets** *(optional)*  
   - Via n8n or Make webhook integration  
   - Updates the respective section or log row automatically

---

## 🧠 2. Integration Options

| Integration | Purpose | Example Action |
|--------------|----------|----------------|
| **Slack Webhook** | Real-time updates | Post migration summaries to `#migration-status` channel |
| **Google Sheets** | Data backup / reporting | Append updated record info |
| **Confluence API** | Leadership visibility | Auto-update summary tables on wiki pages |
| **Email Notifications** | Targeted alerts | Notify repo owners of risk or blockers |

---

## 📊 3. Interface Dashboard Design

Use Airtable **Interface Designer** to visualize:
- Migration % per Organization
- RAG (Red-Amber-Green) Risk Heatmap
- Top 5 blockers (auto-detected by AI field)
- AI-generated team summaries

**Sections Example:**
| Section | View | Description |
|----------|------|--------------|
| “Overview” | Bar & KPI Charts | % migrated, total repos |
| “Risks” | List View | ⚠️ flagged AI summaries |
| “Team Progress” | Grouped by Owner | Show AI summaries for each engineer/team |

---

## 🔁 4. n8n / Make Workflow (Optional)

**Trigger:** Airtable “Record Updated” webhook  
**Actions:**
1. Fetch record details  
2. Format AI summary into a clean message  
3. Send via Slack or update Confluence page  
4. Log the event in Google Sheets

---

## ✅ 5. Example Slack Output
