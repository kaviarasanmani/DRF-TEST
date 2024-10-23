
# **Athena Phase 1 - End User Guide**



## **1. DashboardView API**

### **Overview**
The `DashboardView` class provides an API endpoint for fetching detailed Google Ads performance metrics. Users can retrieve metrics such as impressions, clicks, cost, conversions, top-performing ads, and destination URLs for a specified date range. This data is aggregated and returned in an easy-to-interpret format for building dashboards or tracking campaign performance.

### **Features**
- Retrieves and calculates overall Google Ads metrics for the specified date range.
- Provides daily metrics to analyze performance trends.
- Retrieves top 10 performing ads based on impressions.
- Retrieves top 10 destination URLs based on click-through performance.

---

### **API Endpoint**

**POST** `/api/dashboard/`

#### **Request Body**
To get the metrics, you need to provide a date range in the request body.

```json
{
  "start_date": "YYYY-MM-DD",
  "end_date": "YYYY-MM-DD"
}
```

- **`start_date`**: The beginning of the date range in "YYYY-MM-DD" format.
- **`end_date`**: The end of the date range in "YYYY-MM-DD" format.

#### **Response Example**

```json
{
  "period": "2024-01-01 to 2024-01-07",
  "overall_metrics": {
    "impressions": 12345,
    "clicks": 6789,
    "cost": 5000,
    "conversions": 123,
    "ctr": 5.67,
    "cpc": 2.34,
    "conversion_rate": 2.1,
    "roas": 3.5
  },
  "daily_metrics": [
    {
      "date": "2024-01-01",
      "spend": 500,
      "clicks": 100,
      "conversions": 5,
      "impressions": 2000
    },
    
  ],
  "top_ads": [
    {
      "campaign_id": "123",
      "campaign_name": "Holiday Sale",
      "impressions": 5000,
      "clicks": 300,
      "cost": 1500,
      "conversions": 10
    },
    
  ],
  "top_destination_urls": [
    {
      "campaign_name": "Holiday Sale",
      "final_urls": ["http://example.com/holiday-sale"],
      "impressions": 1000,
      "clicks": 500,
      "conversions": 5
    },
    
  ]
}
```

---

### **Error Responses**
- **400 BAD REQUEST**: Invalid input or missing required parameters.
  - Example: If `start_date` or `end_date` is missing or incorrectly formatted.
  - Example Response:
    ```json
    {
      "error": "Invalid date format. Use YYYY-MM-DD."
    }
    ```

- **404 NOT FOUND**: No data available for the given date range.
  - Example: No Google Ads data found for the specified date range.
  - Example Response:
    ```json
    {
      "error": "No data available for the specified date range."
    }
    ```

- **500 INTERNAL SERVER ERROR**: Unexpected internal errors, such as Google Ads API issues or data processing errors.
  - Example Response:
    ```json
    {
      "error": "An unexpected error occurred. Please try again later."
    }
    ```

---

### **Methods in Detail**

#### **1. post(self, request)**
- **Description**: Processes POST requests to return Google Ads performance metrics.
- **Usage**: Call this method with a valid `start_date` and `end_date` to get the dashboard data.
- **Response Structure**: The response contains overall campaign metrics, daily breakdowns, top ads, and top URLs.
- **Error Handling**: Handles invalid dates, API issues, and missing data gracefully with appropriate status codes and messages.

---

### **Helper Methods**

#### **2. get_google_ads_client(self)**
- **Description**: Returns the `GoogleAdsClient` object needed to communicate with the Google Ads API.
- **Usage**: This is called internally to set up the Google Ads client using the YAML configuration stored in the `GOOGLE_ADS_YAML_PATH` environment variable.

#### **3. get_metrics(self, client, customer_id, start_date, end_date)**
- **Description**: Fetches key performance metrics like impressions, clicks, cost, and conversions for the specified date range.
- **Returns**: A pandas DataFrame with columns such as impressions, clicks, cost, conversions.
- **Error Handling**: If data retrieval fails, logs the error and returns an appropriate message.

#### **4. calculate_metrics(self, df)**
- **Description**: Aggregates and calculates overall metrics from the data, such as CTR (Click-Through Rate), CPC (Cost Per Click), and ROAS (Return on Ad Spend).
- **Returns**: A dictionary with formatted metrics.

- **Key Calculations**:
  - **CTR (Click-Through Rate)**: `(Clicks / Impressions) * 100`
  - **CPC (Cost Per Click)**: `Cost / Clicks`
  - **ROAS (Return on Ad Spend)**: `Conversion Value / Cost`

#### **5. format_metric(self, value)**
- **Description**: Formats the values, ensuring that floats are rounded to two decimal places or converted to integers where appropriate.
- **Example**: 
  - `format_metric(12345.6789)` → `12,345.68`
  - `format_metric(100)` → `100`

#### **6. get_top_ads(self, client, customer_id, start_date, end_date)**
- **Description**: Retrieves the top 10 ads based on impressions for the given date range.
- **Returns**: A list of dictionaries, each representing an ad with associated metrics like clicks, impressions, cost, and conversions.

#### **7. get_top_destination_urls(self, client, customer_id)**
- **Description**: Fetches the top 10 destination URLs based on clicks over the last 30 days.
- **Returns**: A list of URLs and their associated metrics.

#### **8. get_daily_metrics(self, df, start_date, end_date)**
- **Description**: Extracts and formats daily metrics (e.g., spend, clicks, conversions) for the date range.
- **Returns**: A list of dictionaries, each representing daily metrics.

---

### **Custom Serializers**

#### **DashboardRequestSerializer**
- **Description**: Validates the incoming request to ensure `start_date` and `end_date` are present and properly formatted.
- **Validation Rules**: 
  - Both dates must follow the `YYYY-MM-DD` format.
  - `end_date` should be equal to or after `start_date`.

#### **DashboardResponseSerializerv1**
- **Description**: Formats the output for the response, ensuring the data returned to the client is in the correct structure.
- **Usage**: Automatically called to structure the response for the dashboard.

---

### **User Guide: Common Use Cases**

#### **1. Fetching Metrics for the Last 7 Days**
You can easily retrieve metrics for the last week by making a POST request with the appropriate date range.

```bash
curl -X POST http://api.example.com/api/dashboard/ \
-H "Content-Type: application/json" \
-d '{
  "start_date": "2024-01-01",
  "end_date": "2024-01-07"
}'
```

#### **2. Handling Errors**
Ensure that `start_date` and `end_date` are provided in the correct format. If you don’t get any data, confirm that your Google Ads account has data for the given date range.


##  **2.Winning_campaign API**

### Overview

The **Winning campaign** helps you improve the performance of your Google Ads campaigns by identifying ad sets with high potential and suggesting budget adjustments. By analyzing key performance metrics like **Cost Per Acquisition (CPA)**, **Return on Ad Spend (ROAS)**, and **Click-Through Rate (CTR)**, it finds underused ad sets that can be scaled to deliver better results.

This tool reduces wasted clicks and optimizes ad spend, making it easier to focus on ad sets that bring more value for your budget.
### Features

- **Automated Performance Review:** The tool retrieves and analyzes ad performance data for the last 30 days.
- **Winning Ad Sets Detection:** It identifies high-performing ad sets that have a low CPA and significant conversions.
- **Recommendations for Scaling:** You receive recommendations to increase the budget by 20% for the identified ad sets to maximize their potential.
- **Click Fraud Detection:** Monitors click rates to prevent wasted spend on suspicious or fraudulent clicks.

### Key Metrics to Understand

- **Impressions:** The number of times your ad was displayed.
- **Clicks:** The number of times users clicked on your ad.
- **Conversions:** The number of completed goals (such as purchases or sign-ups) resulting from the ad.
- **CPA (Cost Per Acquisition):** The average cost spent to get one conversion.
- **ROAS (Return on Ad Spend):** How much revenue you generate for every dollar spent on ads.
- **CTR (Click-Through Rate):** The percentage of impressions that turned into clicks.

These metrics help you gauge the effectiveness of your ad sets and determine where to allocate more budget.

---

### How It Works

### Step 1: Retrieve Performance Data

- The tool automatically fetches your **Search Campaign** performance data for the last 30 days, including metrics like impressions, clicks, cost, conversions, and ROAS.

### Step 2: Identify Winning Ad Sets

- **Criteria for Winning Ad Sets:**
  - **Conversions:** The ad set should have at least 10 conversions in the past 30 days.
  - **CPA Threshold:** The ad set should have a CPA lower than ₹1000 (adjustable).
  
  These are the ad sets that have been performing well and are likely to benefit from more budget.

### Step 3: Generate Recommendations

- For each winning ad set, the system calculates a recommended budget increase by 20% (scale factor).
- It provides detailed insights into the current performance, suggested budget, and the expected percentage increase.

---

### User Interface & Recommendations

When accessing the **Wasted Clicks View**, you’ll see a list of high-performing ad sets with the following details:

### Example Display:

| **Campaign** | **Ad Group** | **Impressions** | **Clicks** | **Conversions** | **CPA (₹)** | **ROAS** | **CTR** | **Current Spend (₹)** | **Recommended Budget (₹)** | **Budget Increase (%)** |
|--------------|--------------|-----------------|------------|-----------------|-------------|----------|---------|-----------------------|----------------------------|-------------------------|
| Campaign 1   | Ad Group A   | 20,000          | 1000       | 20              | 800         | 4.2      | 5%      | 20,000                | 24,000                     | 20%                    |
| Campaign 2   | Ad Group B   | 10,000          | 500        | 12              | 950         | 3.5      | 5%      | 15,000                | 18,000                     | 20%                    |

---

### How to Interpret the Results

- **Campaign/Ad Group Information:** Shows which campaign and ad group performed well.
- **Impressions/Clicks:** Gives you an idea of how many people are seeing and interacting with your ad.
- **Conversions:** The number of actions taken based on the ad, such as purchases or sign-ups.
- **CPA (₹):** Helps you understand how much you’re paying for each conversion. A lower CPA indicates good performance.
- **ROAS:** Return on Ad Spend shows how much you’re earning for each rupee spent. The higher the ROAS, the better.
- **CTR:** Indicates how often users clicked on your ad compared to how often it was shown.
- **Current Budget & Recommended Budget:** Shows your current spending and suggests a budget increase of 20% for top-performing ad sets.

### How to Use the Recommendations

### 1. **Increase Budget for Winning Ad Sets**
   - Once you’ve identified the top ad sets, you can apply the recommended 20% budget increase to maximize their potential.
   - This helps ensure that you’re allocating more resources to ad sets that are already performing well and likely to bring more conversions.

### 2. **Monitor CPA and ROAS**
   - Keep an eye on the CPA and ROAS values. A low CPA means you’re paying less for each conversion, while a high ROAS means you’re getting more return for every rupee spent.

### 3. **Review Invalid Click Rates**
   - If the tool detects invalid clicks (like fraud or bot activity), it will alert you. This helps protect your budget by flagging campaigns with a high rate of invalid clicks.

### Error Handling

If something goes wrong, here’s what the system will do:

1. **Google Ads API Error:** If there's an issue with accessing data from the Google Ads API, the system will notify you with an error message like:
   - `"Google Ads API error: {error code}"`
   
2. **Unexpected Errors:** If something unexpected happens, you will see this message:
   - `"An unexpected error occurred: {error message}"`

These error messages help you quickly identify any issues with the system or Google Ads API.


##  **3. Invalid Click Analysis**

This `InvalidClickAnalysisView` class provides an API view that fetches Google Ads campaign data, analyzes invalid clicks, and reports on wasted ad spend due to those clicks. Here's a breakdown of how it works and how users can benefit:

### Key Features:
1. **Data Retrieval:**
   - Fetches campaign metrics, including total clicks, invalid clicks, and costs for the selected date range (defaulting to the past 30 days).
   - Focuses only on active and ongoing campaigns.

2. **Campaign Analysis:**
   - Calculates invalid click rates, cost per click in INR, and the wasted spend due to invalid clicks.
   - Provides a detailed analysis for each campaign, including the percentage of clicks that are invalid.

3. **Summary Statistics:**
   - Offers an overview of key metrics, including the total number of active campaigns, total wasted spend, and high-risk campaigns (those with a higher-than-threshold invalid click rate).

4. **High-Risk Campaigns Identification:**
   - Flags campaigns with an invalid click rate exceeding a predefined threshold (`HIGH_INVALID_CLICK_RATE_THRESHOLD`), helping users focus on campaigns that may be targeted by bots or click fraud.

### Response Structure:
The API response provides:
- **Campaign Analysis:** A detailed list of campaigns with key metrics (clicks, invalid clicks, invalid click rate, and wasted spend).
- **Summary Statistics:** Aggregated data, such as total active campaigns and total wasted ad spend.
- **High-Risk Campaigns:** A separate list highlighting campaigns with unusually high invalid click rates, providing details on the wasted spend for these campaigns.

### How Users Benefit:
1. **Budget Optimization:**
   - Helps users identify campaigns where ad spend is being wasted on invalid clicks, enabling them to take action (e.g., pausing or adjusting bids).
  
2. **Click Fraud Monitoring:**
   - Provides visibility into campaigns that may be experiencing fraudulent activity or non-human interactions, allowing users to mitigate risks by reducing exposure to click fraud.

3. **Actionable Insights:**
   - By highlighting high-risk campaigns, users can focus their efforts on minimizing wasted spend and maximizing the efficiency of their Google Ads campaigns.

### Example Output:

```json
{
  "campaign_analysis": [
    {
      "name": "Campaign A",
      "clicks": 5000,
      "invalid_clicks": 100,
      "invalid_click_rate": "2.00%",
      "wasted_spend_inr": "₹1500.00"
    },
    {
      "name": "Campaign B",
      "clicks": 3000,
      "invalid_clicks": 50,
      "invalid_click_rate": "1.67%",
      "wasted_spend_inr": "₹800.00"
    }
  ],
  "summary_statistics": {
    "total_active_campaigns": 2,
    "total_wasted_spend": "₹2300.00",
    "high_risk_campaigns": 0
  },
  "high_risk_campaigns": []
}
```

## **4. AdPerformance Analysis**

The `AdPerformance Analysis` is designed to help advertisers analyze their ad performance data from Google Ads and generate ad copy suggestions based on top-performing ad groups. This view uses the Google Ads API to retrieve data, processes the data to identify top-performing ad groups, and then leverages the OpenAI API to generate ad suggestions.

#### **Endpoint**
- **Method**: `GET`
- **URL**: `/ad-performance-analysis/`

#### **Description**
The view analyzes Google Ads data for the last 30 days, identifies the top 5 ad groups based on revenue, and generates ad copy suggestions. It also provides recommendations to improve ad performance.

#### **Response Fields**
- **top_ad_groups**: A dictionary containing the top 5 ad groups based on their revenue and spend percentages.
  - `revenue_percent`: Percentage of total revenue generated by the ad group.
  - `spend_percent`: Percentage of total ad spend used by the ad group.
  - `rank`: Rank of the ad group based on total revenue.
  
- **ad_suggestions**: Ad copy suggestions generated based on the top-performing ad groups. Each suggestion includes a headline and two descriptions.
  
- **recommendations**: A list of actionable recommendations to improve ad performance and optimize ad copy creation.

#### **Sample Response**

```json
{
  "top_ad_groups": {
    "ad_group_1": {
      "revenue_percent": 25.34,
      "spend_percent": 20.56,
      "rank": 1
    },
    "ad_group_2": {
      "revenue_percent": 18.75,
      "spend_percent": 15.22,
      "rank": 2
    },
    
  },
  "ad_suggestions": [
    {
      "headline": "Get ₹5000 Off on Mobiles!",
      "description_1": "Fast delivery and no-cost EMI available.",
      "description_2": "Hurry! Limited time offer!"
    },
    {
      "headline": "Upgrade to 5G Mobiles Today!",
      "description_1": "Special discounts on top brands.",
      "description_2": "Get free accessories on your purchase!"
    },
    
  ],
  "recommendations": [
    "Review the generated ad copy suggestions and consider testing them in a controlled environment.",
    "Focus on themes from top-performing ad groups in your new ads.",
    "Continuously monitor performance and iterate on your ad copy.",
    "Always adhere to Google Ads policies when creating new ads.",
    "Consider local cultural nuances and preferences in your ad copy."
  ]
}
```

#### **Error Handling**

- **Google Ads API Error**: If an error occurs while fetching data from the Google Ads API, a 500 status response with an error message will be returned.
  
  ```json
  {
    "error": "Google Ads API error: RESOURCE_EXHAUSTED"
  }
  ```

- **Unexpected Error**: If any other unexpected error occurs, the response will include an error message and the 500 status code.

  ```json
  {
    "error": "An unexpected error occurred: [error details]"
  }
  ```

#### **Internal Methods**

1. **`get_google_ads_client(self)`**
   - Loads the Google Ads client configuration from the `GOOGLE_ADS_YAML_PATH` specified in `settings.py`.

   - **Returns**: The initialized Google Ads client.

2. **`get_ad_performance(self, client, customer_id)`**
   - Queries the Google Ads API for performance data from the last 30 days. It retrieves metrics for impressions, clicks, cost, conversions, and ad group names.
   
   - **Returns**: The raw data from the Google Ads API.

3. **`analyze_top_phrases_and_tags(self, ads_data)`**
   - Processes the raw ad data and extracts phrases from the ad headlines and descriptions. It calculates the total revenue, spend, and impressions for each ad group and ranks them based on revenue.
   
   - **Returns**: A DataFrame with the top 5 ad groups, including revenue and spend percentages, impressions, and rank.

4. **`generate_ad_suggestions(self, top_ad_groups)`**
   - Calls the OpenAI API to generate ad copy suggestions based on the top-performing ad groups. The suggestions are tailored for an Indian audience, considering cultural nuances and using INR for price mentions.
   
   - **Returns**: A list of ad copy suggestions (headline and descriptions).

#### **Example Flow**

1. **Data Retrieval**:
   - The view fetches ad performance data from Google Ads, filtering it to only include the last 30 days.

2. **Data Processing**:
   - The ad data is processed to aggregate metrics (impressions, clicks, costs, conversions) by ad group, and the top ad groups are identified based on revenue.

3. **Ad Copy Generation**:
   - Based on the themes of the top-performing ad groups, ad copy suggestions are generated using OpenAI's `gpt-3.5-turbo` model. The suggestions are tailored to the Indian market.

4. **Recommendations**:
   - The view generates actionable recommendations for the user to optimize their ad campaigns based on the data analysis.

#### **Recommendations Provided**

1. Review the generated ad copy suggestions and consider testing them in a controlled environment.
2. Focus on themes from top-performing ad groups in your new ads.
3. Continuously monitor performance and iterate on your ad copy.
4. Always adhere to Google Ads policies when creating new ads.
5. Consider local cultural nuances and preferences in your ad copy.



Here is the documentation for your `CampaignScalingRecommendationView` class, similar to the format from the previous code:

---

## **5. Campaign Scaling Recommendation**
The `Campaign Scaling Recommendation` is a Django Rest Framework `APIView` designed to provide recommendations for scaling Google Ads campaigns. It interacts with the Google Ads API to identify high-performing campaigns based on their Return on Ad Spend (ROAS) and makes suggestions for increasing the budget for these campaigns.
### Methods

##### `get(self, request)`
Handles GET requests for scaling recommendations.

- **Purpose**: Fetches scalable Google Ads campaigns and generates budget recommendations.
- **Response**: A JSON response containing:
  - `recommendations`: A list of campaign scaling recommendations, including the current and recommended budgets.
  - `total_campaigns_for_scaling`: The total number of campaigns recommended for scaling.
- **Errors**: Returns detailed error messages in case of Google Ads API failure or unexpected issues.

##### `get_google_ads_client(self)`
- **Purpose**: Instantiates and returns a Google Ads client using the credentials stored in the YAML file.
- **Returns**: A `GoogleAdsClient` instance loaded from the file path specified in the `GOOGLE_ADS_YAML_PATH` setting.

##### `get_scalable_campaigns(self, client, customer_id)`
- **Purpose**: Queries the Google Ads API for enabled campaigns from the last 7 days, checking each campaign’s ROAS and other performance metrics.
- **Input Parameters**:
  - `client`: A `GoogleAdsClient` instance.
  - `customer_id`: The Google Ads customer ID for the account.
- **Returns**: A list of campaigns that are eligible for scaling based on the following criteria:
  - The ROAS (Return on Ad Spend) for the past 7 days is greater than 10.
  - The campaign has been running for more than 72 hours.

- **Google Ads Query**:
  - The query selects the campaign ID, name, ROAS, cost, start date, budget, and status.
  - Filters only campaigns that are currently enabled and that have data for the last 7 days.

##### `generate_recommendations(self, scalable_campaigns, scale_factor=1.2)`
- **Purpose**: Generates recommendations for scaling campaign budgets.
- **Input Parameters**:
  - `scalable_campaigns`: A list of campaigns identified as suitable for scaling.
  - `scale_factor`: The factor by which to increase the current campaign budget. The default value is 1.2 (i.e., a 20% increase).
- **Returns**: A list of recommendations, where each recommendation contains:
  - `campaign_id`: The ID of the campaign.
  - `campaign_name`: The name of the campaign.
  - `current_budget`: The current daily budget of the campaign.
  - `recommended_budget`: The new recommended budget after scaling.
  - `roas_7d`: The ROAS (Return on Ad Spend) for the past 7 days.

---

#### Error Handling

- **GoogleAdsException**: Catches any errors related to the Google Ads API, logs the error, and returns an error response with a 500 status.
- **General Exception**: Catches any other unexpected exceptions, logs the error, and returns a generic error message with a 500 status.

---

#### Example Response

```json
{
  "recommendations": [
    {
      "campaign_id": "123456789",
      "campaign_name": "Summer Sale Campaign",
      "current_budget": 5000.00,
      "recommended_budget": 6000.00,
      "roas_7d": 12.5
    },
    {
      "campaign_id": "987654321",
      "campaign_name": "New Year Campaign",
      "current_budget": 10000.00,
      "recommended_budget": 12000.00,
      "roas_7d": 15.2
    }
  ],
  "total_campaigns_for_scaling": 2
}
```


Here is the documentation for your `AdPerformanceRecommendationView` class in a similar format as requested:

---

## **6.AdPerformance Recommendation**

The `AdPerformance Recommendation` is a Django Rest Framework `APIView` that provides performance analysis of Google Ads campaigns. It retrieves data on campaign performance, analyzes the metrics, and makes recommendations for improving campaign efficiency, such as adjusting the budget or improving ad relevance.
### Methods

##### `get(self, request)`
Handles GET requests to analyze the performance of ads and return actionable recommendations.

- **Purpose**: Fetches Google Ads campaign performance for the last 30 days and generates improvement recommendations based on metrics like Cost per Conversion, CTR (Click-Through Rate), and Cost per Click.
- **Response**: A JSON response containing:
  - `recommendations`: A list of performance-based recommendations for each campaign.
  - `total_recommendations`: The total number of recommendations generated.
- **Errors**: Handles and logs Google Ads API-related and unexpected errors, returning appropriate error responses.

##### `get_google_ads_client(self)`
- **Purpose**: Instantiates and returns a Google Ads client using the credentials stored in the YAML file.
- **Returns**: A `GoogleAdsClient` instance loaded from the file path specified in the `GOOGLE_ADS_YAML_PATH` setting.

##### `analyze_ad_performance(self, client, customer_id)`
- **Purpose**: Analyzes the performance of active Google Ads campaigns over the past 30 days.
- **Input Parameters**:
  - `client`: A `GoogleAdsClient` instance.
  - `customer_id`: The Google Ads customer ID for the account.
- **Returns**: A list of recommendations based on the following metrics:
  - **Cost per Conversion (CPA)**: If the cost per conversion is higher than the defined `TARGET_CPA` in settings, a recommendation is generated to reduce the campaign budget.
  - **No Conversions with High Cost**: If a campaign has spent more than the `COST_THRESHOLD` but has no conversions, a recommendation is generated to review its effectiveness.
  - **Low CTR (Click-Through Rate)**: If the CTR is lower than the `CTR_THRESHOLD`, a recommendation is generated to improve the ad relevance.

- **Google Ads Query**:
  - The query selects the campaign ID, name, cost, conversions, clicks, and impressions over the last 30 days, filtering for enabled campaigns that are currently serving ads.

##### `format_inr(self, amount)`
- **Purpose**: Formats monetary values in Indian Rupees.
- **Input Parameters**:
  - `amount`: The amount to be formatted.
- **Returns**: The formatted string representation of the amount in INR (Indian Rupees), prefixed with `₹`.

---

#### Error Handling

- **GoogleAdsException**: Catches errors related to the Google Ads API, logs them, and returns a 500 error response indicating the specific Google Ads API error.
- **General Exception**: Catches unexpected exceptions, logs them, and returns a generic error message with a 500 status.

---

#### Example Response

```json
{
  "recommendations": [
    {
      "campaign_id": "123456789",
      "campaign_name": "Holiday Campaign",
      "recommendation": "Consider reducing budget. Cost per conversion (₹550.00) is higher than target (₹500.00).",
      "metrics": {
        "cost": "₹11,000.00",
        "conversions": 20,
        "cpc": "₹55.00",
        "ctr": "2.50%"
      }
    },
    {
      "campaign_id": "987654321",
      "campaign_name": "Summer Sales Campaign",
      "recommendation": "Review campaign effectiveness. Spent ₹15,000.00 with no conversions.",
      "metrics": {
        "cost": "₹15,000.00",
        "conversions": 0,
        "cpc": "₹50.00",
        "ctr": "1.20%"
      }
    }
  ],
  "total_recommendations": 2
}
```
#### Recommendations Logic

1. **High Cost per Conversion**:
   - If the cost per conversion exceeds the `TARGET_CPA` from settings, the system will recommend reducing the campaign’s budget to align costs with the desired CPA target.

2. **No Conversions with High Spend**:
   - If a campaign has spent more than the `COST_THRESHOLD` without any conversions, the system will recommend reviewing the campaign for effectiveness and possible adjustments.

3. **Low CTR**:
   - If the campaign’s CTR (Click-Through Rate) falls below the `CTR_THRESHOLD`, the system will suggest improving the ad's relevance to increase click rates.

Here’s the documentation for the `OverspendingAdsView` class, structured similarly to the previous documentation style:

---

## **7. Overspending Ads**

The `Overspending Ads` class is a Django REST Framework API view designed to analyze Google Ads performance and provide recommendations for campaigns and ad groups that are overspending based on specified thresholds. The class utilizes the Google Ads API to gather performance metrics and can leverage OpenAI's GPT-3.5 to generate actionable recommendations.

### Methods

### `get(self, request)`

Handles GET requests to retrieve overspending ads recommendations.

#### Parameters
- **request**: The incoming HTTP request containing query parameters for analysis.

#### Query Parameters
- **target_cpa**: The target cost per acquisition. Default is **3500**.
- **cost_threshold**: The maximum allowable cost before a warning is generated. Default is **7000**.
- **ctr_threshold**: The minimum click-through rate percentage to trigger a warning. Default is **1.0**.

#### Returns
- **Response**: JSON object containing:
  - `campaign_recommendations`: List of recommendations for campaigns.
  - `adgroup_recommendations`: List of recommendations for ad groups.
  - `parameters`: The parameters used for analysis.

#### Error Handling
- Returns an error response for various exceptions:
  - **GoogleAdsException**: Returns a 500 status with error details from the Google Ads API.
  - **Timeout**: Returns a 504 status indicating a request timeout.
  - **Exception**: Catches all other exceptions and returns a 500 status with the error message.

### `get_google_ads_client(self)`

Creates and returns a Google Ads client using credentials from the specified YAML configuration file.

#### Returns
- **GoogleAdsClient**: An instance of the Google Ads client.

### `analyze_performance(self, client, customer_id, target_cpa, cost_threshold, ctr_threshold)`

Analyzes the performance of campaigns and ad groups over the last 30 days and returns recommendations for overspending entities.

#### Parameters
- **client**: An instance of the Google Ads client.
- **customer_id**: The Google Ads customer ID to analyze.
- **target_cpa**: The target cost per acquisition.
- **cost_threshold**: The maximum allowable cost.
- **ctr_threshold**: The minimum click-through rate percentage.

#### Returns
- **tuple**: A tuple containing:
  - `campaign_recommendations`: List of campaign recommendations.
  - `adgroup_recommendations`: List of ad group recommendations.

### `analyze_entity(self, row, entity_type, target_cpa, cost_threshold, ctr_threshold)`

Analyzes a specific campaign or ad group entity to determine if it meets performance standards and generates recommendations if necessary.

#### Parameters
- **row**: The data row from Google Ads API response.
- **entity_type**: Type of entity being analyzed ("campaign" or "ad_group").
- **target_cpa**: The target cost per acquisition.
- **cost_threshold**: The maximum allowable cost.
- **ctr_threshold**: The minimum click-through rate percentage.

#### Returns
- **dict** or **None**: A dictionary containing entity details and issues if any problems are found; otherwise, returns None.

### `get_ai_recommendations_with_fallback(self, entity_type, campaign_type, issues, metrics)`

Retrieves AI-generated recommendations, falling back to rule-based recommendations if the AI call fails.

#### Parameters
- **entity_type**: The type of entity ("campaign" or "ad_group").
- **campaign_type**: The advertising channel type of the campaign.
- **issues**: List of identified issues for the entity.
- **metrics**: A dictionary containing performance metrics.

#### Returns
- **list**: List of recommendations, either from AI or fallback options.

### `get_ai_recommendations(self, entity_type, campaign_type, issues, metrics)`

Fetches AI-generated recommendations from OpenAI based on the provided parameters.

#### Parameters
- **entity_type**: The type of entity ("campaign" or "ad_group").
- **campaign_type**: The advertising channel type of the campaign.
- **issues**: List of identified issues for the entity.
- **metrics**: A dictionary containing performance metrics.

#### Returns
- **list**: Formatted list of AI recommendations.

### `get_fallback_recommendations(self, entity_type, campaign_type, issues)`

Generates basic fallback recommendations based on identified issues if AI recommendations are unavailable.

#### Parameters
- **entity_type**: The type of entity ("campaign" or "ad_group").
- **campaign_type**: The advertising channel type of the campaign.
- **issues**: List of identified issues for the entity.

#### Returns
- **list**: List of fallback recommendations.

### `format_ai_recommendations(self, ai_response)`

Formats the AI response into a structured list of recommendations.

#### Parameters
- **ai_response**: The raw response string from the AI.

#### Returns
- **list**: List of formatted recommendations.

### `format_inr(self, amount)`

Formats a numeric amount into Indian Rupees.

#### Parameters
- **amount**: The numeric amount to format.

#### Returns
- **str**: Formatted amount as a string in INR.


Here’s the documentation for the `AdSetPerformanceAnalysisView` class, structured in a similar format as the previous documentation:

---

## **8. AdSet Performance Analysis**

The `AdSetPerformanceAnalysisView` class is a Django REST Framework API view designed to analyze the performance of ad sets within Google Ads. It retrieves performance metrics such as clicks, impressions, and conversions, and generates recommendations based on user-defined thresholds for Click-Through Rate (CTR), Cost Per Click (CPC), and Conversion Rate. The class also suggests budget increases based on performance evaluations.

### Constants

### `MICRO_TO_INR`
- **Type**: `int`
- **Description**: A conversion factor to convert cost from micros to Indian Rupees. The value is set to **1,000,000**.

### Methods

### `get(self, request)`

Handles GET requests to retrieve the performance analysis of ad sets.

#### Parameters
- **request**: The incoming HTTP request containing query parameters for performance analysis.

#### Query Parameters
- **ctr_threshold**: The threshold for Click-Through Rate (CTR). Default is **0.05**.
- **cpc_threshold**: The threshold for Cost Per Click (CPC). Default is **50**.
- **conversion_rate_threshold**: The threshold for Conversion Rate. Default is **0.02**.
- **budget_increase_percentage**: The percentage increase in budget suggested for well-performing ad sets. Default is **20**.

#### Returns
- **Response**: JSON object containing:
  - `ad_set_performance`: A dictionary with performance analysis for each ad set.
  - `thresholds_used`: The thresholds used for analysis.

#### Error Handling
- Returns an error response for various exceptions:
  - **GoogleAdsException**: Returns a 500 status with error details from the Google Ads API.
  - **Exception**: Catches all other exceptions and returns a 500 status with the error message.

### `get_ad_set_performance(self, client, customer_id)`

Retrieves performance data for ad sets from Google Ads within the last 7 days.

#### Parameters
- **client**: An instance of the Google Ads client.
- **customer_id**: The Google Ads customer ID to retrieve data for.

#### Returns
- **dict**: A dictionary containing aggregated performance metrics for each ad set.

### `analyze_performance(self, ad_sets, ctr_threshold, cpc_threshold, conversion_rate_threshold, budget_increase_percentage)`

Analyzes the performance of the retrieved ad sets against specified thresholds and prepares a structured response.

#### Parameters
- **ad_sets**: The performance data for ad sets.
- **ctr_threshold**: The threshold for Click-Through Rate (CTR).
- **cpc_threshold**: The threshold for Cost Per Click (CPC).
- **conversion_rate_threshold**: The threshold for Conversion Rate.
- **budget_increase_percentage**: The suggested budget increase percentage.

#### Returns
- **dict**: A structured dictionary containing analyzed performance data for each ad set.

### `calculate_metrics(self, data)`

Calculates various performance metrics from the provided ad set data.

#### Parameters
- **data**: A dictionary containing raw performance data for an ad set.

#### Returns
- **dict**: A dictionary with calculated metrics including impressions, clicks, cost, conversions, conversion values, CTR, CPC, conversion rate, and ROAS (Return on Ad Spend).

### `determine_performance_status(self, metrics, ctr_threshold, cpc_threshold, conversion_rate_threshold)`

Determines the performance status of an ad set based on calculated metrics and user-defined thresholds.

#### Parameters
- **metrics**: A dictionary containing calculated metrics for the ad set.
- **ctr_threshold**: The threshold for Click-Through Rate (CTR).
- **cpc_threshold**: The threshold for Cost Per Click (CPC).
- **conversion_rate_threshold**: The threshold for Conversion Rate.

#### Returns
- **list**: A list of performance status indicators (e.g., "Low CTR", "High CPC", "Low Conversion Rate").

### `calculate_budget_increase(self, cost, performance_status, budget_increase_percentage)`

Calculates the suggested budget increase based on the ad set's performance status.

#### Parameters
- **cost**: The current cost of the ad set.
- **performance_status**: The performance status indicators for the ad set.
- **budget_increase_percentage**: The percentage increase to suggest if the ad set is performing well.

#### Returns
- **str**: The suggested budget increase formatted in Indian Rupees, or "N/A" if not applicable.

### `format_inr(amount)`

Formats a numeric amount into a string representation of Indian Rupees.

#### Parameters
- **amount**: The numeric amount to format.

#### Returns
- **str**: Formatted amount as a string in Indian Rupees (INR).


## **9. AdGroup Performance Analysis**

#### Overview
The `AdGroupPerformanceAnalysisView` is a Django REST API view that allows users to analyze the performance of Google Ads ad groups over a specified period. The view retrieves various performance metrics such as clicks, impressions, cost, conversions, and conversion value from the Google Ads API.

#### Methods

##### `post(request)`
Handles POST requests to retrieve ad group performance metrics based on the specified number of days.

- **Parameters:**
  - `request`: The request object containing the following data:
    - `days_to_analyze` (optional, int): Number of days to analyze. Defaults to 30 if not provided.

- **Returns:**
  - `Response`: A JSON response containing:
    - On success (HTTP 200 OK):
      - `data`: A list of performance metrics for ad groups.
      - `analysis_parameters`: 
        - `customer_id`: The Google Ads customer ID.
        - `days_analyzed`: The number of days analyzed.
    - On failure (HTTP 404 NOT FOUND):
      - `error`: A message indicating no data was retrieved from the Google Ads API.
    - On unexpected errors (HTTP 500 INTERNAL SERVER ERROR):
      - `error`: A message describing the error.

- **Exception Handling:**
  - Logs any exceptions that occur during execution and returns an appropriate error response.

##### `get_ad_group_performance(client, customer_id, days_ago)`
Fetches ad group performance metrics from the Google Ads API.

- **Parameters:**
  - `client`: The Google Ads API client instance.
  - `customer_id`: The Google Ads customer ID (string).
  - `days_ago`: The number of days to analyze (int).

- **Returns:**
  - `pd.DataFrame`: A DataFrame containing the ad group performance metrics. Returns an empty DataFrame if no data is found.

- **Exception Handling:**
  - Logs and raises exceptions specific to Google Ads and any unexpected errors.

##### `build_ad_group_performance_query(days_ago)`
Constructs a Google Ads query to retrieve ad group performance metrics for a specified number of days.

- **Parameters:**
  - `days_ago`: The number of days to analyze (int).

- **Returns:**
  - `str`: A formatted query string to be used with the Google Ads API.


##### `process_ad_group_performance_response(response)`
Processes the response from the Google Ads API to extract ad group performance data.

- **Parameters:**
  - `response`: The response object returned by the Google Ads API.

- **Returns:**
  - `list`: A list of dictionaries containing performance data for each ad group.

##### `log_google_ads_exception(ex)`
Logs details of any Google Ads API exceptions encountered.

- **Parameters:**
  - `ex`: The GoogleAdsException instance.

- **Returns:**
  - None

#### Exception Handling
- The view handles exceptions that may occur during the API call, including:
  - **GoogleAdsException**: Specific errors returned by the Google Ads API are logged, and relevant messages are included in the response.
  - **General Exceptions**: Any other errors that occur during execution are logged, and a generic error message is returned.

#### Logging
- The view employs logging at various points to track the flow of execution and capture any errors that arise. This includes logging the start of data retrieval, any attribute errors during data processing, and detailed information about Google Ads exceptions.

### Example Request
```http
POST /ad_group_performance
Content-Type: application/json

{
  "days_to_analyze": 30
}
```

### Example Response
**Success Response (200 OK):**
```json
{
  "data": [
    {
      "date": "2024-10-01",
      "campaign_id": "123456",
      "campaign_name": "Fall Sale",
      "ad_group_id": "654321",
      "ad_group_name": "Ad Group 1",
      "ad_group_status": "ENABLED",
      "clicks": 150,
      "impressions": 2000,
      "cost_micros": 5000000,
      "conversions": 25,
      "conversions_value": 1000
    }
    // More records
  ],
  "analysis_parameters": {
    "customer_id": "customer123",
    "days_analyzed": 30
  }
}
```

**Error Response (404 NOT FOUND):**
```json
{
  "error": "No data retrieved from Google Ads API"
}
```

**Error Response (500 INTERNAL SERVER ERROR):**
```json
{
  "error": "An error occurred: [error message]"
}
```


Here’s the requested documentation for the `AdManagementView` class, following the same structure as the previous documentation provided:

---

##  **10. Ad Management**

#### Overview
The `AdManagementView` is a Django REST API view that allows users to manage Google Ads campaigns and ad groups. It supports actions such as pausing ad groups, adjusting campaign budgets, adjusting ad group budgets, and adjusting campaign bids.
#### Methods

##### `post(request)`
Handles POST requests to manage ad groups and campaigns based on the specified action.

- **Parameters:**
  - `request`: The request object containing the following data:
    - `action` (string): The action to be performed. Possible values include:
      - `pause_ad_groups`: Pauses specified ad groups.
      - `increase_campaign_budgets`: Increases specified campaign budgets.
      - `decrease_campaign_budgets`: Decreases specified campaign budgets.
      - `increase_ad_group_budgets`: Increases specified ad group budgets.
      - `decrease_ad_group_budgets`: Decreases specified ad group budgets.
      - `increase_campaign_bids`: Increases specified campaign bids.
      - `decrease_campaign_bids`: Decreases specified campaign bids.
    - Depending on the action, additional parameters may include:
      - `ad_group_ids`: List of ad group IDs to be paused.
      - `campaign_budgets`: List of dictionaries containing campaign IDs and budget adjustments.
      - `ad_group_budgets`: List of dictionaries containing ad group IDs and budget adjustments.
      - `campaign_bids`: List of dictionaries containing campaign IDs, criterion IDs, and bid adjustments.

- **Returns:**
  - `Response`: A JSON response containing:
    - On success (HTTP 200 OK):
      - `message`: A success message indicating the action taken.
    - On failure (HTTP 400 BAD REQUEST):
      - `error`: A message indicating the action was invalid or no action was specified.
    - On Google Ads API errors (HTTP 500 INTERNAL SERVER ERROR):
      - `error`: A message describing the Google Ads API error.
    - On unexpected errors (HTTP 500 INTERNAL SERVER ERROR):
      - `error`: A message describing the unexpected error.

- **Exception Handling:**
  - Logs any exceptions that occur during execution and returns an appropriate error response.

##### `pause_ad_groups(client, customer_id, ad_group_ids)`
Pauses the specified ad groups.

- **Parameters:**
  - `client`: The Google Ads API client instance.
  - `customer_id`: The Google Ads customer ID (string).
  - `ad_group_ids`: List of ad group IDs to pause.

- **Returns:**
  - None

##### `create_pause_ad_group_operations(client, ad_group_ids)`
Creates operations to pause specified ad groups.

- **Parameters:**
  - `client`: The Google Ads API client instance.
  - `ad_group_ids`: List of ad group IDs to pause.

- **Returns:**
  - `list`: A list of `AdGroupOperation` instances for the ad groups to be paused.

##### `adjust_campaign_budgets(client, customer_id, campaign_budgets, action)`
Adjusts the budgets of specified campaigns based on the action.

- **Parameters:**
  - `client`: The Google Ads API client instance.
  - `customer_id`: The Google Ads customer ID (string).
  - `campaign_budgets`: List of dictionaries containing campaign IDs and budget adjustments.
  - `action`: The action to perform, either `increase_campaign_budgets` or `decrease_campaign_budgets`.

- **Returns:**
  - None

##### `create_campaign_budget_operations(client, campaign_budgets, action)`
Creates operations to adjust the budgets of specified campaigns.

- **Parameters:**
  - `client`: The Google Ads API client instance.
  - `campaign_budgets`: List of dictionaries containing campaign IDs and budget adjustments.
  - `action`: The action to perform, either `increase_campaign_budgets` or `decrease_campaign_budgets`.

- **Returns:**
  - `list`: A list of `CampaignOperation` instances for the campaigns to be adjusted.

##### `adjust_ad_group_budgets(client, customer_id, ad_group_budgets, action)`
Adjusts the budgets of specified ad groups based on the action.

- **Parameters:**
  - `client`: The Google Ads API client instance.
  - `customer_id`: The Google Ads customer ID (string).
  - `ad_group_budgets`: List of dictionaries containing ad group IDs and budget adjustments.
  - `action`: The action to perform, either `increase_ad_group_budgets` or `decrease_ad_group_budgets`.

- **Returns:**
  - None
  
##### `create_ad_group_budget_operations(client, ad_group_budgets, action)`
Creates operations to adjust the budgets of specified ad groups.

- **Parameters:**
  - `client`: The Google Ads API client instance.
  - `ad_group_budgets`: List of dictionaries containing ad group IDs and budget adjustments.
  - `action`: The action to perform, either `increase_ad_group_budgets` or `decrease_ad_group_budgets`.

- **Returns:**
  - `list`: A list of `AdGroupOperation` instances for the ad groups to be adjusted.

##### `adjust_campaign_bids(client, customer_id, campaign_bids, action)`
Adjusts the bids of specified campaigns based on the action.

- **Parameters:**
  - `client`: The Google Ads API client instance.
  - `customer_id`: The Google Ads customer ID (string).
  - `campaign_bids`: List of dictionaries containing campaign IDs, criterion IDs, and bid adjustments.
  - `action`: The action to perform, either `increase_campaign_bids` or `decrease_campaign_bids`.

- **Returns:**
  - None

##### `create_campaign_bid_operations(client, campaign_bids, action)`
Creates operations to adjust the bids of specified campaigns.

- **Parameters:**
  - `client`: The Google Ads API client instance.
  - `campaign_bids`: List of dictionaries containing campaign IDs, criterion IDs, and bid adjustments.
  - `action`: The action to perform, either `increase_campaign_bids` or `decrease_campaign_bids`.

- **Returns:**
  - `list`: A list of `CampaignCriterionOperation` instances for the campaigns to be adjusted.

#### Exception Handling
- The view handles exceptions that may occur during the API calls, including:
  - **GoogleAdsException**: Specific errors returned by the Google Ads API are logged, and relevant messages are included in the response.
  - **General Exceptions**: Any other errors that occur during execution are logged, and a generic error message is returned.

#### Logging
- The view employs logging at various points to track the flow of execution and capture any errors that arise. This includes logging the start of each action, details of the actions performed, and detailed information about Google Ads exceptions.

### Example Request
```http
POST /ad_management
Content-Type: application/json

{
  "action": "pause_ad_groups",
  "ad_group_ids": ["123456", "789012"]
}
```

### Example Response
**Success Response (200 OK):**
```json
{
  "message": "Ad groups paused successfully"
}
```

**Error Response (400 BAD REQUEST):**
```json
{
  "error": "Invalid action specified"
}
```

**Error Response (500 INTERNAL SERVER ERROR):**
```json
{
  "error": "Google Ads API error: [error code name]"
}
```


Here’s the documentation for the `FunnelAnalysis` class that describes its purpose, methods, parameters, return types, and error handling in a similar style to the provided documentation:

---

## **11.FunnelAnalysis Class**

**Purpose**:  
The `FunnelAnalysis` class provides an API endpoint to analyze advertising funnel data using the Google Ads API. It retrieves performance metrics over a specified date range and processes this data to generate insights.

#### Methods

##### `get(request)`

Handles GET requests to retrieve funnel analysis data.

- **Parameters**:
  - `request` (Request): The HTTP request object containing the user's request data.

- **Returns**: 
  - `Response`: A JSON response containing:
    - `overall_summary`: An object summarizing total performance metrics across all campaigns.
    - `day_wise_summary`: An array of objects with daily performance metrics.
    - `campaign_summary`: An array of objects summarizing performance metrics for each campaign.

- **Raises**:
  - `Exception`: Catches and logs any unexpected errors during the data fetching or processing phases. Returns a JSON response with an error message and a 500 status code if data retrieval fails.

#### Private Methods

##### `fetch_funnel_data(client, customer_id, start_date, end_date)`

Fetches funnel data from Google Ads API for the specified date range.

- **Parameters**:
  - `client` (GoogleAdsClient): The Google Ads client instance used to interact with the API.
  - `customer_id` (str): The ID of the Google Ads customer account.
  - `start_date` (date): The start date for the data retrieval.
  - `end_date` (date): The end date for the data retrieval.

- **Returns**:
  - `list`: A list of fetched campaign data rows, or `None` if an error occurs.

- **Raises**:
  - `Exception`: Catches and logs errors encountered while fetching data from the API.

##### `process_funnel_data(data)`

Processes the fetched funnel data into a pandas DataFrame.

- **Parameters**:
  - `data` (list): The list of campaign data rows fetched from Google Ads API.

- **Returns**:
  - `DataFrame`: A DataFrame containing structured funnel data with columns for date, campaign name, impressions, clicks, cost, conversions, and conversion value.

##### `calculate_overall_summary(df)`

Calculates overall summary metrics from the funnel data.

- **Parameters**:
  - `df` (DataFrame): The DataFrame containing processed funnel data.

- **Returns**:
  - `dict`: A dictionary containing overall performance metrics including:
    - Impressions
    - Clicks
    - Cost
    - Conversions
    - Conversion Value
    - CTR (Click-Through Rate)
    - CPC (Cost Per Click)
    - Conversion Rate
    - CPA (Cost Per Acquisition)
    - ROAS (Return On Ad Spend)

##### `calculate_day_wise_summary(df)`

Calculates daily summary metrics from the funnel data.

- **Parameters**:
  - `df` (DataFrame): The DataFrame containing processed funnel data.

- **Returns**:
  - `list`: An array of dictionaries, each containing daily performance metrics.

##### `calculate_campaign_summary(df)`

Calculates summary metrics for each campaign from the funnel data.

- **Parameters**:
  - `df` (DataFrame): The DataFrame containing processed funnel data.

- **Returns**:
  - `list`: An array of dictionaries, each containing performance metrics for individual campaigns.

##### `safe_division(numerator, denominator)`

Performs safe division, avoiding division by zero.

- **Parameters**:
  - `numerator` (float): The numerator value for the division.
  - `denominator` (float): The denominator value for the division.

- **Returns**:
  - `float`: The result of the division or `0` if the denominator is zero.

### Error Handling

The class employs robust error handling by logging any exceptions that occur during data fetching and processing. If any errors arise, an appropriate error message is returned in the API response, and a `500 Internal Server Error` status is provided.


Here’s a structured documentation outline for the `AdCopyInsights` class in your Django REST framework project. This documentation includes details about the class, its methods, and their functionality, similar to the provided example.

---

## **12. Ad CopyInsights**

## Overview
The `Ad CopyInsights` class is an API view that retrieves and processes ad copy performance metrics from the Google Ads API. It provides insights on ad length metrics, emoji performance, link performance, sentiment performance, and the top emojis and links used in ad copy.

## Inheritance
- Inherits from `APIView` and `GoogleAdsClientMixin`.

## Methods

### `get(self, request)`
Handles GET requests to fetch ad copy insights. This method orchestrates the fetching, processing, and calculation of various ad copy performance metrics.

#### Parameters
- `request`: The HTTP request object.

#### Returns
- `Response`: A JSON response containing the calculated performance metrics or an error message if data retrieval fails.

#### Error Handling
- Returns a 500 HTTP status code with an error message if data fetching from the Google Ads API fails or if an exception occurs during processing.

### `calculate_ad_length_metrics(df)`
Calculates metrics based on the length of ad copies.

#### Parameters
- `df`: A DataFrame containing ad copy data.

#### Returns
- `list`: A list of dictionaries, each containing:
  - `length_category`: The category of ad length.
  - `number_of_ads`: The count of ads in this category.
  - `impressions`: Total impressions for this category.
  - `clicks`: Total clicks for this category.
  - `cost`: Total cost incurred for this category.
  - `revenue`: Total revenue generated from this category.
  - `ctr`: Click-through rate, calculated as `(clicks / impressions) * 100`.
  - `cpc`: Cost per click, calculated as `(cost / clicks)`.
  - `conversion_rate`: Conversion rate, calculated as `(revenue / cost) * 100`.

### `calculate_emoji_performance(df)`
Analyzes the performance of emojis used in ad copies.

#### Parameters
- `df`: A DataFrame containing ad copy data.

#### Returns
- `list`: A list of dictionaries, each containing:
  - `emoji_count_category`: The category based on the number of emojis used.
  - `number_of_ads`: The count of ads in this category.
  - `revenue`: Total revenue generated from this category.
  - `cost`: Total cost incurred for this category.
  - `impressions`: Total impressions for this category.
  - `clicks`: Total clicks for this category.
  - `revenue_percentage`: Percentage of total revenue.
  - `cost_percentage`: Percentage of total cost.
  - `ctr`: Click-through rate.
  - `conversion_rate`: Conversion rate.

### `calculate_link_performance(df)`
Evaluates the performance of ads based on the presence of links in the final URLs.

#### Parameters
- `df`: A DataFrame containing ad copy data.

#### Returns
- `list`: A list of dictionaries containing:
  - `has_link`: Boolean indicating if links are present.
  - `number_of_ads`: The count of ads in this category.
  - `revenue`: Total revenue generated from this category.
  - `cost`: Total cost incurred for this category.
  - `impressions`: Total impressions for this category.
  - `clicks`: Total clicks for this category.
  - `revenue_percentage`: Percentage of total revenue.
  - `cost_percentage`: Percentage of total cost.
  - `ctr`: Click-through rate.
  - `conversion_rate`: Conversion rate.

### `calculate_sentiment_performance(df)`
Assesses the performance of ads based on sentiment analysis.

#### Parameters
- `df`: A DataFrame containing ad copy data.

#### Returns
- `list`: A list of dictionaries, each containing:
  - `sentiment`: The sentiment category of the ad.
  - `number_of_ads`: The count of ads in this sentiment category.
  - `revenue`: Total revenue generated.
  - `cost`: Total cost incurred.
  - `impressions`: Total impressions.
  - `clicks`: Total clicks.
  - `sentiment_score`: Average sentiment score.
  - `revenue_percentage`: Percentage of total revenue.
  - `cost_percentage`: Percentage of total cost.
  - `ctr`: Click-through rate.
  - `conversion_rate`: Conversion rate.

### `get_top_emojis(df)`
Identifies the top-performing emojis in ad copies.

#### Parameters
- `df`: A DataFrame containing ad copy data.

#### Returns
- `list`: A list of dictionaries for the top emojis, each containing:
  - `emoji`: The emoji character.
  - `count`: Number of occurrences of the emoji.
  - `revenue`: Total revenue generated with this emoji.
  - `cost`: Total cost incurred with this emoji.
  - `impressions`: Total impressions for ads containing this emoji.
  - `clicks`: Total clicks for ads containing this emoji.
  - `number_of_ads`: The count of ads using this emoji.
  - `ctr`: Click-through rate.
  - `conversion_rate`: Conversion rate.

### `get_top_links(df)`
Identifies the top-performing links in ad copies.

#### Parameters
- `df`: A DataFrame containing ad copy data.

#### Returns
- `list`: A list of dictionaries for the top links, each containing:
  - `link`: The URL of the link.
  - `count`: Number of occurrences of the link.
  - `revenue`: Total revenue generated from ads containing this link.
  - `cost`: Total cost incurred from ads containing this link.
  - `impressions`: Total impressions for ads containing this link.
  - `clicks`: Total clicks for ads containing this link.
  - `number_of_ads`: The count of ads using this link.
  - `ctr`: Click-through rate.
  - `conversion_rate`: Conversion rate.

### `replace_nan_with_none(obj)`
Recursively replaces NaN and infinite values with `None`.

#### Parameters
- `obj`: The object to be processed (can be a dict, list, float, etc.).

#### Returns
- The input object with NaN and infinite values replaced with `None`.



## **13. Overspending Ads**

This view analyzes the performance of Google Ads campaigns and ad groups to identify overspending issues. It provides recommendations based on specified performance thresholds.

### Methods

#### `get(self, request)`

-   **Description**: Handles GET requests to analyze campaign and ad group performance.
-   **Parameters**:
    -   `target_cpa` (float, optional): Target Cost Per Acquisition (CPA). Defaults to 3500.
    -   `cost_threshold` (float, optional): Threshold for maximum allowable cost. Defaults to 7000.
    -   `ctr_threshold` (float, optional): Threshold for Click-Through Rate (CTR). Defaults to 1.0.
-   **Returns**: A JSON response containing:
    -   `campaign_recommendations`: List of recommendations for campaigns.
    -   `adgroup_recommendations`: List of recommendations for ad groups.
    -   `parameters`: The parameters used for analysis.
-   **Error Handling**:
    -   `GoogleAdsException`: Logs and returns a 500 error with the Google Ads API error message.
    -   `Timeout`: Returns a 504 error if the request times out.
    -   General exceptions: Logs the error and returns a 500 error.

#### `get_google_ads_client(self)`

-   **Description**: Loads and returns a Google Ads client using the configuration specified in the settings.
-   **Returns**: An instance of `GoogleAdsClient`.

#### `analyze_performance(self, client, customer_id, target_cpa, cost_threshold, ctr_threshold)`

-   **Description**: Analyzes campaign and ad group performance over the last 30 days based on the provided parameters.
-   **Parameters**:
    -   `client`: The Google Ads client instance.
    -   `customer_id`: The Google Ads customer ID.
    -   `target_cpa`: Target CPA for analysis.
    -   `cost_threshold`: Maximum cost threshold.
    -   `ctr_threshold`: Minimum CTR threshold.
-   **Returns**: A tuple containing:
    -   `campaign_recommendations`: List of campaign recommendations.
    -   `adgroup_recommendations`: List of ad group recommendations.

#### `analyze_entity(self, row, entity_type, target_cpa, cost_threshold, ctr_threshold)`

-   **Description**: Analyzes a single campaign or ad group entity and identifies issues based on performance metrics.
-   **Parameters**:
    -   `row`: The row of data representing the entity.
    -   `entity_type`: Type of entity ('campaign' or 'ad_group').
    -   `target_cpa`, `cost_threshold`, `ctr_threshold`: Threshold values for analysis.
-   **Returns**: A dictionary containing identified issues, recommendations, and performance metrics, or `None` if no issues are found.

#### `get_ai_recommendations_with_fallback(self, entity_type, campaign_type, issues, metrics)`

-   **Description**: Obtains AI-generated recommendations with a fallback to basic recommendations in case of failure.
-   **Parameters**:
    -   `entity_type`: Type of entity ('campaign' or 'ad_group').
    -   `campaign_type`: Type of campaign.
    -   `issues`: List of identified issues.
    -   `metrics`: Dictionary of performance metrics.
-   **Returns**: A list of recommendations.

#### `get_ai_recommendations(self, entity_type, campaign_type, issues, metrics)`

-   **Description**: Sends a prompt to OpenAI’s API to receive recommendations for improving ad performance based on identified issues.
-   **Parameters**: Same as `get_ai_recommendations_with_fallback`.
-   **Returns**: A list of formatted AI-generated recommendations.

#### `get_fallback_recommendations(self, entity_type, campaign_type, issues)`

-   **Description**: Provides basic, rule-based recommendations based on identified issues.
-   **Parameters**: Same as `get_ai_recommendations_with_fallback`.
-   **Returns**: A list of fallback recommendations.

#### `format_ai_recommendations(self, ai_response)`

-   **Description**: Formats the AI response into a structured list of recommendations.
-   **Parameters**:
    -   `ai_response`: Raw response string from the AI API.
-   **Returns**: A structured list of recommendations.

#### `format_inr(self, amount)`

-   **Description**: Formats a given amount into Indian Rupees (INR).
-   **Parameters**:
    -   `amount`: The numeric amount to format.
-   **Returns**: A string representation of the amount in INR.


Here's a structured documentation for the `StopLossAutomation1` class, detailing its purpose, methods, and usage. This format follows the standard conventions for API documentation.

---



## **14. StopLossAutomation**
The `StopLossAutomation1` class is an API view designed for automating stop-loss strategies in Google Ads campaigns. It identifies underperforming ads based on specified budget and conversion thresholds and provides actionable suggestions to improve ad performance.

### POST /stop-loss-automation/

**Description**: This method handles the incoming POST request to analyze ad performance and suggest improvements.

#### Request Body
The request body should contain the following fields:

| Field                 | Type    | Description                                               |
|-----------------------|---------|-----------------------------------------------------------|
| `budget_threshold`    | float   | The budget threshold in INR to determine underperforming ads. |
| `conversion_threshold`| int     | The maximum number of conversions below which ads are considered underperforming. |

#### Response
- **200 OK**: Returns a list of underperforming ads with suggestions for improvement.
- **400 Bad Request**: Returns validation errors or Google Ads errors.

#### Example Request
```json
{
  "budget_threshold": 1000,
  "conversion_threshold": 5
}
```

#### Example Response
```json
[
  {
    "campaign_id": "123456789",
    "campaign_name": "Campaign A",
    "ad_group_id": "987654321",
    "ad_group_name": "Ad Group 1",
    "ad_id": "54321",
    "ad_name": "Ad Title",
    "cost_inr": 1200.00,
    "conversions": 3,
    "suggestions": [
      "Consider making the ad name more descriptive",
      "Try adding action verbs to make the ad more compelling"
    ]
  }
]
```

#### get_underperforming_ads(client, customer_id, budget_threshold, conversion_threshold)

**Description**: Retrieves a list of underperforming ads based on the specified budget and conversion thresholds.

##### Parameters
- `client`: An instance of the Google Ads API client.
- `customer_id`: The customer ID for the Google Ads account.
- `budget_threshold`: The budget threshold to filter ads.
- `conversion_threshold`: The conversion threshold to filter ads.

##### Returns
A list of dictionaries, each representing an underperforming ad with its details.

#### generate_suggestions(ads)

**Description**: Analyzes ad names using NLP to generate suggestions for improvement.

##### Parameters
- `ads`: A list of dictionaries containing details of underperforming ads.

##### Returns
The input list of ads, enriched with suggestions for each ad.

#### format_google_ads_errors(exception)

**Description**: Formats errors from the Google Ads API exception into a list of readable messages.

##### Parameters
- `exception`: An instance of `GoogleAdsException`.

##### Returns
A list of error messages.

### Example Usage

1. **Send a POST request** to the `/stop-loss-automation/` endpoint with the necessary parameters.
2. **Receive a response** containing the details of underperforming ads and suggestions for improving their performance.



Here’s a structured documentation for the `AIBuiddingOpenTarget` class, detailing its purpose, methods, parameters, and usage. This documentation follows standard API documentation practices.

---

## **15. AI Buidding OpenTarget**

## Overview
The `AIBuiddingOpenTarget` class is an API view designed to analyze the performance of Google Ads campaigns. It retrieves performance data for enabled campaigns, performs data analysis, and provides actionable insights based on the analysis.

## Methods

### POST /ai-building-open-target/

**Description**: This method handles the incoming POST request to fetch campaign performance data and return analysis results.

#### Request Body
The POST request does not require a specific request body but should include authentication as necessary.

#### Response
- **200 OK**: Returns a list of analyzed campaign performance data.
- **400 Bad Request**: Returns an error message if the customer ID is not configured.
- **500 Internal Server Error**: Returns an error message if there is a failure in fetching or processing the campaign data.

#### Example Response (200 OK)
```json
[
  {
    "campaign_id": "123456789",
    "campaign_name": "Campaign A",
    "ad_group_id": "987654321",
    "ad_group_name": "Ad Group 1",
    "impressions": 1000,
    "clicks": 50,
    "cost_micros": 500000,
    "ctr": 0.05,
    "cost_inr": 0.5,
    "cpc_inr": 0.01,
    "segment": 0,
    "performance": "Below Average",
    "recommendation": "Review ad copy and targeting to improve CTR"
  }
]
```

#### get_campaign_performance(client, customer_id, max_retries=3, retry_delay=5)

**Description**: Retrieves performance data for enabled Google Ads campaigns over the last 30 days.

##### Parameters
- `client`: An instance of the Google Ads API client.
- `customer_id`: The customer ID for the Google Ads account.
- `max_retries`: The maximum number of retry attempts in case of failures (default: 3).
- `retry_delay`: The delay (in seconds) between retry attempts (default: 5).

##### Returns
A list of dictionaries, each containing details of campaign performance metrics including impressions, clicks, and cost.

##### Raises
- **GoogleAdsException**: If the API call fails after maximum retries.
- **Exception**: If unable to fetch campaign performance data after all retries.

#### data_analysis(campaign_data)

**Description**: Analyzes campaign performance data to compute metrics, categorize performance, and provide recommendations.

##### Parameters
- `campaign_data`: A list of dictionaries containing raw campaign performance data.

##### Returns
A pandas DataFrame containing the analyzed campaign performance data, including metrics such as CTR, CPC, segmentation, performance categorization, and recommendations.

### Example Usage

1. **Send a POST request** to the `/ai-building-open-target/` endpoint without a body.
2. **Receive a response** containing the analyzed campaign performance data along with actionable insights.

### Dependencies
- **Django REST Framework**: Required for building the API.
- **Google Ads API**: Required for interacting with Google Ads data.
- **Pandas**: Used for data manipulation and analysis.
- **NumPy**: Used for numerical operations.
- **Scikit-learn**: Used for machine learning algorithms like KMeans.
- **Logging**: Used for error logging.


Here's the structured documentation for the `BudgetRecommendationView` class, following the same format as the previous documentation.

---

## **17. Budget Recommendation**

### Overview
The `BudgetRecommendationView` class is an API view designed to generate budget recommendations for Google Ads campaigns based on their performance metrics. It analyzes the current Return on Advertising Spend (ROAS) and suggests adjustments to the campaign budgets to optimize advertising effectiveness.

### POST /budget-recommendation/

**Description**: This method handles the incoming POST request to generate budget recommendations for active Google Ads campaigns based on the provided target ROAS and conversion value.

#### Request Body
- `target_roas` (optional, default: `2.0`): The target Return on Advertising Spend.
- `conversion_value_inr` (required): The monetary value of conversions in Indian Rupees.

#### Response
- **200 OK**: Returns a list of budget recommendations for each active campaign.
- **400 Bad Request**: Returns an error message if `conversion_value_inr` is missing or not a valid number.
- **500 Internal Server Error**: Returns an error message if there is a failure in the Google Ads API call.

#### Example Request
```json
{
  "target_roas": 2.5,
  "conversion_value_inr": 1000
}
```

#### Example Response (200 OK)
```json
[
  {
    "campaign_id": "1234567890",
    "campaign_name": "Campaign 1",
    "current_budget": "₹5000.00",
    "recommended_budget": "₹4500.00",
    "current_roas": "2.00",
    "recommendation": "Decrease budget from ₹5000.00 to ₹4500.00"
  },
  {
    "campaign_id": "0987654321",
    "campaign_name": "Campaign 2",
    "current_budget": "₹3000.00",
    "recommended_budget": "₹3300.00",
    "current_roas": "2.50",
    "recommendation": "Increase budget from ₹3000.00 to ₹3300.00"
  }
]
```

### Private Methods

#### initialize_client()

**Description**: Initializes the Google Ads client using the configuration stored in the specified YAML file.

##### Returns
- `GoogleAdsClient`: An instance of the Google Ads API client.

#### get_active_campaigns(client, customer_id)

**Description**: Retrieves a list of all active campaigns for the specified customer ID.

##### Parameters
- `client`: An instance of the Google Ads API client.
- `customer_id`: The customer ID for the Google Ads account.

##### Returns
- `response`: A list of active campaigns.

#### get_campaign_performance(client, customer_id, campaign_id, date_range)

**Description**: Retrieves performance metrics for a specific campaign over a specified date range.

##### Parameters
- `client`: An instance of the Google Ads API client.
- `customer_id`: The customer ID for the Google Ads account.
- `campaign_id`: The ID of the campaign to retrieve performance metrics for.
- `date_range`: A tuple containing the start and end dates for the performance data.

##### Returns
- `response`: The performance metrics for the specified campaign.

#### generate_budget_recommendations(client, customer_id, target_roas, conversion_value_inr)

**Description**: Generates budget recommendations for active campaigns based on their performance and the specified target ROAS.

##### Parameters
- `client`: An instance of the Google Ads API client.
- `customer_id`: The customer ID for the Google Ads account.
- `target_roas`: The target Return on Advertising Spend.
- `conversion_value_inr`: The monetary value of conversions in Indian Rupees.

##### Returns
- `recommendations`: A list of budget recommendations for each active campaign.

### Example Usage

1. **Send a POST request** to the `/budget-recommendation/` endpoint with the required body.
2. **Receive a response** containing budget recommendations for each active campaign.

### Dependencies
- **Django REST Framework**: Required for building the API.
- **Google Ads API**: Required for retrieving campaign data and performance metrics.
- **Datetime**: Used for handling date calculations.


Sure! Here's a comprehensive documentation for the `pauseLosingAdsToday` class in a similar style as the previous one you provided:

---

## **18.Pause Losing Ads Today**

The `pauseLosingAdsToday` class is an API view that analyzes ad groups from Google Ads data over the last 30 days and provides recommendations to pause ads that are underperforming based on return on investment (ROI) analysis.

### Methods

#### `get(self, request)`

Handles GET requests to analyze ad group performance and generate recommendations.

- **Parameters:**
  - `request`: The HTTP request object.

- **Returns:**
  - A JSON response containing recommendations for ad groups based on their performance metrics.
  - Status code `200 OK` on success.
  - Status code `400 Bad Request` if there is an error in processing the Google Ads data.

- **Process:**
  1. Initializes the Google Ads client using credentials from the YAML file.
  2. Fetches ad group performance data for the past 30 days.
  3. Calls `process_data()` to structure the response data.
  4. Calls `generate_recommendations()` to analyze the performance and generate recommendations based on ROI.

#### `process_data(self, response)`

Processes the Google Ads response to structure ad group data.

- **Parameters:**
  - `response`: The response object returned from the Google Ads API.

- **Returns:**
  - A dictionary containing structured ad group data including costs, revenues, ROIs, impressions, clicks, and conversions.

- **Process:**
  1. Iterates through the response data.
  2. Converts costs from micros to INR.
  3. Calculates ROI and compiles data for each ad group.

#### `generate_recommendations(self, ad_group_data)`

Generates recommendations based on processed ad group data.

- **Parameters:**
  - `ad_group_data`: A dictionary containing structured data for each ad group.

- **Returns:**
  - A list of recommendations for each ad group.

- **Process:**
  1. Iterates over each ad group.
  2. Calls `analyze_ad_group()` to analyze the ad group's performance.
  3. Generates a summary using `generate_summary()`.

#### `analyze_ad_group(self, data)`

Analyzes the performance of an individual ad group and generates a recommendation based on ROI and anomaly detection.

- **Parameters:**
  - `data`: A dictionary containing performance data for a single ad group.

- **Returns:**
  - A string with the recommendation based on the analysis.

- **Process:**
  1. Converts data into a DataFrame for time series analysis.
  2. Performs exponential smoothing for ROI forecasting.
  3. Detects anomalies using Isolation Forest.
  4. Generates a recommendation based on forecasted ROI and anomaly percentage.

#### `generate_summary(self, data)`

Generates a summary of performance metrics for a given ad group.

- **Parameters:**
  - `data`: A dictionary containing performance data for a single ad group.

- **Returns:**
  - A dictionary summarizing the ad group's total cost, revenue, impressions, clicks, conversions, average cost per click (CPC), average cost per acquisition (CPA), and return on ad spend (ROAS).

- **Process:**
  1. Sums up the costs, revenues, impressions, clicks, and conversions.
  2. Calculates average CPC and CPA.
  3. Computes ROAS.

### Exception Handling

If a `GoogleAdsException` occurs during the API call, the class captures the error message and returns a response with status code `400 Bad Request`, including details about the error.

Here’s a structured documentation for your `UnderPerformingAds` class, following a similar style as your previous documentation:

---

## **19. Under Performing Ads Class **

### Overview

The `UnderPerformingAds` class is an API view that retrieves and analyzes Google Ads data to identify underperforming ads based on cost-per-acquisition (CPA). It provides tailored recommendations for improving ad performance. This class utilizes the Google Ads API and employs machine learning techniques to generate insights.

## Endpoints

### GET /underperforming-ads

Retrieves a list of underperforming ads over a specified number of days.

#### Query Parameters

- **days** (optional): An integer representing the number of days to look back for ad performance data. Defaults to 30 if not provided.

#### Response

- **200 OK**: Returns a JSON object containing recommendations for underperforming ads.
- **400 Bad Request**: If the `days` parameter is invalid or not an integer.
- **500 Internal Server Error**: If an error occurs while processing the request, including Google Ads API errors.

### Methods

### `get(self, request)`

Handles GET requests to fetch underperforming ads.

#### Parameters

- **request**: The incoming HTTP request object.

#### Returns

- **Response**: A Response object containing either the recommendations for underperforming ads or an error message.

### `main(self, client, customer_id, days)`

The main method that orchestrates the data fetching, preprocessing, model training, and recommendation generation.

#### Parameters

- **client**: The Google Ads client instance.
- **customer_id**: The Google Ads customer ID.
- **days**: The number of days to retrieve data for.

#### Returns

- **dict**: A dictionary containing recommendations and (optionally) visualizations.

### `get_google_ads_data(self, client, customer_id, days)`

Fetches Google Ads data for the specified customer ID and date range.

#### Parameters

- **client**: The Google Ads client instance.
- **customer_id**: The Google Ads customer ID.
- **days**: The number of days to retrieve data for.

#### Returns

- **List[Dict[str, Any]]**: A list of dictionaries containing ad performance metrics.

### `preprocess_data(self, data)`

Preprocesses the raw Google Ads data into a Pandas DataFrame and computes additional metrics.

#### Parameters

- **data**: A list of dictionaries containing raw Google Ads data.

#### Returns

- **pd.DataFrame**: A DataFrame containing preprocessed ad performance data.

### `train_model(self, df)`

Trains a Random Forest model to predict CPA based on historical ad performance data.

#### Parameters

- **df**: A DataFrame containing preprocessed ad performance data.

#### Returns

- **GridSearchCV**: The trained GridSearchCV object containing the best model and hyperparameters.

### `get_tailored_recommendation(self, ad)`

Generates tailored recommendations for a specific ad based on its performance metrics.

#### Parameters

- **ad**: A Pandas Series containing ad performance metrics.

#### Returns

- **str**: A string containing recommendations for improving ad performance.

### `generate_recommendations(self, df, model, threshold_multiplier=1.2)`

Generates recommendations for underperforming ads based on predicted CPA.

#### Parameters

- **df**: A DataFrame containing preprocessed ad performance data.
- **model**: The trained Random Forest model.
- **threshold_multiplier**: A multiplier for determining the threshold of underperformance.

#### Returns

- **List[Dict[str, Any]]**: A list of dictionaries containing recommendations for underperforming ads.

### `handle_google_ads_exception(self, ex)`

Handles exceptions raised by the Google Ads API and formats the error message for easier understanding.

#### Parameters

- **ex**: The GoogleAdsException object.

#### Returns

- **str**: A formatted error message describing the exception.

### `format_inr(self, amount)`

Formats a given amount as Indian Rupees.

#### Parameters

- **amount**: A float representing the amount to be formatted.

#### Returns

- **str**: A string formatted in Indian Rupees.

### Logging

The class uses the `logger` to record significant events and errors throughout its methods, aiding in debugging and monitoring.

### Dependencies

- **Google Ads API**: For fetching ad performance data.
- **Pandas**: For data manipulation and preprocessing.
- **Scikit-learn**: For machine learning model training and evaluation.
- **NumPy**: For numerical operations.

## **20. Scale Your Winners**
### Overview

The `Scale Your Winners` class is designed to interact with the Google Ads API to fetch active campaign data, process the data for machine learning analysis, and generate recommendations for enhancing campaign performance. This is achieved through the use of various machine learning techniques, including regression and clustering.

**Parameters:**

- `*args`: Variable length argument list.
- `**kwargs`: Arbitrary keyword arguments.

### Methods

### `get_campaigns(self)`

Fetches active Google Ads campaigns from the account.

**Returns:**

- `active_campaigns` (List[Dict]): A list of dictionaries containing details of active campaigns, including ID, name, budget, impressions, clicks, conversions, and enhanced CPC status.

**Exceptions:**

- Raises `GoogleAdsException` if the API request fails.

### `preprocess_data(self, campaigns)`

Prepares the fetched campaign data for machine learning analysis.

**Parameters:**

- `campaigns` (List[Dict]): A list of campaign data fetched from the Google Ads API.

**Returns:**

- `df` (DataFrame): A Pandas DataFrame containing processed campaign data.
- `numeric_columns` (List[str]): A list of numeric feature column names.
- `categorical_columns` (List[str]): A list of categorical feature column names.

### `train_models(self, df, numeric_columns)`

Trains machine learning models on the processed campaign data.

**Parameters:**

- `df` (DataFrame): The processed campaign DataFrame.
- `numeric_columns` (List[str]): A list of numeric feature column names.

**Returns:**

- `rf_model`: Trained Random Forest model.
- `gb_model`: Trained Gradient Boosting model.
- `scaler`: Scikit-learn StandardScaler used for feature scaling.
- `features` (List[str]): A list of feature names used for training.

### `get_feature_importance(self, model, features)`

Retrieves the feature importance scores from a trained model.

**Parameters:**

- `model`: A trained machine learning model (Random Forest or Gradient Boosting).
- `features` (List[str]): A list of feature names.

**Returns:**

- `feature_importance` (List[Tuple[str, float]]): A list of tuples containing feature names and their corresponding importance scores.

### `cluster_campaigns(self, df, numeric_columns)`

Clusters the campaigns based on relevant features using KMeans clustering.

**Parameters:**

- `df` (DataFrame): The processed campaign DataFrame.
- `numeric_columns` (List[str]): A list of numeric feature column names.

**Returns:**

- `df` (DataFrame): The updated DataFrame with cluster assignments.
- `kmeans`: The KMeans model used for clustering.

### `generate_recommendations(self, campaigns)`

Generates performance improvement recommendations for the fetched campaigns.

**Parameters:**

- `campaigns` (List[Dict]): A list of campaign data fetched from the Google Ads API.

**Returns:**

- `recommendations` (List[Dict]): A list of recommendations, each containing details such as campaign ID, name, current budget, predicted conversions, cluster, top features, and suggestions for improvement.

### `post(self, request)`

Handles the POST request to fetch campaigns and generate recommendations.

**Parameters:**

- `request`: The incoming HTTP request.

**Returns:**

- `Response`: A JSON response containing either the recommendations or an error message.

**Exceptions:**

- Handles `GoogleAdsException` and general exceptions, returning appropriate error messages.

### Logging

- The class logs various actions and errors using a logger to facilitate troubleshooting and monitoring.


Here’s a comprehensive documentation outline for your `MLEnhancedCampaignRecommender` and `PerformanceAnalysisView` classes, which can be added as comments in the code or as a separate markdown file.

---

## **21.Low Performing Resource Reallocation**

### Overview

This module provides functionalities to analyze the performance of Google Ads campaigns and generate recommendations based on specified performance metrics for machine learning-based recommendations and `Low Performing Resource Reallocation` for analyzing ad spend performance.
#### Methods

- **`__init__(self, *args, **kwargs)`**
  - Initializes the recommender with Google Ads client settings.
  - **Parameters:**
    - `*args`: Variable length argument list.
    - `**kwargs`: Arbitrary keyword arguments.

- **`get_campaigns(self)`**
  - Fetches all active Google Ads campaigns.
  - **Returns:** 
    - A list of active campaigns with details like ID, name, budget, impressions, clicks, and conversions.

- **`preprocess_data(self, campaigns)`**
  - Prepares the campaign data for machine learning by performing feature engineering and data cleaning.
  - **Parameters:**
    - `campaigns`: List of campaign data dictionaries.
  - **Returns:**
    - A DataFrame of processed data, list of numeric columns, and list of categorical columns.

- **`train_models(self, df, numeric_columns)`**
  - Trains machine learning models (Random Forest and Gradient Boosting) on the campaign data.
  - **Parameters:**
    - `df`: DataFrame containing the campaign data.
    - `numeric_columns`: List of numeric feature names.
  - **Returns:**
    - The trained Random Forest and Gradient Boosting models, the scaler, and the features used for training.

- **`get_feature_importance(self, model, features)`**
  - Retrieves the feature importance from the trained model.
  - **Parameters:**
    - `model`: The trained model.
    - `features`: List of feature names.
  - **Returns:**
    - A sorted list of features and their importance scores.

- **`cluster_campaigns(self, df, numeric_columns)`**
  - Clusters campaigns based on selected numeric features using KMeans clustering.
  - **Parameters:**
    - `df`: DataFrame of campaign data.
    - `numeric_columns`: List of numeric feature names.
  - **Returns:**
    - The DataFrame with cluster labels and the KMeans model.

- **`generate_recommendations(self, campaigns)`**
  - Generates recommendations based on the campaign data and trained models.
  - **Parameters:**
    - `campaigns`: List of campaign data dictionaries.
  - **Returns:**
    - A list of recommendations for each campaign.

- **`post(self, request)`**
  - Handles POST requests to analyze campaigns and generate recommendations.
  - **Parameters:**
    - `request`: The HTTP request object.
  - **Returns:**
    - A Response containing recommendations or error messages.

### PerformanceAnalysisView

This class provides an API endpoint to analyze the performance of Google Ads campaigns based on a user-defined performance threshold.

#### Methods

- **`post(self, request)`**
  - Handles POST requests for performance analysis of Google Ads campaigns.
  - **Parameters:**
    - `request`: The HTTP request object containing the `performance_threshold`.
  - **Returns:**
    - A Response containing recommendations or error messages.

---

### Usage

1. **Fetch Active Campaigns**: The `get_campaigns` method retrieves all currently active Google Ads campaigns.
2. **Analyze Performance**: The `get_campaign_performance` method retrieves the performance data (clicks, impressions, CTR, and ad spend) for a specified campaign.
3. **Generate Recommendations**: The `generate_ad_spend_recommendation` method generates recommendations based on the campaign's CTR compared to the performance threshold.
4. **Run Performance Analysis**: The `run_performance_analysis` method integrates the previous methods to fetch active campaigns, analyze their performance, and return recommendations.
5. **API Integration**: The `PerformanceAnalysisView` class exposes the functionality through a RESTful API, allowing users to submit a performance threshold and receive recommendations.

### Error Handling

- The system handles `GoogleAdsException` for errors related to the Google Ads API, and it will print the error message to the console.
- The API response includes appropriate status codes (e.g., `400 Bad Request` for invalid input) to inform the user about any issues.

### Example Request

### POST /low-performing-resource-reallocation/

**Request Body:**
```json
{
    "performance_threshold": 0.05
}
```

**Response:**
```json
{
    "recommendations": [
        {
            "campaign_id": "123456",
            "campaign_name": "Spring Sale",
            "current_ad_spend": 5000,
            "recommended_ad_spend": 4500,
            "reason": "CTR (4.50%) is below threshold (5.00%)"
        }
    ]
}
```


Here's a detailed documentation outline for your `AdGroupRecommendationsView` class. This documentation can be included as comments in the code or as a separate markdown file.

---

## **22. Kill Losing Ad Groups**

## Overview

The `Kill Losing Ad Groups` class provides an API endpoint for generating recommendations for ad groups based on their performance metrics in Google Ads. It utilizes two helper classes, `AdGroupProfiler` and `AdGroupRecommender`, to analyze ad group performance and generate actionable insights.

## Class: AdGroupRecommendationsView

### Inheritance
- Inherits from `APIView`, which is part of the Django REST framework.

### Attributes
- **`parser_classes`**: Specifies the parser for incoming requests. Here, it uses `JSONParser` to handle JSON data.

### Methods

#### `post(self, request)`

Handles POST requests to generate ad group recommendations based on the specified time frame and ROI threshold.

**Parameters:**
- `request`: The HTTP request object containing the following data in JSON format:
  - `days` (optional): An integer indicating the number of days for performance analysis (default is 30).
  - `roi_threshold` (optional): A float representing the return on investment (ROI) threshold for recommendations (default is 0).

**Returns:**
- On success:
  - `Response`: A JSON response containing the list of recommendations generated.
  
- On error:
  - `Response`: A JSON response with an error message and corresponding HTTP status code.

**Error Handling:**
- **Invalid Input**: If `days` or `roi_threshold` cannot be converted to the appropriate type, it returns a `400 Bad Request` with an error message.
- **Google Ads Client Error**: If the Google Ads client fails to load, it logs the error and returns a `500 Internal Server Error` with a corresponding message.
- **Google Ads API Error**: If there are errors during performance retrieval or recommendation generation, it captures detailed error messages from the Google Ads API and returns a `400 Bad Request`.
- **General Error**: Any other exceptions encountered during processing are logged and result in a `500 Internal Server Error`.

### Usage

1. **Send a POST Request**: The client sends a POST request to the endpoint associated with this view, providing the desired `days` and `roi_threshold` values.
2. **Process Request**: The view processes the request:
   - Validates and converts the input parameters.
   - Loads the Google Ads client.
   - Retrieves performance data for active ad groups using the `AdGroupProfiler` class.
   - Calculates profitability metrics.
   - Generates recommendations using the `AdGroupRecommender` class.
3. **Response**: The server responds with either a list of recommendations or an error message.

### Example Request

#### POST /Kill_Losing_Ad_Groups/

**Request Body:**
```json
{
    "days": 30,
    "roi_threshold": 1.5
}
```

**Successful Response:**
```json
[
    {
        "ad_group_id": "1234567890",
        "ad_group_name": "Ad Group 1",
        "recommended_action": "Increase budget by 20%",
        "expected_roi": 2.0
    },
    {
        "ad_group_id": "0987654321",
        "ad_group_name": "Ad Group 2",
        "recommended_action": "Reduce budget by 15%",
        "expected_roi": 0.8
    }
]
```

**Error Response Example:**
```json
{
    "error": "Invalid days or roi_threshold parameter"
}
```

---

### Logging

The view uses logging to capture important events and errors:
- Logs the number of generated recommendations for audit purposes.
- Logs errors encountered during processing, including specific Google Ads API errors and general exceptions.


Here's a detailed documentation outline for your `AdsAnalysisView` class. This documentation can be included as comments in the code or as a separate markdown file.

---

## **23. Mark High Ctr**
### Overview

The `mark-high-ctr` class provides an API endpoint for analyzing ad performance data from Google Ads and generating recommendations based on the analysis. It utilizes clustering and anomaly detection techniques to identify high-performing ads.

### Class: AdsAnalysisView

### Inheritance
- Inherits from `APIView`, which is part of the Django REST framework.

### Methods

#### `get_ad_performance_data(self, client, customer_id: str) -> List[Dict]`

Retrieves ad performance data from Google Ads.

**Parameters:**
- `client`: An instance of the Google Ads client used to make API calls.
- `customer_id` (str): The Google Ads customer ID for which to retrieve ad performance data.

**Returns:**
- `List[Dict]`: A list of dictionaries containing ad performance metrics.

**Error Handling:**
- Logs an error message and returns an empty list if an exception occurs.

#### `preprocess_data(self, ads_data: List[Dict]) -> np.ndarray`

Preprocesses the retrieved ad data for further analysis.

**Parameters:**
- `ads_data`: A list of dictionaries containing ad performance metrics.

**Returns:**
- `np.ndarray`: A scaled array of features (CTR, clicks, impressions, cost) suitable for clustering.

#### `identify_high_performing_ads(self, X_scaled: np.ndarray, ads_data: List[Dict]) -> List[Dict]`

Identifies high-performing ads using clustering and anomaly detection techniques.

**Parameters:**
- `X_scaled`: A scaled array of features to analyze.
- `ads_data`: A list of dictionaries containing ad performance metrics.

**Returns:**
- `List[Dict]`: A list of dictionaries containing high-performing ads along with the reason for their classification.

#### `generate_recommendations(self, high_performing_ads: List[Dict]) -> List[Dict]`

Generates performance-based recommendations for the identified high-performing ads.

**Parameters:**
- `high_performing_ads`: A list of dictionaries containing high-performing ad data.

**Returns:**
- `List[Dict]`: A list of recommendations for improving ad performance.

#### `get(self, request)`

Handles GET requests to analyze ad performance and generate recommendations.

**Parameters:**
- `request`: The HTTP request object.

**Returns:**
- On success:
  - `Response`: A JSON response containing a list of recommendations.
  
- On error:
  - `Response`: A JSON response with an error message and corresponding HTTP status code.

**Error Handling:**
- If no ad data is retrieved, it returns a `404 Not Found` response.
- Catches general exceptions and returns a `500 Internal Server Error` response with the error message.

### Usage

1. **Send a GET Request**: The client sends a GET request to the endpoint associated with this view.
2. **Process Request**: The view processes the request:
   - Loads the Google Ads client.
   - Retrieves ad performance data using the `get_ad_performance_data` method.
   - Preprocesses the data using the `preprocess_data` method.
   - Identifies high-performing ads using the `identify_high_performing_ads` method.
   - Generates recommendations using the `generate_recommendations` method.
3. **Response**: The server responds with either a list of recommendations or an error message.

### Example Request

#### GET /mark-high-ctr/

**Successful Response:**
```json
{
    "recommendations": [
        {
            "ad_id": "1234567890",
            "ad_name": "Ad 1",
            "ad_group": "Ad Group 1",
            "campaign": "Campaign 1",
            "performance": "Best Cluster",
            "recommendations": [
                "Consider increasing budget for this high-CTR ad"
            ]
        },
        {
            "ad_id": "0987654321",
            "ad_name": "Ad 2",
            "ad_group": "Ad Group 2",
            "campaign": "Campaign 2",
            "performance": "Anomaly",
            "recommendations": [
                "Optimize ad copy to increase clicks",
                "Monitor and optimize bidding strategy to control costs"
            ]
        }
    ]
}
```

**Error Response Example:**
```json
{
    "error": "No ad data retrieved. Please check your account and try again."
}
```

### Logging

The view logs important events and errors during processing:
- Logs errors encountered while retrieving ad performance data.
- Returns clear error messages in the response for troubleshooting.


## 24.Revive Ad-Group Recommendations

### Overview
The `revive-ad-grouprecommendations` is a Django REST Framework API view that generates advertising recommendations based on Google Ads performance metrics. This view utilizes the Google Ads API to retrieve ad performance data and provide actionable insights to improve ad campaign effectiveness.

### Endpoint
- **POST** `/api/revive-ad-grouprecommendations/`

### Request
- **Method:** `POST`
- **Headers:** 
  - `Content-Type: application/json`
- **Body:** No specific body parameters are required. The request can be empty.

### Response
- **Success Response:**
  - **Status Code:** `200 OK`
  - **Body:** 
    ```json
    [
      {
        "campaign_id": "123456",
        "campaign_name": "Campaign Name",
        "ad_group_id": "789012",
        "ad_group_name": "Ad Group Name",
        "clicks": 5,
        "impressions": 2000,
        "ctr": 0.0025,
        "cpa": 150.00,
        "recommendation": "Low clicks with high impressions",
        "action": "Consider increasing bids by 20% to improve visibility",
        "score": 10
      },
      
    ]
    ```
  - **Description:** Returns a list of the top advertising recommendations, sorted by their score.

- **Error Response:**
  - **Status Code:** `500 Internal Server Error`
  - **Body:** 
    ```json
    {
      "error": "Error message detailing what went wrong"
    }
    ```
  - **Description:** Returns an error message if there is an issue with generating recommendations or fetching data.

### Methods

#### 1. `post(request)`
- **Description:** Handles POST requests to generate and return advertising recommendations.
- **Parameters:**
  - `request`: The HTTP request object containing user input or parameters (not utilized in this method).
- **Returns:** A JSON response containing the top advertising recommendations or an error message.

#### 2. `get_google_ads_client()`
- **Description:** Initializes and returns a Google Ads client based on configuration settings.
- **Returns:** An instance of `GoogleAdsClient` configured with the settings defined in the project.

#### 3. `generate_recommendations(client, customer_id)`
- **Description:** Fetches ad performance data and generates recommendations based on specified criteria.
- **Parameters:**
  - `client`: An instance of `GoogleAdsClient`.
  - `customer_id`: The Google Ads customer ID for which recommendations are generated.
- **Returns:** A list of recommendations based on ad performance metrics.

#### 4. `process_row(row)`
- **Description:** Processes a single row of ad performance data and generates a recommendation if applicable.
- **Parameters:**
  - `row`: A row object containing metrics from the Google Ads API.
- **Returns:** A structured recommendation dictionary if criteria are met, otherwise `None`.

#### 5. `create_recommendation(campaign, ad_group, clicks, impressions, ctr, cpa, recommendation, action, score)`
- **Description:** Creates a structured recommendation dictionary based on ad performance metrics.
- **Parameters:**
  - `campaign`: The campaign object associated with the ad.
  - `ad_group`: The ad group object associated with the ad.
  - `clicks`: Number of clicks received by the ad.
  - `impressions`: Number of impressions received by the ad.
  - `ctr`: Click-through rate of the ad.
  - `cpa`: Cost per acquisition for the ad.
  - `recommendation`: The recommendation text generated.
  - `action`: Suggested action to improve ad performance.
  - `score`: The score assigned to the recommendation based on performance metrics.
- **Returns:** A dictionary containing the structured recommendation details.

#### 6. `get_top_recommendations(recommendations, n=20)`
- **Description:** Sorts recommendations by score and returns the top N recommendations.
- **Parameters:**
  - `recommendations`: A list of recommendation dictionaries.
  - `n`: The number of top recommendations to return (default is 20).
- **Returns:** A list of the top N recommendations sorted by score.

### Usage
- The endpoint is used by clients (e.g., front-end applications or other services) to retrieve recommendations for optimizing Google Ads campaigns. No input parameters are required in the request body, making it straightforward to integrate.

### Exception Handling
- The view handles exceptions related to Google Ads API requests and returns a meaningful error message with a `500 Internal Server Error` status code if any error occurs.

Below is the structured documentation for the `ReviveAdRecommendationView` class. This includes details about the class methods, inputs, outputs, and functionality, formatted for use as a comprehensive guide or API documentation.

---

## **25. Revive-Ad-Recommendations**

### Overview
The `revive-ad-recommendations` is a Django REST Framework API view designed to generate recommendations for Google Ads campaigns based on performance data. It retrieves relevant ad metrics from the Google Ads API and generates insights and actionable steps to improve ad effectiveness.

### Endpoint
- **POST** `/api/revive-ad-recommendations/`

### Request
- **Method:** `POST`
- **Headers:** 
  - `Content-Type: application/json`
- **Body:** No request body is required.

### Response
- **Success Response:**
  - **Status Code:** `200 OK`
  - **Body:** 
    ```json
    [
      {
        "campaign_id": "123456",
        "campaign_name": "Campaign Name",
        "ad_group_id": "789012",
        "ad_group_name": "Ad Group Name",
        "ad_id": "345678",
        "ad_name": "Ad Name",
        "ad_status": "ENABLED",
        "clicks": 5,
        "impressions": 2000,
        "ctr": 0.0025,
        "cpa": 150.00,
        "recommendation": "Low clicks with high impressions",
        "action": "Review ad copy and consider increasing bids",
        "score": 10
      },
      
    ]
    ```
  - **Description:** Returns a list of top advertising recommendations, sorted by their score.

- **Error Response:**
  - **Status Code:** `500 Internal Server Error`
  - **Body:** 
    ```json
    {
      "error": "Error message explaining what went wrong"
    }
    ```
  - **Description:** Returns an error message if there is an issue with generating recommendations or interacting with the Google Ads API.

### Class Methods

#### `post(request)`
- **Description:** Handles `POST` requests to generate and return Google Ads recommendations.
- **Parameters:**
  - `request`: The HTTP request object. No specific request body is required.
- **Returns:** A JSON response containing the top recommendations or an error message.
- **Error Handling:** Catches `GoogleAdsException` and returns a `500 Internal Server Error` with a message.

#### `get_google_ads_client()`
- **Description:** Initializes and returns a `GoogleAdsClient` instance using the Google Ads configuration defined in a YAML file.
- **Implementation:**
  - Reads the Google Ads configuration from the YAML file specified in `settings.GOOGLE_ADS_YAML_PATH`.
  - Loads the client using the `GoogleAdsClient.load_from_dict()` method.
- **Returns:** A configured instance of `GoogleAdsClient`.

#### `generate_ad_recommendations(client, customer_id)`
- **Description:** Retrieves ad performance data for a given customer from the Google Ads API and generates recommendations based on specified criteria.
- **Parameters:**
  - `client`: An instance of `GoogleAdsClient` for making API requests.
  - `customer_id`: The customer ID of the Google Ads account.
- **Returns:** A list of recommendations based on ad performance data.
- **Error Handling:** If an error occurs while querying the API, a `GoogleAdsException` is raised and handled by the `post` method.

#### `process_ad_row(row)`
- **Description:** Processes a single row of Google Ads performance data and generates a recommendation if applicable.
- **Parameters:**
  - `row`: A row object containing campaign, ad group, ad, and performance metrics.
- **Returns:** A structured recommendation dictionary if conditions are met, otherwise returns `None`.
- **Logic:**
  - Evaluates various performance metrics such as clicks, impressions, CTR (click-through rate), CPA (cost per acquisition), and ad status.
  - Generates recommendations based on the following conditions:
    - **Paused Ads:** If the ad is paused, suggests reactivation and assigns a high priority score.
    - **Low Clicks/High Impressions:** If the clicks are below a threshold and impressions are high, recommends reviewing the ad copy or adjusting bids.
    - **Low CTR:** If the CTR is below 1%, suggests improving ad relevance and adjusting targeting.
    - **High CPA:** If CPA is high (greater than 100), recommends optimizing for conversions.
- **Returns:** A structured dictionary containing the recommendation and related performance metrics.

#### `create_ad_recommendation(campaign, ad_group, ad, clicks, impressions, ctr, cpa, status, recommendation, action, score)`
- **Description:** Creates and structures a recommendation dictionary using the provided ad performance data and analysis.
- **Parameters:**
  - `campaign`: The campaign object associated with the ad.
  - `ad_group`: The ad group object associated with the ad.
  - `ad`: The ad object.
  - `clicks`: Number of clicks received by the ad.
  - `impressions`: Number of impressions received by the ad.
  - `ctr`: Click-through rate of the ad.
  - `cpa`: Cost per acquisition for the ad.
  - `status`: The status of the ad.
  - `recommendation`: The recommendation message generated for the ad.
  - `action`: Suggested action to improve ad performance.
  - `score`: The score assigned to the recommendation based on performance metrics.
- **Returns:** A dictionary containing the structured recommendation details.

#### `get_top_recommendations(recommendations, n=20)`
- **Description:** Sorts the list of recommendations by their score and returns the top `n` recommendations.
- **Parameters:**
  - `recommendations`: A list of recommendation dictionaries generated from `process_ad_row()`.
  - `n`: Number of top recommendations to return. Default is 20.
- **Returns:** A list of the top `n` recommendations, sorted in descending order by score.

### Example Usage
1. **Request:**
   - **POST** `/api/ad-recommendations/`
   - No body is required.
   
2. **Response:**
   ```json
   [
     {
       "campaign_id": "123456",
       "campaign_name": "Campaign Name",
       "ad_group_id": "789012",
       "ad_group_name": "Ad Group Name",
       "ad_id": "345678",
       "ad_name": "Ad Name",
       "ad_status": "ENABLED",
       "clicks": 5,
       "impressions": 2000,
       "ctr": 0.0025,
       "cpa": 150.00,
       "recommendation": "Low clicks with high impressions",
       "action": "Review ad copy and consider increasing bids",
       "score": 10
     }
   ]
   ```

### Error Handling
- The view catches `GoogleAdsException` errors and returns a `500 Internal Server Error` with an error message detailing the issue.
