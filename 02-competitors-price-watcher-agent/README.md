# 🛒 Automated B2B Price Monitoring & PDP Discovery System

**Real-time market intelligence to prevent pricing disruptions and monitor retailer compliance.**

This project is a multi-stage automation pipeline built for a Dutch wholesale distributor. It automatically discovers product pages across major retail partners, verifies the matches using AI, and monitors sales prices multiple times a day to instantly catch unauthorized price drops.

---

## 🛑 The Problem
In B2B distribution, when one major retailer drops a product's price below the Suggested Retail Price (SRP), it triggers a chain reaction. Other retailers complain and demand lower wholesale prices, destroying margins. 
Manually finding Product Detail Pages (PDPs) across different retailers and checking them daily for a large catalog is impossible.

## 💡 The Solution
A fully automated n8n architecture that handles everything from discovering the URLs to historical price logging. 

This system takes a list of EANs/SKUs from Airtable, searches target retailers (`cameranu.nl`, `kamera-express.nl`), completely bypasses their anti-scraping tools, and logs the current "Buy Box" price into a historical database. It also directly integrates with the client's internal system (ProductFlow) to fetch their own marketplace prices.

### ✨ The Engineering Highlight: Strict AI Product Validation
When searching a retailer's site via EAN, the search engine might return an accessory (e.g., a battery for a camera) instead of the camera itself. 

To prevent logging incorrect prices, this system uses **GPT-4o-mini** as a strict product identity classifier. Before saving a discovered PDP URL, the LLM compares the internal Airtable description with the scraped retailer title. It categorizes the match as `CERTAIN_MATCH`, `CERTAIN_NOT_MATCH`, or `UNSURE`. Only 100% certain matches are automatically added to the daily scraping queue; the rest are flagged for human review.

---

## ⚙️ How It Works (The Architecture)

This system is broken down into three distinct, decoupled workflow modules:

### Phase 1: PDP Discovery (Workflows 1.1 & 1.2)
* **Trigger:** Runs weekly (or manually for new products).
* **Action:** Fetches products missing a PDP URL from Airtable. 
* **Search & Bypass:** Uses [Scrappey](https://scrappey.com/) to bypass Cloudflare/anti-bot protections and searches the retailer's site using the product EAN.
* **AI Validation:** Extracts the resulting product title and URL, passing it to OpenAI to ensure the scraped product exactly matches the internal catalog.
* **Storage:** Saves the verified PDP URL back to Airtable.

### Phase 2: Competitor Price Scraping (Workflows 2.1 & 2.2)
* **Trigger:** Runs 3x daily (6 AM, 12 PM, 6 PM).
* **Action:** Fetches all verified PDP URLs from Airtable.
* **Extraction:** Visits the exact PDPs via Scrappey, parses the DOM, and extracts the current selling price via CSS selectors.
* **History Logging:** Formats the price and pushes it to an Airtable `Price History` table, creating a time-series database for trend analysis.

### Phase 3: Internal Marketplace Pricing (Workflows 3.1 & 3.2)
* **Trigger:** Runs daily.
* **Action:** Bypasses scraping entirely for the client's own direct-to-consumer brand.
* **Integration:** Connects to the **ProductFlow API** to fetch live marketplace offers (Bol.com, Amazon NL, Amazon DE).
* **Calculation:** Computes the final adjusted prices and logs them alongside the competitor data in Airtable.

---

## 🛠️ Tech Stack

* **[n8n](https://n8n.io/):** The orchestration engine managing schedules, batching, and routing.
* **[Airtable](https://airtable.com/):** Acts as the central Headless CMS and time-series database for historical prices.
* **[Scrappey API](https://scrappey.com/):** Handles proxy rotation, browser fingerprinting, and Cloudflare bypass to scrape protected e-commerce sites.
* **[OpenAI (GPT-4o-mini)](https://openai.com/):** Processes fuzzy logic for strict product identity matching.
* **ProductFlow API:** Provides direct access to internal marketplace pricing data.

---

## 📦 Repository Contents

* `Workflow 1.1 PDP Finder.json`: Batch processor for missing URLs.
* `Workflow 1.2_ PDP Finder.json`: Scraper and AI validator for URL discovery.
* `Workflow 2.1 Price Finder.json`: Batch processor for daily price checks.
* `Workflow 2.2 Price Finder.json`: DOM parser and price logger.
* `Workflow 3.1 Mojo Price Finder.json`: ProductFlow API data cleaner.
* `Workflow 3.2 Mojo Price Finder.json`: Marketplace offer calculator and logger.

---

## 👤 Author

**Syed Shahid Ali** | Founder @ CodeFlow Nexus | Building AI-Driven Automation & Scalable Software Systems  
*Connect with me on [LinkedIn](https://www.linkedin.com/in/syed-shahid-ali-ssa/) to discuss e-commerce automation and scraping architecture.*
