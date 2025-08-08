# Ad Campaign Keyword Strategizer

This notebook provides an automated workflow to analyze and categorize keywords for a digital advertising campaign, specifically for a **Performance Max** campaign on Google Ads. It uses a combination of data processing with pandas and the Gemini API for keyword classification.

The process involves:
1. **Data Ingestion**: Loading campaign details and keyword data.
2. **Data Processing**: Cleaning, merging, and filtering keyword data.
3. **AI-Powered Thematic Grouping**: Using the Gemini API to intelligently group keywords into logical ad themes.
4. **Report Generation**: Creating a detailed HTML report summarizing the strategic analysis and the final keyword themes.

---

## 🚀 Workflow Breakdown

### 1. Data Ingestion & Configuration

The workflow begins by loading configuration data from an `input.yaml` file, which specifies the brand's website, competitor's website, and target service locations. Currently, we scrape the keyword data manually from [WordStream](https://tools.wordstream.com/fkt?website=www.cubehq.ai&cid=&camplink=&campname=&geoflow=0) and store them as `.csv` files for the POC code. We shall explore automated ways of doing this by finding developer APIs or web scraping tools.

### 2. Data Processing and Cleaning

We process and clean the data by:

* **Load Keywords**: It loads keyword data for the brand and its competitors into separate pandas DataFrames.
* **Merge DataFrames**: The two DataFrames are concatenated into a single combined DataFrame.
* **Remove Duplicates**: Duplicate keywords are removed to ensure a clean dataset.
* **Filter by Search Volume**: Keywords with a search volume below a predefined threshold (e.g., 500) are filtered out. This focuses the analysis on the most impactful keywords.

### 3. AI-Powered Keyword Classification

The cleaned keyword data is fed into the **Gemini 1.5 Flash** model via the API.

#### 3.1 Prompt Engineering

A carefully designed prompt is created to instruct the model to function as a **Marketing Strategist and Ad Campaign Manager**. The prompt is structured to include **Chain of Thought reasoning**, guiding the model to follow a step-by-step approach. It asks the model to:

* Identify high-value keywords by balancing **high search volume** with **low-to-medium competition**.
* Analyze patterns and brainstorm potential themes.
* Develop a logical grouping strategy.
* Classify keywords into thematic groups, referred to as "asset groups" in the context of a Performance Max campaign.

To enhance the model's understanding, **Few-Shot Prompting** is employed by providing clear examples within the prompt.

#### 3.2 Model Interaction

The model processes the cleaned keyword data and returns a structured **JSON object**. This output includes:

* A strategic analysis of the keywords.
* The final thematic keyword groups, organized logically for campaign optimization.

### 4. Output and Reporting

The final stage of the notebook takes the structured JSON output from the Gemini model and generates a comprehensive HTML report.

* **Report Content**: The report includes:
    * A summary of the AI's **strategic analysis**, including high-value keyword identification and grouping logic.
    * A list of each **thematic keyword group** (asset group).
    * A **rationale** for each theme, explaining the grouping logic.
    * A list of the top keywords selected for each theme.
* **File Generation**: The report is saved as a self-contained HTML file (`asset_group_themes.html`), making it easy to share and review.