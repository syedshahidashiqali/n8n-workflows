# 🚀 AI-Driven B2B Lead Enrichment & Outreach Automation

**Transforming 2-3 hours of manual lead research into 5 minutes of automated intelligence.**

This project is a fully automated B2B lead enrichment and cold outreach pipeline. Built for a Dutch marketing agency, it takes raw leads from Google Sheets, scrapes their business context, analyzes their traditional SEO and Generative AI visibility, and drafts highly personalized outreach emails—all without human intervention.

🏆 **Featured in the DataForSEO December Community Showcase** 🏆  
*"The best builds aren’t defined by size. They’re defined by one thing: they work, and they save time... A pipeline that takes a raw lead list and turns it into a usable outreach sheet." — DataForSEO*

---

## 🛑 The Problem
Sales and marketing teams often have lists of leads but zero context about the companies. To write a compelling, non-salesy outreach email, SDRs spend hours manually researching:
* What the company actually does.
* What keywords they rank for.
* Who their competitors are.
* How they are positioned in the market.

## 💡 The Solution
This workflow automates the entire research and copywriting phase. By simply dropping a lead into a Google Sheet, the system automatically returns a complete intelligence report and a ready-to-send personalized email. 

### ✨ The Game Changer: LLM Visibility Score (GEO)
Traditional SEO tells you where a company ranks on Google. But today's buyers are starting their searches on ChatGPT and Claude. 

This system introduces an **"AI Visibility Score" (0-10)**. It queries LLMs to see how often a lead's brand is recommended versus their competitors. This allows agencies to pitch Generative Engine Optimization (GEO) services based on hard data.

---

## ⚙️ How It Works (The Pipeline)

1. **Trigger:** A new lead is added to Google Sheets (Name, Domain, Email, Language).
2. **Scraping:** Jina AI scrapes the lead's website to understand their business model.
3. **SEO Analysis:** DataForSEO API pulls the top 20 ranking keywords and identifies the top 3 organic competitors.
4. **AI Visibility Check:** The system dynamically queries ChatGPT via DataForSEO to check if the lead is recommended for their top keywords, calculating a custom 0-10 visibility score.
5. **Email Generation:** OpenAI (GPT-4o-mini) analyzes the gathered intelligence to draft a highly personalized, data-driven cold email (under 150 words) along with 3 unique subject lines and preview text.
6. **Delivery:** The enriched data and email drafts are pushed back into the Google Sheet.

### What Each Lead Gets:
* 📊 **Business Overview** (2-sentence summary of what they do)
* 🔍 **Top 20 SEO Keywords**
* 🏆 **Main Competitors** (Domain + why their SEO is strong)
* 🤖 **LLM Visibility Score** (0-10 rating on AI search presence)
* ✉️ **Ready-to-send personalized email** (in English or Dutch)

---

## 🛠️ Tech Stack

* **[n8n](https://n8n.io/):** The automation backbone orchestrating the entire workflow.
* **[DataForSEO](https://dataforseo.com/):** Powers the SEO layer (Keywords, SERP Competitors, LLM Brand Mentions).
* **[OpenAI (GPT-4o-mini)](https://openai.com/):** Analyzes data and generates the localized outreach copy.
* **[Jina AI](https://jina.ai/):** Extracts clean, readable text from target websites.
* **Google Sheets API:** Serves as the database and user interface for the sales team.

---

## 👤 Author

**Syed Shahid Ali** Founder @ CodeFlow Nexus | Building AI-Driven Automation & Scalable Software Systems  
*Connect with me on [LinkedIn](https://www.linkedin.com/in/syed-shahid-ali-ssa/) to see more AI automation builds.*