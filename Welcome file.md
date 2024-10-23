<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Welcome file</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__left">
    <div class="stackedit__toc">
      
<ul>
<li><a href="#athena-phase-1---end-user-guide">Athena Phase 1 - End User Guide</a>
<ul>
<li></li>
<li><a href="#winning_campaign-api">2.Winning_campaign API</a></li>
<li><a href="#overview-1">Overview</a></li>
<li><a href="#features-1">Features</a></li>
<li><a href="#key-metrics-to-understand">Key Metrics to Understand</a></li>
<li><a href="#how-it-works">How It Works</a></li>
<li><a href="#user-interface--recommendations">User Interface & Recommendations</a></li>
<li><a href="#invalid-click-analysis">Invalid Click Analysis</a></li>
<li><a href="#overspending-ads">2.Overspending Ads</a></li>
<li><a href="#methods-2">Methods</a></li>
<li><a href="#adset-performance-analysis">8. AdSet Performance Analysis</a></li>
<li><a href="#constants">Constants</a></li>
<li><a href="#methods-3">Methods</a></li>
<li><a href="#funnelanalysis-class">11.FunnelAnalysis Class</a>
<ul>
<li></li>
<li><a href="#error-handling-6">Error Handling</a></li>
</ul>
</li>
<li><a href="#ad-copyinsights">12. Ad CopyInsights</a></li>
<li><a href="#overview-4">Overview</a></li>
<li><a href="#inheritance">Inheritance</a></li>
<li><a href="#methods-7">Methods</a></li>
<li><a href="#overspending-ads-1">13. Overspending Ads</a></li>
<li><a href="#stoplossautomation">14. StopLossAutomation</a></li>
<li><a href="#example-usage">Example Usage</a></li>
<li><a href="#ai-buidding-opentarget">15. AI Buidding OpenTarget</a></li>
<li><a href="#overview-5">Overview</a></li>
<li><a href="#methods-9">Methods</a></li>
<li><a href="#dependencies">Dependencies</a></li>
</ul>
</li>
<li><a href="#budget-recommendation">17. Budget Recommendation</a>
<ul>
<li><a href="#overview-6">Overview</a></li>
<li><a href="#dependencies-1">Dependencies</a></li>
<li><a href="#pause-losing-ads-today">17.Pause Losing Ads Today</a></li>
<li><a href="#under-performing-ads-class-">**18. Under Performing Ads Class **</a></li>
<li><a href="#overview-7">Overview</a></li>
<li><a href="#endpoints">Endpoints</a></li>
<li><a href="#methods-11">Methods</a></li>
<li><a href="#logging-2">Logging</a></li>
<li><a href="#dependencies-2">Dependencies</a></li>
<li><a href="#scale-your-winners">Scale Your Winners</a></li>
<li><a href="#methods-12">Methods</a></li>
<li><a href="#logging-3">Logging</a></li>
<li><a href="#low-performing-resource-reallocation">Low Performing Resource Reallocation</a></li>
<li><a href="#overview-9">Overview</a>
<ul>
<li></li>
<li><a href="#performanceanalysisview">PerformanceAnalysisView</a></li>
</ul>
</li>
<li><a href="#usage">Usage</a></li>
<li><a href="#error-handling-8">Error Handling</a></li>
<li><a href="#example-request-4">Example Request</a></li>
<li><a href="#kill-losing-ad-groups">19. Kill Losing Ad Groups</a></li>
<li><a href="#overview-10">Overview</a></li>
<li><a href="#class-adgrouprecommendationsview">Class: AdGroupRecommendationsView</a></li>
<li><a href="#logging-4">Logging</a></li>
<li><a href="#mark-high-ctr">Mark High Ctr</a></li>
<li><a href="#overview-11">Overview</a></li>
<li><a href="#class-adsanalysisview">Class: AdsAnalysisView</a></li>
<li><a href="#logging-5">Logging</a></li>
<li><a href="#revive-ad-group-recommendations">21.Revive Ad-Group Recommendations</a></li>
<li><a href="#revive-ad-recommendations">Revive-Ad-Recommendations</a></li>
</ul>
</li>
</ul>

    </div>
  </div>
  <div class="stackedit__right">
    <div class="stackedit__html">
      <h1 id="athena-phase-1---end-user-guide"><strong>Athena Phase 1 - End User Guide</strong></h1>
<h3 id="dashboardview-api"><strong>1.DashboardView API</strong></h3>
<h3 id="overview"><strong>Overview</strong></h3>
<p>The <code>DashboardView</code> class provides astrikethrough textn API endpoint for fetching detailed Google Ads performance metrics. Users can retrieve metrics such as impressions, clicks, cost, conversions, top-performing ads, and destination URLs for a specified date range. This data is aggregated and returned in an easy-to-interpret format for building dashboards or tracking campaign performance.</p>
<h3 id="features"><strong>Features</strong></h3>
<ul>
<li>Retrieves and calculates overall Google Ads metrics for the specified date range.</li>
<li>Provides daily metrics to analyze performance trends.</li>
<li>Retrieves top 10 performing ads based on impressions.</li>
<li>Retrieves top 10 destination URLs based on click-through performance.</li>
</ul>
<hr>
<h3 id="api-endpoint"><strong>API Endpoint</strong></h3>
<p><strong>POST</strong> <code>/api/dashboard/</code></p>
<h4 id="request-body"><strong>Request Body</strong></h4>
<p>To get the metrics, you need to provide a date range in the request body.</p>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
  <span class="token string">"start_date"</span><span class="token punctuation">:</span> <span class="token string">"YYYY-MM-DD"</span><span class="token punctuation">,</span>
  <span class="token string">"end_date"</span><span class="token punctuation">:</span> <span class="token string">"YYYY-MM-DD"</span>
<span class="token punctuation">}</span>
</code></pre>
<ul>
<li><strong><code>start_date</code></strong>: The beginning of the date range in “YYYY-MM-DD” format.</li>
<li><strong><code>end_date</code></strong>: The end of the date range in “YYYY-MM-DD” format.</li>
</ul>
<h4 id="response-example"><strong>Response Example</strong></h4>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
  <span class="token string">"period"</span><span class="token punctuation">:</span> <span class="token string">"2024-01-01 to 2024-01-07"</span><span class="token punctuation">,</span>
  <span class="token string">"overall_metrics"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
    <span class="token string">"impressions"</span><span class="token punctuation">:</span> <span class="token number">12345</span><span class="token punctuation">,</span>
    <span class="token string">"clicks"</span><span class="token punctuation">:</span> <span class="token number">6789</span><span class="token punctuation">,</span>
    <span class="token string">"cost"</span><span class="token punctuation">:</span> <span class="token number">5000</span><span class="token punctuation">,</span>
    <span class="token string">"conversions"</span><span class="token punctuation">:</span> <span class="token number">123</span><span class="token punctuation">,</span>
    <span class="token string">"ctr"</span><span class="token punctuation">:</span> <span class="token number">5.67</span><span class="token punctuation">,</span>
    <span class="token string">"cpc"</span><span class="token punctuation">:</span> <span class="token number">2.34</span><span class="token punctuation">,</span>
    <span class="token string">"conversion_rate"</span><span class="token punctuation">:</span> <span class="token number">2.1</span><span class="token punctuation">,</span>
    <span class="token string">"roas"</span><span class="token punctuation">:</span> <span class="token number">3.5</span>
  <span class="token punctuation">}</span><span class="token punctuation">,</span>
  <span class="token string">"daily_metrics"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
    <span class="token punctuation">{</span>
      <span class="token string">"date"</span><span class="token punctuation">:</span> <span class="token string">"2024-01-01"</span><span class="token punctuation">,</span>
      <span class="token string">"spend"</span><span class="token punctuation">:</span> <span class="token number">500</span><span class="token punctuation">,</span>
      <span class="token string">"clicks"</span><span class="token punctuation">:</span> <span class="token number">100</span><span class="token punctuation">,</span>
      <span class="token string">"conversions"</span><span class="token punctuation">:</span> <span class="token number">5</span><span class="token punctuation">,</span>
      <span class="token string">"impressions"</span><span class="token punctuation">:</span> <span class="token number">2000</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    <span class="token operator">...</span>
  <span class="token punctuation">]</span><span class="token punctuation">,</span>
  <span class="token string">"top_ads"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
    <span class="token punctuation">{</span>
      <span class="token string">"campaign_id"</span><span class="token punctuation">:</span> <span class="token string">"123"</span><span class="token punctuation">,</span>
      <span class="token string">"campaign_name"</span><span class="token punctuation">:</span> <span class="token string">"Holiday Sale"</span><span class="token punctuation">,</span>
      <span class="token string">"impressions"</span><span class="token punctuation">:</span> <span class="token number">5000</span><span class="token punctuation">,</span>
      <span class="token string">"clicks"</span><span class="token punctuation">:</span> <span class="token number">300</span><span class="token punctuation">,</span>
      <span class="token string">"cost"</span><span class="token punctuation">:</span> <span class="token number">1500</span><span class="token punctuation">,</span>
      <span class="token string">"conversions"</span><span class="token punctuation">:</span> <span class="token number">10</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    <span class="token operator">...</span>
  <span class="token punctuation">]</span><span class="token punctuation">,</span>
  <span class="token string">"top_destination_urls"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
    <span class="token punctuation">{</span>
      <span class="token string">"campaign_name"</span><span class="token punctuation">:</span> <span class="token string">"Holiday Sale"</span><span class="token punctuation">,</span>
      <span class="token string">"final_urls"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token string">"http://example.com/holiday-sale"</span><span class="token punctuation">]</span><span class="token punctuation">,</span>
      <span class="token string">"impressions"</span><span class="token punctuation">:</span> <span class="token number">1000</span><span class="token punctuation">,</span>
      <span class="token string">"clicks"</span><span class="token punctuation">:</span> <span class="token number">500</span><span class="token punctuation">,</span>
      <span class="token string">"conversions"</span><span class="token punctuation">:</span> <span class="token number">5</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    <span class="token operator">...</span>
  <span class="token punctuation">]</span>
<span class="token punctuation">}</span>
</code></pre>
<hr>
<h3 id="error-responses"><strong>Error Responses</strong></h3>
<ul>
<li>
<p><strong>400 BAD REQUEST</strong>: Invalid input or missing required parameters.</p>
<ul>
<li>Example: If <code>start_date</code> or <code>end_date</code> is missing or incorrectly formatted.</li>
<li>Example Response:<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
  <span class="token string">"error"</span><span class="token punctuation">:</span> <span class="token string">"Invalid date format. Use YYYY-MM-DD."</span>
<span class="token punctuation">}</span>
</code></pre>
</li>
</ul>
</li>
<li>
<p><strong>404 NOT FOUND</strong>: No data available for the given date range.</p>
<ul>
<li>Example: No Google Ads data found for the specified date range.</li>
<li>Example Response:<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
  <span class="token string">"error"</span><span class="token punctuation">:</span> <span class="token string">"No data available for the specified date range."</span>
<span class="token punctuation">}</span>
</code></pre>
</li>
</ul>
</li>
<li>
<p><strong>500 INTERNAL SERVER ERROR</strong>: Unexpected internal errors, such as Google Ads API issues or data processing errors.</p>
<ul>
<li>Example Response:<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
  <span class="token string">"error"</span><span class="token punctuation">:</span> <span class="token string">"An unexpected error occurred. Please try again later."</span>
<span class="token punctuation">}</span>
</code></pre>
</li>
</ul>
</li>
</ul>
<hr>
<h3 id="methods-in-detail"><strong>Methods in Detail</strong></h3>
<h4 id="postself-request"><strong>1. post(self, request)</strong></h4>
<ul>
<li><strong>Description</strong>: Processes POST requests to return Google Ads performance metrics.</li>
<li><strong>Usage</strong>: Call this method with a valid <code>start_date</code> and <code>end_date</code> to get the dashboard data.</li>
<li><strong>Response Structure</strong>: The response contains overall campaign metrics, daily breakdowns, top ads, and top URLs.</li>
<li><strong>Error Handling</strong>: Handles invalid dates, API issues, and missing data gracefully with appropriate status codes and messages.</li>
</ul>
<hr>
<h3 id="helper-methods"><strong>Helper Methods</strong></h3>
<h4 id="get_google_ads_clientself"><strong>2. get_google_ads_client(self)</strong></h4>
<ul>
<li><strong>Description</strong>: Returns the <code>GoogleAdsClient</code> object needed to communicate with the Google Ads API.</li>
<li><strong>Usage</strong>: This is called internally to set up the Google Ads client using the YAML configuration stored in the <code>GOOGLE_ADS_YAML_PATH</code> environment variable.</li>
</ul>
<h4 id="get_metricsself-client-customer_id-start_date-end_date"><strong>3. get_metrics(self, client, customer_id, start_date, end_date)</strong></h4>
<ul>
<li><strong>Description</strong>: Fetches key performance metrics like impressions, clicks, cost, and conversions for the specified date range.</li>
<li><strong>Returns</strong>: A pandas DataFrame with columns such as impressions, clicks, cost, conversions.</li>
<li><strong>Error Handling</strong>: If data retrieval fails, logs the error and returns an appropriate message.</li>
</ul>
<h4 id="calculate_metricsself-df"><strong>4. calculate_metrics(self, df)</strong></h4>
<ul>
<li>
<p><strong>Description</strong>: Aggregates and calculates overall metrics from the data, such as CTR (Click-Through Rate), CPC (Cost Per Click), and ROAS (Return on Ad Spend).</p>
</li>
<li>
<p><strong>Returns</strong>: A dictionary with formatted metrics.</p>
</li>
<li>
<p><strong>Key Calculations</strong>:</p>
<ul>
<li><strong>CTR (Click-Through Rate)</strong>: <code>(Clicks / Impressions) * 100</code></li>
<li><strong>CPC (Cost Per Click)</strong>: <code>Cost / Clicks</code></li>
<li><strong>ROAS (Return on Ad Spend)</strong>: <code>Conversion Value / Cost</code></li>
</ul>
</li>
</ul>
<h4 id="format_metricself-value"><strong>5. format_metric(self, value)</strong></h4>
<ul>
<li><strong>Description</strong>: Formats the values, ensuring that floats are rounded to two decimal places or converted to integers where appropriate.</li>
<li><strong>Example</strong>:
<ul>
<li><code>format_metric(12345.6789)</code> → <code>12,345.68</code></li>
<li><code>format_metric(100)</code> → <code>100</code></li>
</ul>
</li>
</ul>
<h4 id="get_top_adsself-client-customer_id-start_date-end_date"><strong>6. get_top_ads(self, client, customer_id, start_date, end_date)</strong></h4>
<ul>
<li><strong>Description</strong>: Retrieves the top 10 ads based on impressions for the given date range.</li>
<li><strong>Returns</strong>: A list of dictionaries, each representing an ad with associated metrics like clicks, impressions, cost, and conversions.</li>
</ul>
<h4 id="get_top_destination_urlsself-client-customer_id"><strong>7. get_top_destination_urls(self, client, customer_id)</strong></h4>
<ul>
<li><strong>Description</strong>: Fetches the top 10 destination URLs based on clicks over the last 30 days.</li>
<li><strong>Returns</strong>: A list of URLs and their associated metrics.</li>
</ul>
<h4 id="get_daily_metricsself-df-start_date-end_date"><strong>8. get_daily_metrics(self, df, start_date, end_date)</strong></h4>
<ul>
<li><strong>Description</strong>: Extracts and formats daily metrics (e.g., spend, clicks, conversions) for the date range.</li>
<li><strong>Returns</strong>: A list of dictionaries, each representing daily metrics.</li>
</ul>
<hr>
<h3 id="custom-serializers"><strong>Custom Serializers</strong></h3>
<h4 id="dashboardrequestserializer"><strong>DashboardRequestSerializer</strong></h4>
<ul>
<li><strong>Description</strong>: Validates the incoming request to ensure <code>start_date</code> and <code>end_date</code> are present and properly formatted.</li>
<li><strong>Validation Rules</strong>:
<ul>
<li>Both dates must follow the <code>YYYY-MM-DD</code> format.</li>
<li><code>end_date</code> should be equal to or after <code>start_date</code>.</li>
</ul>
</li>
</ul>
<h4 id="dashboardresponseserializerv1"><strong>DashboardResponseSerializerv1</strong></h4>
<ul>
<li><strong>Description</strong>: Formats the output for the response, ensuring the data returned to the client is in the correct structure.</li>
<li><strong>Usage</strong>: Automatically called to structure the response for the dashboard.</li>
</ul>
<hr>
<h3 id="user-guide-common-use-cases"><strong>User Guide: Common Use Cases</strong></h3>
<h4 id="fetching-metrics-for-the-last-7-days"><strong>1. Fetching Metrics for the Last 7 Days</strong></h4>
<p>You can easily retrieve metrics for the last week by making a POST request with the appropriate date range.</p>
<pre class=" language-bash"><code class="prism  language-bash">curl -X POST http://api.example.com/api/dashboard/ \
-H <span class="token string">"Content-Type: application/json"</span> \
-d <span class="token string">'{
  "start_date": "2024-01-01",
  "end_date": "2024-01-07"
}'</span>
</code></pre>
<h4 id="handling-errors"><strong>2. Handling Errors</strong></h4>
<p>Ensure that <code>start_date</code> and <code>end_date</code> are provided in the correct format. If you don’t get any data, confirm that your Google Ads account has data for the given date range.</p>
<h2 id="winning_campaign-api"><strong>2.Winning_campaign API</strong></h2>
<h2 id="overview-1">Overview</h2>
<p>The <strong>Winning campaign</strong> helps you improve the performance of your Google Ads campaigns by identifying ad sets with high potential and suggesting budget adjustments. By analyzing key performance metrics like <strong>Cost Per Acquisition (CPA)</strong>, <strong>Return on Ad Spend (ROAS)</strong>, and <strong>Click-Through Rate (CTR)</strong>, it finds underused ad sets that can be scaled to deliver better results.</p>
<p>This tool reduces wasted clicks and optimizes ad spend, making it easier to focus on ad sets that bring more value for your budget.</p>
<h2 id="features-1">Features</h2>
<ul>
<li><strong>Automated Performance Review:</strong> The tool retrieves and analyzes ad performance data for the last 30 days.</li>
<li><strong>Winning Ad Sets Detection:</strong> It identifies high-performing ad sets that have a low CPA and significant conversions.</li>
<li><strong>Recommendations for Scaling:</strong> You receive recommendations to increase the budget by 20% for the identified ad sets to maximize their potential.</li>
<li><strong>Click Fraud Detection:</strong> Monitors click rates to prevent wasted spend on suspicious or fraudulent clicks.</li>
</ul>
<h2 id="key-metrics-to-understand">Key Metrics to Understand</h2>
<ul>
<li><strong>Impressions:</strong> The number of times your ad was displayed.</li>
<li><strong>Clicks:</strong> The number of times users clicked on your ad.</li>
<li><strong>Conversions:</strong> The number of completed goals (such as purchases or sign-ups) resulting from the ad.</li>
<li><strong>CPA (Cost Per Acquisition):</strong> The average cost spent to get one conversion.</li>
<li><strong>ROAS (Return on Ad Spend):</strong> How much revenue you generate for every dollar spent on ads.</li>
<li><strong>CTR (Click-Through Rate):</strong> The percentage of impressions that turned into clicks.</li>
</ul>
<p>These metrics help you gauge the effectiveness of your ad sets and determine where to allocate more budget.</p>
<hr>
<h2 id="how-it-works">How It Works</h2>
<h3 id="step-1-retrieve-performance-data">Step 1: Retrieve Performance Data</h3>
<ul>
<li>The tool automatically fetches your <strong>Search Campaign</strong> performance data for the last 30 days, including metrics like impressions, clicks, cost, conversions, and ROAS.</li>
</ul>
<h3 id="step-2-identify-winning-ad-sets">Step 2: Identify Winning Ad Sets</h3>
<ul>
<li>
<p><strong>Criteria for Winning Ad Sets:</strong></p>
<ul>
<li><strong>Conversions:</strong> The ad set should have at least 10 conversions in the past 30 days.</li>
<li><strong>CPA Threshold:</strong> The ad set should have a CPA lower than ₹1000 (adjustable).</li>
</ul>
<p>These are the ad sets that have been performing well and are likely to benefit from more budget.</p>
</li>
</ul>
<h3 id="step-3-generate-recommendations">Step 3: Generate Recommendations</h3>
<ul>
<li>For each winning ad set, the system calculates a recommended budget increase by 20% (scale factor).</li>
<li>It provides detailed insights into the current performance, suggested budget, and the expected percentage increase.</li>
</ul>
<hr>
<h2 id="user-interface--recommendations">User Interface &amp; Recommendations</h2>
<p>When accessing the <strong>Wasted Clicks View</strong>, you’ll see a list of high-performing ad sets with the following details:</p>
<h3 id="example-display">Example Display:</h3>

<table>
<thead>
<tr>
<th><strong>Campaign</strong></th>
<th><strong>Ad Group</strong></th>
<th><strong>Impressions</strong></th>
<th><strong>Clicks</strong></th>
<th><strong>Conversions</strong></th>
<th><strong>CPA (₹)</strong></th>
<th><strong>ROAS</strong></th>
<th><strong>CTR</strong></th>
<th><strong>Current Spend (₹)</strong></th>
<th><strong>Recommended Budget (₹)</strong></th>
<th><strong>Budget Increase (%)</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>Campaign 1</td>
<td>Ad Group A</td>
<td>20,000</td>
<td>1000</td>
<td>20</td>
<td>800</td>
<td>4.2</td>
<td>5%</td>
<td>20,000</td>
<td>24,000</td>
<td>20%</td>
</tr>
<tr>
<td>Campaign 2</td>
<td>Ad Group B</td>
<td>10,000</td>
<td>500</td>
<td>12</td>
<td>950</td>
<td>3.5</td>
<td>5%</td>
<td>15,000</td>
<td>18,000</td>
<td>20%</td>
</tr>
</tbody>
</table><hr>
<h3 id="how-to-interpret-the-results">How to Interpret the Results</h3>
<ul>
<li><strong>Campaign/Ad Group Information:</strong> Shows which campaign and ad group performed well.</li>
<li><strong>Impressions/Clicks:</strong> Gives you an idea of how many people are seeing and interacting with your ad.</li>
<li><strong>Conversions:</strong> The number of actions taken based on the ad, such as purchases or sign-ups.</li>
<li><strong>CPA (₹):</strong> Helps you understand how much you’re paying for each conversion. A lower CPA indicates good performance.</li>
<li><strong>ROAS:</strong> Return on Ad Spend shows how much you’re earning for each rupee spent. The higher the ROAS, the better.</li>
<li><strong>CTR:</strong> Indicates how often users clicked on your ad compared to how often it was shown.</li>
<li><strong>Current Budget &amp; Recommended Budget:</strong> Shows your current spending and suggests a budget increase of 20% for top-performing ad sets.</li>
</ul>
<h3 id="how-to-use-the-recommendations">How to Use the Recommendations</h3>
<h3 id="increase-budget-for-winning-ad-sets">1. <strong>Increase Budget for Winning Ad Sets</strong></h3>
<ul>
<li>Once you’ve identified the top ad sets, you can apply the recommended 20% budget increase to maximize their potential.</li>
<li>This helps ensure that you’re allocating more resources to ad sets that are already performing well and likely to bring more conversions.</li>
</ul>
<h3 id="monitor-cpa-and-roas">2. <strong>Monitor CPA and ROAS</strong></h3>
<ul>
<li>Keep an eye on the CPA and ROAS values. A low CPA means you’re paying less for each conversion, while a high ROAS means you’re getting more return for every rupee spent.</li>
</ul>
<h3 id="review-invalid-click-rates">3. <strong>Review Invalid Click Rates</strong></h3>
<ul>
<li>If the tool detects invalid clicks (like fraud or bot activity), it will alert you. This helps protect your budget by flagging campaigns with a high rate of invalid clicks.</li>
</ul>
<h3 id="error-handling">Error Handling</h3>
<p>If something goes wrong, here’s what the system will do:</p>
<ol>
<li>
<p><strong>Google Ads API Error:</strong> If there’s an issue with accessing data from the Google Ads API, the system will notify you with an error message like:</p>
<ul>
<li><code>"Google Ads API error: {error code}"</code></li>
</ul>
</li>
<li>
<p><strong>Unexpected Errors:</strong> If something unexpected happens, you will see this message:</p>
<ul>
<li><code>"An unexpected error occurred: {error message}"</code></li>
</ul>
</li>
</ol>
<p>These error messages help you quickly identify any issues with the system or Google Ads API.</p>
<h2 id="invalid-click-analysis"><strong>Invalid Click Analysis</strong></h2>
<p>This <code>InvalidClickAnalysisView</code> class provides an API view that fetches Google Ads campaign data, analyzes invalid clicks, and reports on wasted ad spend due to those clicks. Here’s a breakdown of how it works and how users can benefit:</p>
<h3 id="key-features">Key Features:</h3>
<ol>
<li>
<p><strong>Data Retrieval:</strong></p>
<ul>
<li>Fetches campaign metrics, including total clicks, invalid clicks, and costs for the selected date range (defaulting to the past 30 days).</li>
<li>Focuses only on active and ongoing campaigns.</li>
</ul>
</li>
<li>
<p><strong>Campaign Analysis:</strong></p>
<ul>
<li>Calculates invalid click rates, cost per click in INR, and the wasted spend due to invalid clicks.</li>
<li>Provides a detailed analysis for each campaign, including the percentage of clicks that are invalid.</li>
</ul>
</li>
<li>
<p><strong>Summary Statistics:</strong></p>
<ul>
<li>Offers an overview of key metrics, including the total number of active campaigns, total wasted spend, and high-risk campaigns (those with a higher-than-threshold invalid click rate).</li>
</ul>
</li>
<li>
<p><strong>High-Risk Campaigns Identification:</strong></p>
<ul>
<li>Flags campaigns with an invalid click rate exceeding a predefined threshold (<code>HIGH_INVALID_CLICK_RATE_THRESHOLD</code>), helping users focus on campaigns that may be targeted by bots or click fraud.</li>
</ul>
</li>
</ol>
<h3 id="response-structure">Response Structure:</h3>
<p>The API response provides:</p>
<ul>
<li><strong>Campaign Analysis:</strong> A detailed list of campaigns with key metrics (clicks, invalid clicks, invalid click rate, and wasted spend).</li>
<li><strong>Summary Statistics:</strong> Aggregated data, such as total active campaigns and total wasted ad spend.</li>
<li><strong>High-Risk Campaigns:</strong> A separate list highlighting campaigns with unusually high invalid click rates, providing details on the wasted spend for these campaigns.</li>
</ul>
<h3 id="how-users-benefit">How Users Benefit:</h3>
<ol>
<li>
<p><strong>Budget Optimization:</strong></p>
<ul>
<li>Helps users identify campaigns where ad spend is being wasted on invalid clicks, enabling them to take action (e.g., pausing or adjusting bids).</li>
</ul>
</li>
<li>
<p><strong>Click Fraud Monitoring:</strong></p>
<ul>
<li>Provides visibility into campaigns that may be experiencing fraudulent activity or non-human interactions, allowing users to mitigate risks by reducing exposure to click fraud.</li>
</ul>
</li>
<li>
<p><strong>Actionable Insights:</strong></p>
<ul>
<li>By highlighting high-risk campaigns, users can focus their efforts on minimizing wasted spend and maximizing the efficiency of their Google Ads campaigns.</li>
</ul>
</li>
</ol>
<h3 id="example-output">Example Output:</h3>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
  <span class="token string">"campaign_analysis"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
    <span class="token punctuation">{</span>
      <span class="token string">"name"</span><span class="token punctuation">:</span> <span class="token string">"Campaign A"</span><span class="token punctuation">,</span>
      <span class="token string">"clicks"</span><span class="token punctuation">:</span> <span class="token number">5000</span><span class="token punctuation">,</span>
      <span class="token string">"invalid_clicks"</span><span class="token punctuation">:</span> <span class="token number">100</span><span class="token punctuation">,</span>
      <span class="token string">"invalid_click_rate"</span><span class="token punctuation">:</span> <span class="token string">"2.00%"</span><span class="token punctuation">,</span>
      <span class="token string">"wasted_spend_inr"</span><span class="token punctuation">:</span> <span class="token string">"₹1500.00"</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    <span class="token punctuation">{</span>
      <span class="token string">"name"</span><span class="token punctuation">:</span> <span class="token string">"Campaign B"</span><span class="token punctuation">,</span>
      <span class="token string">"clicks"</span><span class="token punctuation">:</span> <span class="token number">3000</span><span class="token punctuation">,</span>
      <span class="token string">"invalid_clicks"</span><span class="token punctuation">:</span> <span class="token number">50</span><span class="token punctuation">,</span>
      <span class="token string">"invalid_click_rate"</span><span class="token punctuation">:</span> <span class="token string">"1.67%"</span><span class="token punctuation">,</span>
      <span class="token string">"wasted_spend_inr"</span><span class="token punctuation">:</span> <span class="token string">"₹800.00"</span>
    <span class="token punctuation">}</span>
  <span class="token punctuation">]</span><span class="token punctuation">,</span>
  <span class="token string">"summary_statistics"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
    <span class="token string">"total_active_campaigns"</span><span class="token punctuation">:</span> <span class="token number">2</span><span class="token punctuation">,</span>
    <span class="token string">"total_wasted_spend"</span><span class="token punctuation">:</span> <span class="token string">"₹2300.00"</span><span class="token punctuation">,</span>
    <span class="token string">"high_risk_campaigns"</span><span class="token punctuation">:</span> <span class="token number">0</span>
  <span class="token punctuation">}</span><span class="token punctuation">,</span>
  <span class="token string">"high_risk_campaigns"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token punctuation">]</span>
<span class="token punctuation">}</span>
</code></pre>
<h3 id="adperformance-analysis"><strong>4. AdPerformance Analysis</strong></h3>
<p>The <code>AdPerformance Analysis</code> is designed to help advertisers analyze their ad performance data from Google Ads and generate ad copy suggestions based on top-performing ad groups. This view uses the Google Ads API to retrieve data, processes the data to identify top-performing ad groups, and then leverages the OpenAI API to generate ad suggestions.</p>
<h4 id="endpoint"><strong>Endpoint</strong></h4>
<ul>
<li><strong>Method</strong>: <code>GET</code></li>
<li><strong>URL</strong>: <code>/ad-performance-analysis/</code></li>
</ul>
<h4 id="description"><strong>Description</strong></h4>
<p>The view analyzes Google Ads data for the last 30 days, identifies the top 5 ad groups based on revenue, and generates ad copy suggestions. It also provides recommendations to improve ad performance.</p>
<h4 id="response-fields"><strong>Response Fields</strong></h4>
<ul>
<li>
<p><strong>top_ad_groups</strong>: A dictionary containing the top 5 ad groups based on their revenue and spend percentages.</p>
<ul>
<li><code>revenue_percent</code>: Percentage of total revenue generated by the ad group.</li>
<li><code>spend_percent</code>: Percentage of total ad spend used by the ad group.</li>
<li><code>rank</code>: Rank of the ad group based on total revenue.</li>
</ul>
</li>
<li>
<p><strong>ad_suggestions</strong>: Ad copy suggestions generated based on the top-performing ad groups. Each suggestion includes a headline and two descriptions.</p>
</li>
<li>
<p><strong>recommendations</strong>: A list of actionable recommendations to improve ad performance and optimize ad copy creation.</p>
</li>
</ul>
<h4 id="sample-response"><strong>Sample Response</strong></h4>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
  <span class="token string">"top_ad_groups"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
    <span class="token string">"ad_group_1"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
      <span class="token string">"revenue_percent"</span><span class="token punctuation">:</span> <span class="token number">25.34</span><span class="token punctuation">,</span>
      <span class="token string">"spend_percent"</span><span class="token punctuation">:</span> <span class="token number">20.56</span><span class="token punctuation">,</span>
      <span class="token string">"rank"</span><span class="token punctuation">:</span> <span class="token number">1</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    <span class="token string">"ad_group_2"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
      <span class="token string">"revenue_percent"</span><span class="token punctuation">:</span> <span class="token number">18.75</span><span class="token punctuation">,</span>
      <span class="token string">"spend_percent"</span><span class="token punctuation">:</span> <span class="token number">15.22</span><span class="token punctuation">,</span>
      <span class="token string">"rank"</span><span class="token punctuation">:</span> <span class="token number">2</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    <span class="token operator">...</span>
  <span class="token punctuation">}</span><span class="token punctuation">,</span>
  <span class="token string">"ad_suggestions"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
    <span class="token punctuation">{</span>
      <span class="token string">"headline"</span><span class="token punctuation">:</span> <span class="token string">"Get ₹5000 Off on Mobiles!"</span><span class="token punctuation">,</span>
      <span class="token string">"description_1"</span><span class="token punctuation">:</span> <span class="token string">"Fast delivery and no-cost EMI available."</span><span class="token punctuation">,</span>
      <span class="token string">"description_2"</span><span class="token punctuation">:</span> <span class="token string">"Hurry! Limited time offer!"</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    <span class="token punctuation">{</span>
      <span class="token string">"headline"</span><span class="token punctuation">:</span> <span class="token string">"Upgrade to 5G Mobiles Today!"</span><span class="token punctuation">,</span>
      <span class="token string">"description_1"</span><span class="token punctuation">:</span> <span class="token string">"Special discounts on top brands."</span><span class="token punctuation">,</span>
      <span class="token string">"description_2"</span><span class="token punctuation">:</span> <span class="token string">"Get free accessories on your purchase!"</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    <span class="token operator">...</span>
  <span class="token punctuation">]</span><span class="token punctuation">,</span>
  <span class="token string">"recommendations"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
    <span class="token string">"Review the generated ad copy suggestions and consider testing them in a controlled environment."</span><span class="token punctuation">,</span>
    <span class="token string">"Focus on themes from top-performing ad groups in your new ads."</span><span class="token punctuation">,</span>
    <span class="token string">"Continuously monitor performance and iterate on your ad copy."</span><span class="token punctuation">,</span>
    <span class="token string">"Always adhere to Google Ads policies when creating new ads."</span><span class="token punctuation">,</span>
    <span class="token string">"Consider local cultural nuances and preferences in your ad copy."</span>
  <span class="token punctuation">]</span>
<span class="token punctuation">}</span>
</code></pre>
<h4 id="error-handling-1"><strong>Error Handling</strong></h4>
<ul>
<li>
<p><strong>Google Ads API Error</strong>: If an error occurs while fetching data from the Google Ads API, a 500 status response with an error message will be returned.</p>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
  <span class="token string">"error"</span><span class="token punctuation">:</span> <span class="token string">"Google Ads API error: RESOURCE_EXHAUSTED"</span>
<span class="token punctuation">}</span>
</code></pre>
</li>
<li>
<p><strong>Unexpected Error</strong>: If any other unexpected error occurs, the response will include an error message and the 500 status code.</p>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
  <span class="token string">"error"</span><span class="token punctuation">:</span> <span class="token string">"An unexpected error occurred: [error details]"</span>
<span class="token punctuation">}</span>
</code></pre>
</li>
</ul>
<h4 id="internal-methods"><strong>Internal Methods</strong></h4>
<ol>
<li>
<p><strong><code>get_google_ads_client(self)</code></strong></p>
<ul>
<li>
<p>Loads the Google Ads client configuration from the <code>GOOGLE_ADS_YAML_PATH</code> specified in <code>settings.py</code>.</p>
</li>
<li>
<p><strong>Returns</strong>: The initialized Google Ads client.</p>
</li>
</ul>
</li>
<li>
<p><strong><code>get_ad_performance(self, client, customer_id)</code></strong></p>
<ul>
<li>
<p>Queries the Google Ads API for performance data from the last 30 days. It retrieves metrics for impressions, clicks, cost, conversions, and ad group names.</p>
</li>
<li>
<p><strong>Returns</strong>: The raw data from the Google Ads API.</p>
</li>
</ul>
</li>
<li>
<p><strong><code>analyze_top_phrases_and_tags(self, ads_data)</code></strong></p>
<ul>
<li>
<p>Processes the raw ad data and extracts phrases from the ad headlines and descriptions. It calculates the total revenue, spend, and impressions for each ad group and ranks them based on revenue.</p>
</li>
<li>
<p><strong>Returns</strong>: A DataFrame with the top 5 ad groups, including revenue and spend percentages, impressions, and rank.</p>
</li>
</ul>
</li>
<li>
<p><strong><code>generate_ad_suggestions(self, top_ad_groups)</code></strong></p>
<ul>
<li>
<p>Calls the OpenAI API to generate ad copy suggestions based on the top-performing ad groups. The suggestions are tailored for an Indian audience, considering cultural nuances and using INR for price mentions.</p>
</li>
<li>
<p><strong>Returns</strong>: A list of ad copy suggestions (headline and descriptions).</p>
</li>
</ul>
</li>
</ol>
<h4 id="example-flow"><strong>Example Flow</strong></h4>
<ol>
<li>
<p><strong>Data Retrieval</strong>:</p>
<ul>
<li>The view fetches ad performance data from Google Ads, filtering it to only include the last 30 days.</li>
</ul>
</li>
<li>
<p><strong>Data Processing</strong>:</p>
<ul>
<li>The ad data is processed to aggregate metrics (impressions, clicks, costs, conversions) by ad group, and the top ad groups are identified based on revenue.</li>
</ul>
</li>
<li>
<p><strong>Ad Copy Generation</strong>:</p>
<ul>
<li>Based on the themes of the top-performing ad groups, ad copy suggestions are generated using OpenAI’s <code>gpt-3.5-turbo</code> model. The suggestions are tailored to the Indian market.</li>
</ul>
</li>
<li>
<p><strong>Recommendations</strong>:</p>
<ul>
<li>The view generates actionable recommendations for the user to optimize their ad campaigns based on the data analysis.</li>
</ul>
</li>
</ol>
<h4 id="recommendations-provided"><strong>Recommendations Provided</strong></h4>
<ol>
<li>Review the generated ad copy suggestions and consider testing them in a controlled environment.</li>
<li>Focus on themes from top-performing ad groups in your new ads.</li>
<li>Continuously monitor performance and iterate on your ad copy.</li>
<li>Always adhere to Google Ads policies when creating new ads.</li>
<li>Consider local cultural nuances and preferences in your ad copy.</li>
</ol>
<p>Here is the documentation for your <code>CampaignScalingRecommendationView</code> class, similar to the format from the previous code:</p>
<hr>
<h3 id="campaign-scaling-recommendation"><strong>5.Campaign Scaling Recommendation</strong></h3>
<p>The <code>Campaign Scaling Recommendation</code> is a Django Rest Framework <code>APIView</code> designed to provide recommendations for scaling Google Ads campaigns. It interacts with the Google Ads API to identify high-performing campaigns based on their Return on Ad Spend (ROAS) and makes suggestions for increasing the budget for these campaigns.</p>
<h4 id="methods">Methods</h4>
<h5 id="getself-request"><code>get(self, request)</code></h5>
<p>Handles GET requests for scaling recommendations.</p>
<ul>
<li><strong>Purpose</strong>: Fetches scalable Google Ads campaigns and generates budget recommendations.</li>
<li><strong>Response</strong>: A JSON response containing:
<ul>
<li><code>recommendations</code>: A list of campaign scaling recommendations, including the current and recommended budgets.</li>
<li><code>total_campaigns_for_scaling</code>: The total number of campaigns recommended for scaling.</li>
</ul>
</li>
<li><strong>Errors</strong>: Returns detailed error messages in case of Google Ads API failure or unexpected issues.</li>
</ul>
<h5 id="get_google_ads_clientself-1"><code>get_google_ads_client(self)</code></h5>
<ul>
<li><strong>Purpose</strong>: Instantiates and returns a Google Ads client using the credentials stored in the YAML file.</li>
<li><strong>Returns</strong>: A <code>GoogleAdsClient</code> instance loaded from the file path specified in the <code>GOOGLE_ADS_YAML_PATH</code> setting.</li>
</ul>
<h5 id="get_scalable_campaignsself-client-customer_id"><code>get_scalable_campaigns(self, client, customer_id)</code></h5>
<ul>
<li>
<p><strong>Purpose</strong>: Queries the Google Ads API for enabled campaigns from the last 7 days, checking each campaign’s ROAS and other performance metrics.</p>
</li>
<li>
<p><strong>Input Parameters</strong>:</p>
<ul>
<li><code>client</code>: A <code>GoogleAdsClient</code> instance.</li>
<li><code>customer_id</code>: The Google Ads customer ID for the account.</li>
</ul>
</li>
<li>
<p><strong>Returns</strong>: A list of campaigns that are eligible for scaling based on the following criteria:</p>
<ul>
<li>The ROAS (Return on Ad Spend) for the past 7 days is greater than 10.</li>
<li>The campaign has been running for more than 72 hours.</li>
</ul>
</li>
<li>
<p><strong>Google Ads Query</strong>:</p>
<ul>
<li>The query selects the campaign ID, name, ROAS, cost, start date, budget, and status.</li>
<li>Filters only campaigns that are currently enabled and that have data for the last 7 days.</li>
</ul>
</li>
</ul>
<h5 id="generate_recommendationsself-scalable_campaigns-scale_factor1.2"><code>generate_recommendations(self, scalable_campaigns, scale_factor=1.2)</code></h5>
<ul>
<li><strong>Purpose</strong>: Generates recommendations for scaling campaign budgets.</li>
<li><strong>Input Parameters</strong>:
<ul>
<li><code>scalable_campaigns</code>: A list of campaigns identified as suitable for scaling.</li>
<li><code>scale_factor</code>: The factor by which to increase the current campaign budget. The default value is 1.2 (i.e., a 20% increase).</li>
</ul>
</li>
<li><strong>Returns</strong>: A list of recommendations, where each recommendation contains:
<ul>
<li><code>campaign_id</code>: The ID of the campaign.</li>
<li><code>campaign_name</code>: The name of the campaign.</li>
<li><code>current_budget</code>: The current daily budget of the campaign.</li>
<li><code>recommended_budget</code>: The new recommended budget after scaling.</li>
<li><code>roas_7d</code>: The ROAS (Return on Ad Spend) for the past 7 days.</li>
</ul>
</li>
</ul>
<hr>
<h4 id="error-handling-2">Error Handling</h4>
<ul>
<li><strong>GoogleAdsException</strong>: Catches any errors related to the Google Ads API, logs the error, and returns an error response with a 500 status.</li>
<li><strong>General Exception</strong>: Catches any other unexpected exceptions, logs the error, and returns a generic error message with a 500 status.</li>
</ul>
<hr>
<h4 id="example-response">Example Response</h4>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
  <span class="token string">"recommendations"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
    <span class="token punctuation">{</span>
      <span class="token string">"campaign_id"</span><span class="token punctuation">:</span> <span class="token string">"123456789"</span><span class="token punctuation">,</span>
      <span class="token string">"campaign_name"</span><span class="token punctuation">:</span> <span class="token string">"Summer Sale Campaign"</span><span class="token punctuation">,</span>
      <span class="token string">"current_budget"</span><span class="token punctuation">:</span> <span class="token number">5000.00</span><span class="token punctuation">,</span>
      <span class="token string">"recommended_budget"</span><span class="token punctuation">:</span> <span class="token number">6000.00</span><span class="token punctuation">,</span>
      <span class="token string">"roas_7d"</span><span class="token punctuation">:</span> <span class="token number">12.5</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    <span class="token punctuation">{</span>
      <span class="token string">"campaign_id"</span><span class="token punctuation">:</span> <span class="token string">"987654321"</span><span class="token punctuation">,</span>
      <span class="token string">"campaign_name"</span><span class="token punctuation">:</span> <span class="token string">"New Year Campaign"</span><span class="token punctuation">,</span>
      <span class="token string">"current_budget"</span><span class="token punctuation">:</span> <span class="token number">10000.00</span><span class="token punctuation">,</span>
      <span class="token string">"recommended_budget"</span><span class="token punctuation">:</span> <span class="token number">12000.00</span><span class="token punctuation">,</span>
      <span class="token string">"roas_7d"</span><span class="token punctuation">:</span> <span class="token number">15.2</span>
    <span class="token punctuation">}</span>
  <span class="token punctuation">]</span><span class="token punctuation">,</span>
  <span class="token string">"total_campaigns_for_scaling"</span><span class="token punctuation">:</span> <span class="token number">2</span>
<span class="token punctuation">}</span>
</code></pre>
<p>Here is the documentation for your <code>AdPerformanceRecommendationView</code> class in a similar format as requested:</p>
<hr>
<h3 id="adperformance-recommendation"><strong>6.AdPerformance Recommendation</strong></h3>
<p>The <code>AdPerformance Recommendation</code> is a Django Rest Framework <code>APIView</code> that provides performance analysis of Google Ads campaigns. It retrieves data on campaign performance, analyzes the metrics, and makes recommendations for improving campaign efficiency, such as adjusting the budget or improving ad relevance.</p>
<h4 id="methods-1">Methods</h4>
<h5 id="getself-request-1"><code>get(self, request)</code></h5>
<p>Handles GET requests to analyze the performance of ads and return actionable recommendations.</p>
<ul>
<li><strong>Purpose</strong>: Fetches Google Ads campaign performance for the last 30 days and generates improvement recommendations based on metrics like Cost per Conversion, CTR (Click-Through Rate), and Cost per Click.</li>
<li><strong>Response</strong>: A JSON response containing:
<ul>
<li><code>recommendations</code>: A list of performance-based recommendations for each campaign.</li>
<li><code>total_recommendations</code>: The total number of recommendations generated.</li>
</ul>
</li>
<li><strong>Errors</strong>: Handles and logs Google Ads API-related and unexpected errors, returning appropriate error responses.</li>
</ul>
<h5 id="get_google_ads_clientself-2"><code>get_google_ads_client(self)</code></h5>
<ul>
<li><strong>Purpose</strong>: Instantiates and returns a Google Ads client using the credentials stored in the YAML file.</li>
<li><strong>Returns</strong>: A <code>GoogleAdsClient</code> instance loaded from the file path specified in the <code>GOOGLE_ADS_YAML_PATH</code> setting.</li>
</ul>
<h5 id="analyze_ad_performanceself-client-customer_id"><code>analyze_ad_performance(self, client, customer_id)</code></h5>
<ul>
<li>
<p><strong>Purpose</strong>: Analyzes the performance of active Google Ads campaigns over the past 30 days.</p>
</li>
<li>
<p><strong>Input Parameters</strong>:</p>
<ul>
<li><code>client</code>: A <code>GoogleAdsClient</code> instance.</li>
<li><code>customer_id</code>: The Google Ads customer ID for the account.</li>
</ul>
</li>
<li>
<p><strong>Returns</strong>: A list of recommendations based on the following metrics:</p>
<ul>
<li><strong>Cost per Conversion (CPA)</strong>: If the cost per conversion is higher than the defined <code>TARGET_CPA</code> in settings, a recommendation is generated to reduce the campaign budget.</li>
<li><strong>No Conversions with High Cost</strong>: If a campaign has spent more than the <code>COST_THRESHOLD</code> but has no conversions, a recommendation is generated to review its effectiveness.</li>
<li><strong>Low CTR (Click-Through Rate)</strong>: If the CTR is lower than the <code>CTR_THRESHOLD</code>, a recommendation is generated to improve the ad relevance.</li>
</ul>
</li>
<li>
<p><strong>Google Ads Query</strong>:</p>
<ul>
<li>The query selects the campaign ID, name, cost, conversions, clicks, and impressions over the last 30 days, filtering for enabled campaigns that are currently serving ads.</li>
</ul>
</li>
</ul>
<h5 id="format_inrself-amount"><code>format_inr(self, amount)</code></h5>
<ul>
<li><strong>Purpose</strong>: Formats monetary values in Indian Rupees.</li>
<li><strong>Input Parameters</strong>:
<ul>
<li><code>amount</code>: The amount to be formatted.</li>
</ul>
</li>
<li><strong>Returns</strong>: The formatted string representation of the amount in INR (Indian Rupees), prefixed with <code>₹</code>.</li>
</ul>
<hr>
<h4 id="error-handling-3">Error Handling</h4>
<ul>
<li><strong>GoogleAdsException</strong>: Catches errors related to the Google Ads API, logs them, and returns a 500 error response indicating the specific Google Ads API error.</li>
<li><strong>General Exception</strong>: Catches unexpected exceptions, logs them, and returns a generic error message with a 500 status.</li>
</ul>
<hr>
<h4 id="example-response-1">Example Response</h4>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
  <span class="token string">"recommendations"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
    <span class="token punctuation">{</span>
      <span class="token string">"campaign_id"</span><span class="token punctuation">:</span> <span class="token string">"123456789"</span><span class="token punctuation">,</span>
      <span class="token string">"campaign_name"</span><span class="token punctuation">:</span> <span class="token string">"Holiday Campaign"</span><span class="token punctuation">,</span>
      <span class="token string">"recommendation"</span><span class="token punctuation">:</span> <span class="token string">"Consider reducing budget. Cost per conversion (₹550.00) is higher than target (₹500.00)."</span><span class="token punctuation">,</span>
      <span class="token string">"metrics"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
        <span class="token string">"cost"</span><span class="token punctuation">:</span> <span class="token string">"₹11,000.00"</span><span class="token punctuation">,</span>
        <span class="token string">"conversions"</span><span class="token punctuation">:</span> <span class="token number">20</span><span class="token punctuation">,</span>
        <span class="token string">"cpc"</span><span class="token punctuation">:</span> <span class="token string">"₹55.00"</span><span class="token punctuation">,</span>
        <span class="token string">"ctr"</span><span class="token punctuation">:</span> <span class="token string">"2.50%"</span>
      <span class="token punctuation">}</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    <span class="token punctuation">{</span>
      <span class="token string">"campaign_id"</span><span class="token punctuation">:</span> <span class="token string">"987654321"</span><span class="token punctuation">,</span>
      <span class="token string">"campaign_name"</span><span class="token punctuation">:</span> <span class="token string">"Summer Sales Campaign"</span><span class="token punctuation">,</span>
      <span class="token string">"recommendation"</span><span class="token punctuation">:</span> <span class="token string">"Review campaign effectiveness. Spent ₹15,000.00 with no conversions."</span><span class="token punctuation">,</span>
      <span class="token string">"metrics"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
        <span class="token string">"cost"</span><span class="token punctuation">:</span> <span class="token string">"₹15,000.00"</span><span class="token punctuation">,</span>
        <span class="token string">"conversions"</span><span class="token punctuation">:</span> <span class="token number">0</span><span class="token punctuation">,</span>
        <span class="token string">"cpc"</span><span class="token punctuation">:</span> <span class="token string">"₹50.00"</span><span class="token punctuation">,</span>
        <span class="token string">"ctr"</span><span class="token punctuation">:</span> <span class="token string">"1.20%"</span>
      <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
  <span class="token punctuation">]</span><span class="token punctuation">,</span>
  <span class="token string">"total_recommendations"</span><span class="token punctuation">:</span> <span class="token number">2</span>
<span class="token punctuation">}</span>
</code></pre>
<h4 id="recommendations-logic">Recommendations Logic</h4>
<ol>
<li>
<p><strong>High Cost per Conversion</strong>:</p>
<ul>
<li>If the cost per conversion exceeds the <code>TARGET_CPA</code> from settings, the system will recommend reducing the campaign’s budget to align costs with the desired CPA target.</li>
</ul>
</li>
<li>
<p><strong>No Conversions with High Spend</strong>:</p>
<ul>
<li>If a campaign has spent more than the <code>COST_THRESHOLD</code> without any conversions, the system will recommend reviewing the campaign for effectiveness and possible adjustments.</li>
</ul>
</li>
<li>
<p><strong>Low CTR</strong>:</p>
<ul>
<li>If the campaign’s CTR (Click-Through Rate) falls below the <code>CTR_THRESHOLD</code>, the system will suggest improving the ad’s relevance to increase click rates.</li>
</ul>
</li>
</ol>
<p>Here’s the documentation for the <code>OverspendingAdsView</code> class, structured similarly to the previous documentation style:</p>
<hr>
<h2 id="overspending-ads"><strong>2.Overspending Ads</strong></h2>
<p>The <code>Overspending Ads</code> class is a Django REST Framework API view designed to analyze Google Ads performance and provide recommendations for campaigns and ad groups that are overspending based on specified thresholds. The class utilizes the Google Ads API to gather performance metrics and can leverage OpenAI’s GPT-3.5 to generate actionable recommendations.</p>
<h2 id="methods-2">Methods</h2>
<h3 id="getself-request-2"><code>get(self, request)</code></h3>
<p>Handles GET requests to retrieve overspending ads recommendations.</p>
<h4 id="parameters">Parameters</h4>
<ul>
<li><strong>request</strong>: The incoming HTTP request containing query parameters for analysis.</li>
</ul>
<h4 id="query-parameters">Query Parameters</h4>
<ul>
<li><strong>target_cpa</strong>: The target cost per acquisition. Default is <strong>3500</strong>.</li>
<li><strong>cost_threshold</strong>: The maximum allowable cost before a warning is generated. Default is <strong>7000</strong>.</li>
<li><strong>ctr_threshold</strong>: The minimum click-through rate percentage to trigger a warning. Default is <strong>1.0</strong>.</li>
</ul>
<h4 id="returns">Returns</h4>
<ul>
<li><strong>Response</strong>: JSON object containing:
<ul>
<li><code>campaign_recommendations</code>: List of recommendations for campaigns.</li>
<li><code>adgroup_recommendations</code>: List of recommendations for ad groups.</li>
<li><code>parameters</code>: The parameters used for analysis.</li>
</ul>
</li>
</ul>
<h4 id="error-handling-4">Error Handling</h4>
<ul>
<li>Returns an error response for various exceptions:
<ul>
<li><strong>GoogleAdsException</strong>: Returns a 500 status with error details from the Google Ads API.</li>
<li><strong>Timeout</strong>: Returns a 504 status indicating a request timeout.</li>
<li><strong>Exception</strong>: Catches all other exceptions and returns a 500 status with the error message.</li>
</ul>
</li>
</ul>
<h3 id="get_google_ads_clientself-3"><code>get_google_ads_client(self)</code></h3>
<p>Creates and returns a Google Ads client using credentials from the specified YAML configuration file.</p>
<h4 id="returns-1">Returns</h4>
<ul>
<li><strong>GoogleAdsClient</strong>: An instance of the Google Ads client.</li>
</ul>
<h3 id="analyze_performanceself-client-customer_id-target_cpa-cost_threshold-ctr_threshold"><code>analyze_performance(self, client, customer_id, target_cpa, cost_threshold, ctr_threshold)</code></h3>
<p>Analyzes the performance of campaigns and ad groups over the last 30 days and returns recommendations for overspending entities.</p>
<h4 id="parameters-1">Parameters</h4>
<ul>
<li><strong>client</strong>: An instance of the Google Ads client.</li>
<li><strong>customer_id</strong>: The Google Ads customer ID to analyze.</li>
<li><strong>target_cpa</strong>: The target cost per acquisition.</li>
<li><strong>cost_threshold</strong>: The maximum allowable cost.</li>
<li><strong>ctr_threshold</strong>: The minimum click-through rate percentage.</li>
</ul>
<h4 id="returns-2">Returns</h4>
<ul>
<li><strong>tuple</strong>: A tuple containing:
<ul>
<li><code>campaign_recommendations</code>: List of campaign recommendations.</li>
<li><code>adgroup_recommendations</code>: List of ad group recommendations.</li>
</ul>
</li>
</ul>
<h3 id="analyze_entityself-row-entity_type-target_cpa-cost_threshold-ctr_threshold"><code>analyze_entity(self, row, entity_type, target_cpa, cost_threshold, ctr_threshold)</code></h3>
<p>Analyzes a specific campaign or ad group entity to determine if it meets performance standards and generates recommendations if necessary.</p>
<h4 id="parameters-2">Parameters</h4>
<ul>
<li><strong>row</strong>: The data row from Google Ads API response.</li>
<li><strong>entity_type</strong>: Type of entity being analyzed (“campaign” or “ad_group”).</li>
<li><strong>target_cpa</strong>: The target cost per acquisition.</li>
<li><strong>cost_threshold</strong>: The maximum allowable cost.</li>
<li><strong>ctr_threshold</strong>: The minimum click-through rate percentage.</li>
</ul>
<h4 id="returns-3">Returns</h4>
<ul>
<li><strong>dict</strong> or <strong>None</strong>: A dictionary containing entity details and issues if any problems are found; otherwise, returns None.</li>
</ul>
<h3 id="get_ai_recommendations_with_fallbackself-entity_type-campaign_type-issues-metrics"><code>get_ai_recommendations_with_fallback(self, entity_type, campaign_type, issues, metrics)</code></h3>
<p>Retrieves AI-generated recommendations, falling back to rule-based recommendations if the AI call fails.</p>
<h4 id="parameters-3">Parameters</h4>
<ul>
<li><strong>entity_type</strong>: The type of entity (“campaign” or “ad_group”).</li>
<li><strong>campaign_type</strong>: The advertising channel type of the campaign.</li>
<li><strong>issues</strong>: List of identified issues for the entity.</li>
<li><strong>metrics</strong>: A dictionary containing performance metrics.</li>
</ul>
<h4 id="returns-4">Returns</h4>
<ul>
<li><strong>list</strong>: List of recommendations, either from AI or fallback options.</li>
</ul>
<h3 id="get_ai_recommendationsself-entity_type-campaign_type-issues-metrics"><code>get_ai_recommendations(self, entity_type, campaign_type, issues, metrics)</code></h3>
<p>Fetches AI-generated recommendations from OpenAI based on the provided parameters.</p>
<h4 id="parameters-4">Parameters</h4>
<ul>
<li><strong>entity_type</strong>: The type of entity (“campaign” or “ad_group”).</li>
<li><strong>campaign_type</strong>: The advertising channel type of the campaign.</li>
<li><strong>issues</strong>: List of identified issues for the entity.</li>
<li><strong>metrics</strong>: A dictionary containing performance metrics.</li>
</ul>
<h4 id="returns-5">Returns</h4>
<ul>
<li><strong>list</strong>: Formatted list of AI recommendations.</li>
</ul>
<h3 id="get_fallback_recommendationsself-entity_type-campaign_type-issues"><code>get_fallback_recommendations(self, entity_type, campaign_type, issues)</code></h3>
<p>Generates basic fallback recommendations based on identified issues if AI recommendations are unavailable.</p>
<h4 id="parameters-5">Parameters</h4>
<ul>
<li><strong>entity_type</strong>: The type of entity (“campaign” or “ad_group”).</li>
<li><strong>campaign_type</strong>: The advertising channel type of the campaign.</li>
<li><strong>issues</strong>: List of identified issues for the entity.</li>
</ul>
<h4 id="returns-6">Returns</h4>
<ul>
<li><strong>list</strong>: List of fallback recommendations.</li>
</ul>
<h3 id="format_ai_recommendationsself-ai_response"><code>format_ai_recommendations(self, ai_response)</code></h3>
<p>Formats the AI response into a structured list of recommendations.</p>
<h4 id="parameters-6">Parameters</h4>
<ul>
<li><strong>ai_response</strong>: The raw response string from the AI.</li>
</ul>
<h4 id="returns-7">Returns</h4>
<ul>
<li><strong>list</strong>: List of formatted recommendations.</li>
</ul>
<h3 id="format_inrself-amount-1"><code>format_inr(self, amount)</code></h3>
<p>Formats a numeric amount into Indian Rupees.</p>
<h4 id="parameters-7">Parameters</h4>
<ul>
<li><strong>amount</strong>: The numeric amount to format.</li>
</ul>
<h4 id="returns-8">Returns</h4>
<ul>
<li><strong>str</strong>: Formatted amount as a string in INR.</li>
</ul>
<p>Here’s the documentation for the <code>AdSetPerformanceAnalysisView</code> class, structured in a similar format as the previous documentation:</p>
<hr>
<h2 id="adset-performance-analysis"><strong>8. AdSet Performance Analysis</strong></h2>
<p>The <code>AdSetPerformanceAnalysisView</code> class is a Django REST Framework API view designed to analyze the performance of ad sets within Google Ads. It retrieves performance metrics such as clicks, impressions, and conversions, and generates recommendations based on user-defined thresholds for Click-Through Rate (CTR), Cost Per Click (CPC), and Conversion Rate. The class also suggests budget increases based on performance evaluations.</p>
<h2 id="constants">Constants</h2>
<h3 id="micro_to_inr"><code>MICRO_TO_INR</code></h3>
<ul>
<li><strong>Type</strong>: <code>int</code></li>
<li><strong>Description</strong>: A conversion factor to convert cost from micros to Indian Rupees. The value is set to <strong>1,000,000</strong>.</li>
</ul>
<h2 id="methods-3">Methods</h2>
<h3 id="getself-request-3"><code>get(self, request)</code></h3>
<p>Handles GET requests to retrieve the performance analysis of ad sets.</p>
<h4 id="parameters-8">Parameters</h4>
<ul>
<li><strong>request</strong>: The incoming HTTP request containing query parameters for performance analysis.</li>
</ul>
<h4 id="query-parameters-1">Query Parameters</h4>
<ul>
<li><strong>ctr_threshold</strong>: The threshold for Click-Through Rate (CTR). Default is <strong>0.05</strong>.</li>
<li><strong>cpc_threshold</strong>: The threshold for Cost Per Click (CPC). Default is <strong>50</strong>.</li>
<li><strong>conversion_rate_threshold</strong>: The threshold for Conversion Rate. Default is <strong>0.02</strong>.</li>
<li><strong>budget_increase_percentage</strong>: The percentage increase in budget suggested for well-performing ad sets. Default is <strong>20</strong>.</li>
</ul>
<h4 id="returns-9">Returns</h4>
<ul>
<li><strong>Response</strong>: JSON object containing:
<ul>
<li><code>ad_set_performance</code>: A dictionary with performance analysis for each ad set.</li>
<li><code>thresholds_used</code>: The thresholds used for analysis.</li>
</ul>
</li>
</ul>
<h4 id="error-handling-5">Error Handling</h4>
<ul>
<li>Returns an error response for various exceptions:
<ul>
<li><strong>GoogleAdsException</strong>: Returns a 500 status with error details from the Google Ads API.</li>
<li><strong>Exception</strong>: Catches all other exceptions and returns a 500 status with the error message.</li>
</ul>
</li>
</ul>
<h3 id="get_ad_set_performanceself-client-customer_id"><code>get_ad_set_performance(self, client, customer_id)</code></h3>
<p>Retrieves performance data for ad sets from Google Ads within the last 7 days.</p>
<h4 id="parameters-9">Parameters</h4>
<ul>
<li><strong>client</strong>: An instance of the Google Ads client.</li>
<li><strong>customer_id</strong>: The Google Ads customer ID to retrieve data for.</li>
</ul>
<h4 id="returns-10">Returns</h4>
<ul>
<li><strong>dict</strong>: A dictionary containing aggregated performance metrics for each ad set.</li>
</ul>
<h3 id="analyze_performanceself-ad_sets-ctr_threshold-cpc_threshold-conversion_rate_threshold-budget_increase_percentage"><code>analyze_performance(self, ad_sets, ctr_threshold, cpc_threshold, conversion_rate_threshold, budget_increase_percentage)</code></h3>
<p>Analyzes the performance of the retrieved ad sets against specified thresholds and prepares a structured response.</p>
<h4 id="parameters-10">Parameters</h4>
<ul>
<li><strong>ad_sets</strong>: The performance data for ad sets.</li>
<li><strong>ctr_threshold</strong>: The threshold for Click-Through Rate (CTR).</li>
<li><strong>cpc_threshold</strong>: The threshold for Cost Per Click (CPC).</li>
<li><strong>conversion_rate_threshold</strong>: The threshold for Conversion Rate.</li>
<li><strong>budget_increase_percentage</strong>: The suggested budget increase percentage.</li>
</ul>
<h4 id="returns-11">Returns</h4>
<ul>
<li><strong>dict</strong>: A structured dictionary containing analyzed performance data for each ad set.</li>
</ul>
<h3 id="calculate_metricsself-data"><code>calculate_metrics(self, data)</code></h3>
<p>Calculates various performance metrics from the provided ad set data.</p>
<h4 id="parameters-11">Parameters</h4>
<ul>
<li><strong>data</strong>: A dictionary containing raw performance data for an ad set.</li>
</ul>
<h4 id="returns-12">Returns</h4>
<ul>
<li><strong>dict</strong>: A dictionary with calculated metrics including impressions, clicks, cost, conversions, conversion values, CTR, CPC, conversion rate, and ROAS (Return on Ad Spend).</li>
</ul>
<h3 id="determine_performance_statusself-metrics-ctr_threshold-cpc_threshold-conversion_rate_threshold"><code>determine_performance_status(self, metrics, ctr_threshold, cpc_threshold, conversion_rate_threshold)</code></h3>
<p>Determines the performance status of an ad set based on calculated metrics and user-defined thresholds.</p>
<h4 id="parameters-12">Parameters</h4>
<ul>
<li><strong>metrics</strong>: A dictionary containing calculated metrics for the ad set.</li>
<li><strong>ctr_threshold</strong>: The threshold for Click-Through Rate (CTR).</li>
<li><strong>cpc_threshold</strong>: The threshold for Cost Per Click (CPC).</li>
<li><strong>conversion_rate_threshold</strong>: The threshold for Conversion Rate.</li>
</ul>
<h4 id="returns-13">Returns</h4>
<ul>
<li><strong>list</strong>: A list of performance status indicators (e.g., “Low CTR”, “High CPC”, “Low Conversion Rate”).</li>
</ul>
<h3 id="calculate_budget_increaseself-cost-performance_status-budget_increase_percentage"><code>calculate_budget_increase(self, cost, performance_status, budget_increase_percentage)</code></h3>
<p>Calculates the suggested budget increase based on the ad set’s performance status.</p>
<h4 id="parameters-13">Parameters</h4>
<ul>
<li><strong>cost</strong>: The current cost of the ad set.</li>
<li><strong>performance_status</strong>: The performance status indicators for the ad set.</li>
<li><strong>budget_increase_percentage</strong>: The percentage increase to suggest if the ad set is performing well.</li>
</ul>
<h4 id="returns-14">Returns</h4>
<ul>
<li><strong>str</strong>: The suggested budget increase formatted in Indian Rupees, or “N/A” if not applicable.</li>
</ul>
<h3 id="format_inramount"><code>format_inr(amount)</code></h3>
<p>Formats a numeric amount into a string representation of Indian Rupees.</p>
<h4 id="parameters-14">Parameters</h4>
<ul>
<li><strong>amount</strong>: The numeric amount to format.</li>
</ul>
<h4 id="returns-15">Returns</h4>
<ul>
<li><strong>str</strong>: Formatted amount as a string in Indian Rupees (INR).</li>
</ul>
<h3 id="adgroup-performance-analysis"><strong>9. AdGroup Performance Analysis</strong></h3>
<h4 id="overview-2">Overview</h4>
<p>The <code>AdGroupPerformanceAnalysisView</code> is a Django REST API view that allows users to analyze the performance of Google Ads ad groups over a specified period. The view retrieves various performance metrics such as clicks, impressions, cost, conversions, and conversion value from the Google Ads API.</p>
<h4 id="methods-4">Methods</h4>
<h5 id="postrequest"><code>post(request)</code></h5>
<p>Handles POST requests to retrieve ad group performance metrics based on the specified number of days.</p>
<ul>
<li>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>request</code>: The request object containing the following data:
<ul>
<li><code>days_to_analyze</code> (optional, int): Number of days to analyze. Defaults to 30 if not provided.</li>
</ul>
</li>
</ul>
</li>
<li>
<p><strong>Returns:</strong></p>
<ul>
<li><code>Response</code>: A JSON response containing:
<ul>
<li>On success (HTTP 200 OK):
<ul>
<li><code>data</code>: A list of performance metrics for ad groups.</li>
<li><code>analysis_parameters</code>:
<ul>
<li><code>customer_id</code>: The Google Ads customer ID.</li>
<li><code>days_analyzed</code>: The number of days analyzed.</li>
</ul>
</li>
</ul>
</li>
<li>On failure (HTTP 404 NOT FOUND):
<ul>
<li><code>error</code>: A message indicating no data was retrieved from the Google Ads API.</li>
</ul>
</li>
<li>On unexpected errors (HTTP 500 INTERNAL SERVER ERROR):
<ul>
<li><code>error</code>: A message describing the error.</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
<li>
<p><strong>Exception Handling:</strong></p>
<ul>
<li>Logs any exceptions that occur during execution and returns an appropriate error response.</li>
</ul>
</li>
</ul>
<h5 id="get_ad_group_performanceclient-customer_id-days_ago"><code>get_ad_group_performance(client, customer_id, days_ago)</code></h5>
<p>Fetches ad group performance metrics from the Google Ads API.</p>
<ul>
<li>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>client</code>: The Google Ads API client instance.</li>
<li><code>customer_id</code>: The Google Ads customer ID (string).</li>
<li><code>days_ago</code>: The number of days to analyze (int).</li>
</ul>
</li>
<li>
<p><strong>Returns:</strong></p>
<ul>
<li><code>pd.DataFrame</code>: A DataFrame containing the ad group performance metrics. Returns an empty DataFrame if no data is found.</li>
</ul>
</li>
<li>
<p><strong>Exception Handling:</strong></p>
<ul>
<li>Logs and raises exceptions specific to Google Ads and any unexpected errors.</li>
</ul>
</li>
</ul>
<h5 id="build_ad_group_performance_querydays_ago"><code>build_ad_group_performance_query(days_ago)</code></h5>
<p>Constructs a Google Ads query to retrieve ad group performance metrics for a specified number of days.</p>
<ul>
<li>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>days_ago</code>: The number of days to analyze (int).</li>
</ul>
</li>
<li>
<p><strong>Returns:</strong></p>
<ul>
<li><code>str</code>: A formatted query string to be used with the Google Ads API.</li>
</ul>
</li>
</ul>
<h5 id="process_ad_group_performance_responseresponse"><code>process_ad_group_performance_response(response)</code></h5>
<p>Processes the response from the Google Ads API to extract ad group performance data.</p>
<ul>
<li>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>response</code>: The response object returned by the Google Ads API.</li>
</ul>
</li>
<li>
<p><strong>Returns:</strong></p>
<ul>
<li><code>list</code>: A list of dictionaries containing performance data for each ad group.</li>
</ul>
</li>
</ul>
<h5 id="log_google_ads_exceptionex"><code>log_google_ads_exception(ex)</code></h5>
<p>Logs details of any Google Ads API exceptions encountered.</p>
<ul>
<li>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>ex</code>: The GoogleAdsException instance.</li>
</ul>
</li>
<li>
<p><strong>Returns:</strong></p>
<ul>
<li>None</li>
</ul>
</li>
</ul>
<h4 id="exception-handling">Exception Handling</h4>
<ul>
<li>The view handles exceptions that may occur during the API call, including:
<ul>
<li><strong>GoogleAdsException</strong>: Specific errors returned by the Google Ads API are logged, and relevant messages are included in the response.</li>
<li><strong>General Exceptions</strong>: Any other errors that occur during execution are logged, and a generic error message is returned.</li>
</ul>
</li>
</ul>
<h4 id="logging">Logging</h4>
<ul>
<li>The view employs logging at various points to track the flow of execution and capture any errors that arise. This includes logging the start of data retrieval, any attribute errors during data processing, and detailed information about Google Ads exceptions.</li>
</ul>
<h3 id="example-request">Example Request</h3>
<pre class=" language-http"><code class="prism  language-http">POST /ad_group_performance
<span class="token header-name keyword">Content-Type:</span> application/json<span class="token application/json">

<span class="token punctuation">{</span>
  <span class="token string">"days_to_analyze"</span><span class="token punctuation">:</span> <span class="token number">30</span>
<span class="token punctuation">}</span>
</span></code></pre>
<h3 id="example-response-2">Example Response</h3>
<p><strong>Success Response (200 OK):</strong></p>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
  <span class="token string">"data"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
    <span class="token punctuation">{</span>
      <span class="token string">"date"</span><span class="token punctuation">:</span> <span class="token string">"2024-10-01"</span><span class="token punctuation">,</span>
      <span class="token string">"campaign_id"</span><span class="token punctuation">:</span> <span class="token string">"123456"</span><span class="token punctuation">,</span>
      <span class="token string">"campaign_name"</span><span class="token punctuation">:</span> <span class="token string">"Fall Sale"</span><span class="token punctuation">,</span>
      <span class="token string">"ad_group_id"</span><span class="token punctuation">:</span> <span class="token string">"654321"</span><span class="token punctuation">,</span>
      <span class="token string">"ad_group_name"</span><span class="token punctuation">:</span> <span class="token string">"Ad Group 1"</span><span class="token punctuation">,</span>
      <span class="token string">"ad_group_status"</span><span class="token punctuation">:</span> <span class="token string">"ENABLED"</span><span class="token punctuation">,</span>
      <span class="token string">"clicks"</span><span class="token punctuation">:</span> <span class="token number">150</span><span class="token punctuation">,</span>
      <span class="token string">"impressions"</span><span class="token punctuation">:</span> <span class="token number">2000</span><span class="token punctuation">,</span>
      <span class="token string">"cost_micros"</span><span class="token punctuation">:</span> <span class="token number">5000000</span><span class="token punctuation">,</span>
      <span class="token string">"conversions"</span><span class="token punctuation">:</span> <span class="token number">25</span><span class="token punctuation">,</span>
      <span class="token string">"conversions_value"</span><span class="token punctuation">:</span> <span class="token number">1000</span>
    <span class="token punctuation">}</span>
    <span class="token comment">// More records...</span>
  <span class="token punctuation">]</span><span class="token punctuation">,</span>
  <span class="token string">"analysis_parameters"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>
    <span class="token string">"customer_id"</span><span class="token punctuation">:</span> <span class="token string">"customer123"</span><span class="token punctuation">,</span>
    <span class="token string">"days_analyzed"</span><span class="token punctuation">:</span> <span class="token number">30</span>
  <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<p><strong>Error Response (404 NOT FOUND):</strong></p>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
  <span class="token string">"error"</span><span class="token punctuation">:</span> <span class="token string">"No data retrieved from Google Ads API"</span>
<span class="token punctuation">}</span>
</code></pre>
<p><strong>Error Response (500 INTERNAL SERVER ERROR):</strong></p>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
  <span class="token string">"error"</span><span class="token punctuation">:</span> <span class="token string">"An error occurred: [error message]"</span>
<span class="token punctuation">}</span>
</code></pre>
<p>Here’s the requested documentation for the <code>AdManagementView</code> class, following the same structure as the previous documentation provided:</p>
<hr>
<h3 id="admanagementview-documentation"><strong>10.AdManagementView Documentation</strong></h3>
<h4 id="overview-3">Overview</h4>
<p>The <code>AdManagementView</code> is a Django REST API view that allows users to manage Google Ads campaigns and ad groups. It supports actions such as pausing ad groups, adjusting campaign budgets, adjusting ad group budgets, and adjusting campaign bids.</p>
<h4 id="methods-5">Methods</h4>
<h5 id="postrequest-1"><code>post(request)</code></h5>
<p>Handles POST requests to manage ad groups and campaigns based on the specified action.</p>
<ul>
<li>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>request</code>: The request object containing the following data:
<ul>
<li><code>action</code> (string): The action to be performed. Possible values include:
<ul>
<li><code>pause_ad_groups</code>: Pauses specified ad groups.</li>
<li><code>increase_campaign_budgets</code>: Increases specified campaign budgets.</li>
<li><code>decrease_campaign_budgets</code>: Decreases specified campaign budgets.</li>
<li><code>increase_ad_group_budgets</code>: Increases specified ad group budgets.</li>
<li><code>decrease_ad_group_budgets</code>: Decreases specified ad group budgets.</li>
<li><code>increase_campaign_bids</code>: Increases specified campaign bids.</li>
<li><code>decrease_campaign_bids</code>: Decreases specified campaign bids.</li>
</ul>
</li>
<li>Depending on the action, additional parameters may include:
<ul>
<li><code>ad_group_ids</code>: List of ad group IDs to be paused.</li>
<li><code>campaign_budgets</code>: List of dictionaries containing campaign IDs and budget adjustments.</li>
<li><code>ad_group_budgets</code>: List of dictionaries containing ad group IDs and budget adjustments.</li>
<li><code>campaign_bids</code>: List of dictionaries containing campaign IDs, criterion IDs, and bid adjustments.</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
<li>
<p><strong>Returns:</strong></p>
<ul>
<li><code>Response</code>: A JSON response containing:
<ul>
<li>On success (HTTP 200 OK):
<ul>
<li><code>message</code>: A success message indicating the action taken.</li>
</ul>
</li>
<li>On failure (HTTP 400 BAD REQUEST):
<ul>
<li><code>error</code>: A message indicating the action was invalid or no action was specified.</li>
</ul>
</li>
<li>On Google Ads API errors (HTTP 500 INTERNAL SERVER ERROR):
<ul>
<li><code>error</code>: A message describing the Google Ads API error.</li>
</ul>
</li>
<li>On unexpected errors (HTTP 500 INTERNAL SERVER ERROR):
<ul>
<li><code>error</code>: A message describing the unexpected error.</li>
</ul>
</li>
</ul>
</li>
</ul>
</li>
<li>
<p><strong>Exception Handling:</strong></p>
<ul>
<li>Logs any exceptions that occur during execution and returns an appropriate error response.</li>
</ul>
</li>
</ul>
<h5 id="pause_ad_groupsclient-customer_id-ad_group_ids"><code>pause_ad_groups(client, customer_id, ad_group_ids)</code></h5>
<p>Pauses the specified ad groups.</p>
<ul>
<li>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>client</code>: The Google Ads API client instance.</li>
<li><code>customer_id</code>: The Google Ads customer ID (string).</li>
<li><code>ad_group_ids</code>: List of ad group IDs to pause.</li>
</ul>
</li>
<li>
<p><strong>Returns:</strong></p>
<ul>
<li>None</li>
</ul>
</li>
</ul>
<h5 id="create_pause_ad_group_operationsclient-ad_group_ids"><code>create_pause_ad_group_operations(client, ad_group_ids)</code></h5>
<p>Creates operations to pause specified ad groups.</p>
<ul>
<li>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>client</code>: The Google Ads API client instance.</li>
<li><code>ad_group_ids</code>: List of ad group IDs to pause.</li>
</ul>
</li>
<li>
<p><strong>Returns:</strong></p>
<ul>
<li><code>list</code>: A list of <code>AdGroupOperation</code> instances for the ad groups to be paused.</li>
</ul>
</li>
</ul>
<h5 id="adjust_campaign_budgetsclient-customer_id-campaign_budgets-action"><code>adjust_campaign_budgets(client, customer_id, campaign_budgets, action)</code></h5>
<p>Adjusts the budgets of specified campaigns based on the action.</p>
<ul>
<li>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>client</code>: The Google Ads API client instance.</li>
<li><code>customer_id</code>: The Google Ads customer ID (string).</li>
<li><code>campaign_budgets</code>: List of dictionaries containing campaign IDs and budget adjustments.</li>
<li><code>action</code>: The action to perform, either <code>increase_campaign_budgets</code> or <code>decrease_campaign_budgets</code>.</li>
</ul>
</li>
<li>
<p><strong>Returns:</strong></p>
<ul>
<li>None</li>
</ul>
</li>
</ul>
<h5 id="create_campaign_budget_operationsclient-campaign_budgets-action"><code>create_campaign_budget_operations(client, campaign_budgets, action)</code></h5>
<p>Creates operations to adjust the budgets of specified campaigns.</p>
<ul>
<li>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>client</code>: The Google Ads API client instance.</li>
<li><code>campaign_budgets</code>: List of dictionaries containing campaign IDs and budget adjustments.</li>
<li><code>action</code>: The action to perform, either <code>increase_campaign_budgets</code> or <code>decrease_campaign_budgets</code>.</li>
</ul>
</li>
<li>
<p><strong>Returns:</strong></p>
<ul>
<li><code>list</code>: A list of <code>CampaignOperation</code> instances for the campaigns to be adjusted.</li>
</ul>
</li>
</ul>
<h5 id="adjust_ad_group_budgetsclient-customer_id-ad_group_budgets-action"><code>adjust_ad_group_budgets(client, customer_id, ad_group_budgets, action)</code></h5>
<p>Adjusts the budgets of specified ad groups based on the action.</p>
<ul>
<li>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>client</code>: The Google Ads API client instance.</li>
<li><code>customer_id</code>: The Google Ads customer ID (string).</li>
<li><code>ad_group_budgets</code>: List of dictionaries containing ad group IDs and budget adjustments.</li>
<li><code>action</code>: The action to perform, either <code>increase_ad_group_budgets</code> or <code>decrease_ad_group_budgets</code>.</li>
</ul>
</li>
<li>
<p><strong>Returns:</strong></p>
<ul>
<li>None</li>
</ul>
</li>
</ul>
<h5 id="create_ad_group_budget_operationsclient-ad_group_budgets-action"><code>create_ad_group_budget_operations(client, ad_group_budgets, action)</code></h5>
<p>Creates operations to adjust the budgets of specified ad groups.</p>
<ul>
<li>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>client</code>: The Google Ads API client instance.</li>
<li><code>ad_group_budgets</code>: List of dictionaries containing ad group IDs and budget adjustments.</li>
<li><code>action</code>: The action to perform, either <code>increase_ad_group_budgets</code> or <code>decrease_ad_group_budgets</code>.</li>
</ul>
</li>
<li>
<p><strong>Returns:</strong></p>
<ul>
<li><code>list</code>: A list of <code>AdGroupOperation</code> instances for the ad groups to be adjusted.</li>
</ul>
</li>
</ul>
<h5 id="adjust_campaign_bidsclient-customer_id-campaign_bids-action"><code>adjust_campaign_bids(client, customer_id, campaign_bids, action)</code></h5>
<p>Adjusts the bids of specified campaigns based on the action.</p>
<ul>
<li>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>client</code>: The Google Ads API client instance.</li>
<li><code>customer_id</code>: The Google Ads customer ID (string).</li>
<li><code>campaign_bids</code>: List of dictionaries containing campaign IDs, criterion IDs, and bid adjustments.</li>
<li><code>action</code>: The action to perform, either <code>increase_campaign_bids</code> or <code>decrease_campaign_bids</code>.</li>
</ul>
</li>
<li>
<p><strong>Returns:</strong></p>
<ul>
<li>None</li>
</ul>
</li>
</ul>
<h5 id="create_campaign_bid_operationsclient-campaign_bids-action"><code>create_campaign_bid_operations(client, campaign_bids, action)</code></h5>
<p>Creates operations to adjust the bids of specified campaigns.</p>
<ul>
<li>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>client</code>: The Google Ads API client instance.</li>
<li><code>campaign_bids</code>: List of dictionaries containing campaign IDs, criterion IDs, and bid adjustments.</li>
<li><code>action</code>: The action to perform, either <code>increase_campaign_bids</code> or <code>decrease_campaign_bids</code>.</li>
</ul>
</li>
<li>
<p><strong>Returns:</strong></p>
<ul>
<li><code>list</code>: A list of <code>CampaignCriterionOperation</code> instances for the campaigns to be adjusted.</li>
</ul>
</li>
</ul>
<h4 id="exception-handling-1">Exception Handling</h4>
<ul>
<li>The view handles exceptions that may occur during the API calls, including:
<ul>
<li><strong>GoogleAdsException</strong>: Specific errors returned by the Google Ads API are logged, and relevant messages are included in the response.</li>
<li><strong>General Exceptions</strong>: Any other errors that occur during execution are logged, and a generic error message is returned.</li>
</ul>
</li>
</ul>
<h4 id="logging-1">Logging</h4>
<ul>
<li>The view employs logging at various points to track the flow of execution and capture any errors that arise. This includes logging the start of each action, details of the actions performed, and detailed information about Google Ads exceptions.</li>
</ul>
<h3 id="example-request-1">Example Request</h3>
<pre class=" language-http"><code class="prism  language-http">POST /ad_management
<span class="token header-name keyword">Content-Type:</span> application/json<span class="token application/json">

<span class="token punctuation">{</span>
  <span class="token string">"action"</span><span class="token punctuation">:</span> <span class="token string">"pause_ad_groups"</span><span class="token punctuation">,</span>
  <span class="token string">"ad_group_ids"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token string">"123456"</span><span class="token punctuation">,</span> <span class="token string">"789012"</span><span class="token punctuation">]</span>
<span class="token punctuation">}</span>
</span></code></pre>
<h3 id="example-response-3">Example Response</h3>
<p><strong>Success Response (200 OK):</strong></p>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
  <span class="token string">"message"</span><span class="token punctuation">:</span> <span class="token string">"Ad groups paused successfully"</span>
<span class="token punctuation">}</span>
</code></pre>
<p><strong>Error Response (400 BAD REQUEST):</strong></p>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
  <span class="token string">"error"</span><span class="token punctuation">:</span> <span class="token string">"Invalid action specified"</span>
<span class="token punctuation">}</span>
</code></pre>
<p><strong>Error Response (500 INTERNAL SERVER ERROR):</strong></p>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
  <span class="token string">"error"</span><span class="token punctuation">:</span> <span class="token string">"Google Ads API error: [error code name]"</span>
<span class="token punctuation">}</span>
</code></pre>
<p>Here’s the documentation for the <code>FunnelAnalysis</code> class that describes its purpose, methods, parameters, return types, and error handling in a similar style to the provided documentation:</p>
<hr>
<h2 id="funnelanalysis-class"><strong>11.FunnelAnalysis Class</strong></h2>
<p><strong>Purpose</strong>:<br>
The <code>FunnelAnalysis</code> class provides an API endpoint to analyze advertising funnel data using the Google Ads API. It retrieves performance metrics over a specified date range and processes this data to generate insights.</p>
<h4 id="methods-6">Methods</h4>
<h5 id="getrequest"><code>get(request)</code></h5>
<p>Handles GET requests to retrieve funnel analysis data.</p>
<ul>
<li>
<p><strong>Parameters</strong>:</p>
<ul>
<li><code>request</code> (Request): The HTTP request object containing the user’s request data.</li>
</ul>
</li>
<li>
<p><strong>Returns</strong>:</p>
<ul>
<li><code>Response</code>: A JSON response containing:
<ul>
<li><code>overall_summary</code>: An object summarizing total performance metrics across all campaigns.</li>
<li><code>day_wise_summary</code>: An array of objects with daily performance metrics.</li>
<li><code>campaign_summary</code>: An array of objects summarizing performance metrics for each campaign.</li>
</ul>
</li>
</ul>
</li>
<li>
<p><strong>Raises</strong>:</p>
<ul>
<li><code>Exception</code>: Catches and logs any unexpected errors during the data fetching or processing phases. Returns a JSON response with an error message and a 500 status code if data retrieval fails.</li>
</ul>
</li>
</ul>
<h4 id="private-methods">Private Methods</h4>
<h5 id="fetch_funnel_dataclient-customer_id-start_date-end_date"><code>fetch_funnel_data(client, customer_id, start_date, end_date)</code></h5>
<p>Fetches funnel data from Google Ads API for the specified date range.</p>
<ul>
<li>
<p><strong>Parameters</strong>:</p>
<ul>
<li><code>client</code> (GoogleAdsClient): The Google Ads client instance used to interact with the API.</li>
<li><code>customer_id</code> (str): The ID of the Google Ads customer account.</li>
<li><code>start_date</code> (date): The start date for the data retrieval.</li>
<li><code>end_date</code> (date): The end date for the data retrieval.</li>
</ul>
</li>
<li>
<p><strong>Returns</strong>:</p>
<ul>
<li><code>list</code>: A list of fetched campaign data rows, or <code>None</code> if an error occurs.</li>
</ul>
</li>
<li>
<p><strong>Raises</strong>:</p>
<ul>
<li><code>Exception</code>: Catches and logs errors encountered while fetching data from the API.</li>
</ul>
</li>
</ul>
<h5 id="process_funnel_datadata"><code>process_funnel_data(data)</code></h5>
<p>Processes the fetched funnel data into a pandas DataFrame.</p>
<ul>
<li>
<p><strong>Parameters</strong>:</p>
<ul>
<li><code>data</code> (list): The list of campaign data rows fetched from Google Ads API.</li>
</ul>
</li>
<li>
<p><strong>Returns</strong>:</p>
<ul>
<li><code>DataFrame</code>: A DataFrame containing structured funnel data with columns for date, campaign name, impressions, clicks, cost, conversions, and conversion value.</li>
</ul>
</li>
</ul>
<h5 id="calculate_overall_summarydf"><code>calculate_overall_summary(df)</code></h5>
<p>Calculates overall summary metrics from the funnel data.</p>
<ul>
<li>
<p><strong>Parameters</strong>:</p>
<ul>
<li><code>df</code> (DataFrame): The DataFrame containing processed funnel data.</li>
</ul>
</li>
<li>
<p><strong>Returns</strong>:</p>
<ul>
<li><code>dict</code>: A dictionary containing overall performance metrics including:
<ul>
<li>Impressions</li>
<li>Clicks</li>
<li>Cost</li>
<li>Conversions</li>
<li>Conversion Value</li>
<li>CTR (Click-Through Rate)</li>
<li>CPC (Cost Per Click)</li>
<li>Conversion Rate</li>
<li>CPA (Cost Per Acquisition)</li>
<li>ROAS (Return On Ad Spend)</li>
</ul>
</li>
</ul>
</li>
</ul>
<h5 id="calculate_day_wise_summarydf"><code>calculate_day_wise_summary(df)</code></h5>
<p>Calculates daily summary metrics from the funnel data.</p>
<ul>
<li>
<p><strong>Parameters</strong>:</p>
<ul>
<li><code>df</code> (DataFrame): The DataFrame containing processed funnel data.</li>
</ul>
</li>
<li>
<p><strong>Returns</strong>:</p>
<ul>
<li><code>list</code>: An array of dictionaries, each containing daily performance metrics.</li>
</ul>
</li>
</ul>
<h5 id="calculate_campaign_summarydf"><code>calculate_campaign_summary(df)</code></h5>
<p>Calculates summary metrics for each campaign from the funnel data.</p>
<ul>
<li>
<p><strong>Parameters</strong>:</p>
<ul>
<li><code>df</code> (DataFrame): The DataFrame containing processed funnel data.</li>
</ul>
</li>
<li>
<p><strong>Returns</strong>:</p>
<ul>
<li><code>list</code>: An array of dictionaries, each containing performance metrics for individual campaigns.</li>
</ul>
</li>
</ul>
<h5 id="safe_divisionnumerator-denominator"><code>safe_division(numerator, denominator)</code></h5>
<p>Performs safe division, avoiding division by zero.</p>
<ul>
<li>
<p><strong>Parameters</strong>:</p>
<ul>
<li><code>numerator</code> (float): The numerator value for the division.</li>
<li><code>denominator</code> (float): The denominator value for the division.</li>
</ul>
</li>
<li>
<p><strong>Returns</strong>:</p>
<ul>
<li><code>float</code>: The result of the division or <code>0</code> if the denominator is zero.</li>
</ul>
</li>
</ul>
<h3 id="error-handling-6">Error Handling</h3>
<p>The class employs robust error handling by logging any exceptions that occur during data fetching and processing. If any errors arise, an appropriate error message is returned in the API response, and a <code>500 Internal Server Error</code> status is provided.</p>
<p>Here’s a structured documentation outline for the <code>AdCopyInsights</code> class in your Django REST framework project. This documentation includes details about the class, its methods, and their functionality, similar to the provided example.</p>
<hr>
<h2 id="ad-copyinsights"><strong>12. Ad CopyInsights</strong></h2>
<h2 id="overview-4">Overview</h2>
<p>The <code>Ad CopyInsights</code> class is an API view that retrieves and processes ad copy performance metrics from the Google Ads API. It provides insights on ad length metrics, emoji performance, link performance, sentiment performance, and the top emojis and links used in ad copy.</p>
<h2 id="inheritance">Inheritance</h2>
<ul>
<li>Inherits from <code>APIView</code> and <code>GoogleAdsClientMixin</code>.</li>
</ul>
<h2 id="methods-7">Methods</h2>
<h3 id="getself-request-4"><code>get(self, request)</code></h3>
<p>Handles GET requests to fetch ad copy insights. This method orchestrates the fetching, processing, and calculation of various ad copy performance metrics.</p>
<h4 id="parameters-15">Parameters</h4>
<ul>
<li><code>request</code>: The HTTP request object.</li>
</ul>
<h4 id="returns-16">Returns</h4>
<ul>
<li><code>Response</code>: A JSON response containing the calculated performance metrics or an error message if data retrieval fails.</li>
</ul>
<h4 id="error-handling-7">Error Handling</h4>
<ul>
<li>Returns a 500 HTTP status code with an error message if data fetching from the Google Ads API fails or if an exception occurs during processing.</li>
</ul>
<h3 id="calculate_ad_length_metricsdf"><code>calculate_ad_length_metrics(df)</code></h3>
<p>Calculates metrics based on the length of ad copies.</p>
<h4 id="parameters-16">Parameters</h4>
<ul>
<li><code>df</code>: A DataFrame containing ad copy data.</li>
</ul>
<h4 id="returns-17">Returns</h4>
<ul>
<li><code>list</code>: A list of dictionaries, each containing:
<ul>
<li><code>length_category</code>: The category of ad length.</li>
<li><code>number_of_ads</code>: The count of ads in this category.</li>
<li><code>impressions</code>: Total impressions for this category.</li>
<li><code>clicks</code>: Total clicks for this category.</li>
<li><code>cost</code>: Total cost incurred for this category.</li>
<li><code>revenue</code>: Total revenue generated from this category.</li>
<li><code>ctr</code>: Click-through rate, calculated as <code>(clicks / impressions) * 100</code>.</li>
<li><code>cpc</code>: Cost per click, calculated as <code>(cost / clicks)</code>.</li>
<li><code>conversion_rate</code>: Conversion rate, calculated as <code>(revenue / cost) * 100</code>.</li>
</ul>
</li>
</ul>
<h3 id="calculate_emoji_performancedf"><code>calculate_emoji_performance(df)</code></h3>
<p>Analyzes the performance of emojis used in ad copies.</p>
<h4 id="parameters-17">Parameters</h4>
<ul>
<li><code>df</code>: A DataFrame containing ad copy data.</li>
</ul>
<h4 id="returns-18">Returns</h4>
<ul>
<li><code>list</code>: A list of dictionaries, each containing:
<ul>
<li><code>emoji_count_category</code>: The category based on the number of emojis used.</li>
<li><code>number_of_ads</code>: The count of ads in this category.</li>
<li><code>revenue</code>: Total revenue generated from this category.</li>
<li><code>cost</code>: Total cost incurred for this category.</li>
<li><code>impressions</code>: Total impressions for this category.</li>
<li><code>clicks</code>: Total clicks for this category.</li>
<li><code>revenue_percentage</code>: Percentage of total revenue.</li>
<li><code>cost_percentage</code>: Percentage of total cost.</li>
<li><code>ctr</code>: Click-through rate.</li>
<li><code>conversion_rate</code>: Conversion rate.</li>
</ul>
</li>
</ul>
<h3 id="calculate_link_performancedf"><code>calculate_link_performance(df)</code></h3>
<p>Evaluates the performance of ads based on the presence of links in the final URLs.</p>
<h4 id="parameters-18">Parameters</h4>
<ul>
<li><code>df</code>: A DataFrame containing ad copy data.</li>
</ul>
<h4 id="returns-19">Returns</h4>
<ul>
<li><code>list</code>: A list of dictionaries containing:
<ul>
<li><code>has_link</code>: Boolean indicating if links are present.</li>
<li><code>number_of_ads</code>: The count of ads in this category.</li>
<li><code>revenue</code>: Total revenue generated from this category.</li>
<li><code>cost</code>: Total cost incurred for this category.</li>
<li><code>impressions</code>: Total impressions for this category.</li>
<li><code>clicks</code>: Total clicks for this category.</li>
<li><code>revenue_percentage</code>: Percentage of total revenue.</li>
<li><code>cost_percentage</code>: Percentage of total cost.</li>
<li><code>ctr</code>: Click-through rate.</li>
<li><code>conversion_rate</code>: Conversion rate.</li>
</ul>
</li>
</ul>
<h3 id="calculate_sentiment_performancedf"><code>calculate_sentiment_performance(df)</code></h3>
<p>Assesses the performance of ads based on sentiment analysis.</p>
<h4 id="parameters-19">Parameters</h4>
<ul>
<li><code>df</code>: A DataFrame containing ad copy data.</li>
</ul>
<h4 id="returns-20">Returns</h4>
<ul>
<li><code>list</code>: A list of dictionaries, each containing:
<ul>
<li><code>sentiment</code>: The sentiment category of the ad.</li>
<li><code>number_of_ads</code>: The count of ads in this sentiment category.</li>
<li><code>revenue</code>: Total revenue generated.</li>
<li><code>cost</code>: Total cost incurred.</li>
<li><code>impressions</code>: Total impressions.</li>
<li><code>clicks</code>: Total clicks.</li>
<li><code>sentiment_score</code>: Average sentiment score.</li>
<li><code>revenue_percentage</code>: Percentage of total revenue.</li>
<li><code>cost_percentage</code>: Percentage of total cost.</li>
<li><code>ctr</code>: Click-through rate.</li>
<li><code>conversion_rate</code>: Conversion rate.</li>
</ul>
</li>
</ul>
<h3 id="get_top_emojisdf"><code>get_top_emojis(df)</code></h3>
<p>Identifies the top-performing emojis in ad copies.</p>
<h4 id="parameters-20">Parameters</h4>
<ul>
<li><code>df</code>: A DataFrame containing ad copy data.</li>
</ul>
<h4 id="returns-21">Returns</h4>
<ul>
<li><code>list</code>: A list of dictionaries for the top emojis, each containing:
<ul>
<li><code>emoji</code>: The emoji character.</li>
<li><code>count</code>: Number of occurrences of the emoji.</li>
<li><code>revenue</code>: Total revenue generated with this emoji.</li>
<li><code>cost</code>: Total cost incurred with this emoji.</li>
<li><code>impressions</code>: Total impressions for ads containing this emoji.</li>
<li><code>clicks</code>: Total clicks for ads containing this emoji.</li>
<li><code>number_of_ads</code>: The count of ads using this emoji.</li>
<li><code>ctr</code>: Click-through rate.</li>
<li><code>conversion_rate</code>: Conversion rate.</li>
</ul>
</li>
</ul>
<h3 id="get_top_linksdf"><code>get_top_links(df)</code></h3>
<p>Identifies the top-performing links in ad copies.</p>
<h4 id="parameters-21">Parameters</h4>
<ul>
<li><code>df</code>: A DataFrame containing ad copy data.</li>
</ul>
<h4 id="returns-22">Returns</h4>
<ul>
<li><code>list</code>: A list of dictionaries for the top links, each containing:
<ul>
<li><code>link</code>: The URL of the link.</li>
<li><code>count</code>: Number of occurrences of the link.</li>
<li><code>revenue</code>: Total revenue generated from ads containing this link.</li>
<li><code>cost</code>: Total cost incurred from ads containing this link.</li>
<li><code>impressions</code>: Total impressions for ads containing this link.</li>
<li><code>clicks</code>: Total clicks for ads containing this link.</li>
<li><code>number_of_ads</code>: The count of ads using this link.</li>
<li><code>ctr</code>: Click-through rate.</li>
<li><code>conversion_rate</code>: Conversion rate.</li>
</ul>
</li>
</ul>
<h3 id="replace_nan_with_noneobj"><code>replace_nan_with_none(obj)</code></h3>
<p>Recursively replaces NaN and infinite values with <code>None</code>.</p>
<h4 id="parameters-22">Parameters</h4>
<ul>
<li><code>obj</code>: The object to be processed (can be a dict, list, float, etc.).</li>
</ul>
<h4 id="returns-23">Returns</h4>
<ul>
<li>The input object with NaN and infinite values replaced with <code>None</code>.</li>
</ul>
<h2 id="overspending-ads-1"><strong>13. Overspending Ads</strong></h2>
<p>This view analyzes the performance of Google Ads campaigns and ad groups to identify overspending issues. It provides recommendations based on specified performance thresholds.</p>
<h3 id="methods-8">Methods</h3>
<h4 id="getself-request-5"><code>get(self, request)</code></h4>
<ul>
<li><strong>Description</strong>: Handles GET requests to analyze campaign and ad group performance.</li>
<li><strong>Parameters</strong>:
<ul>
<li><code>target_cpa</code> (float, optional): Target Cost Per Acquisition (CPA). Defaults to 3500.</li>
<li><code>cost_threshold</code> (float, optional): Threshold for maximum allowable cost. Defaults to 7000.</li>
<li><code>ctr_threshold</code> (float, optional): Threshold for Click-Through Rate (CTR). Defaults to 1.0.</li>
</ul>
</li>
<li><strong>Returns</strong>: A JSON response containing:
<ul>
<li><code>campaign_recommendations</code>: List of recommendations for campaigns.</li>
<li><code>adgroup_recommendations</code>: List of recommendations for ad groups.</li>
<li><code>parameters</code>: The parameters used for analysis.</li>
</ul>
</li>
<li><strong>Error Handling</strong>:
<ul>
<li><code>GoogleAdsException</code>: Logs and returns a 500 error with the Google Ads API error message.</li>
<li><code>Timeout</code>: Returns a 504 error if the request times out.</li>
<li>General exceptions: Logs the error and returns a 500 error.</li>
</ul>
</li>
</ul>
<h4 id="get_google_ads_clientself-4"><code>get_google_ads_client(self)</code></h4>
<ul>
<li><strong>Description</strong>: Loads and returns a Google Ads client using the configuration specified in the settings.</li>
<li><strong>Returns</strong>: An instance of <code>GoogleAdsClient</code>.</li>
</ul>
<h4 id="analyze_performanceself-client-customer_id-target_cpa-cost_threshold-ctr_threshold-1"><code>analyze_performance(self, client, customer_id, target_cpa, cost_threshold, ctr_threshold)</code></h4>
<ul>
<li><strong>Description</strong>: Analyzes campaign and ad group performance over the last 30 days based on the provided parameters.</li>
<li><strong>Parameters</strong>:
<ul>
<li><code>client</code>: The Google Ads client instance.</li>
<li><code>customer_id</code>: The Google Ads customer ID.</li>
<li><code>target_cpa</code>: Target CPA for analysis.</li>
<li><code>cost_threshold</code>: Maximum cost threshold.</li>
<li><code>ctr_threshold</code>: Minimum CTR threshold.</li>
</ul>
</li>
<li><strong>Returns</strong>: A tuple containing:
<ul>
<li><code>campaign_recommendations</code>: List of campaign recommendations.</li>
<li><code>adgroup_recommendations</code>: List of ad group recommendations.</li>
</ul>
</li>
</ul>
<h4 id="analyze_entityself-row-entity_type-target_cpa-cost_threshold-ctr_threshold-1"><code>analyze_entity(self, row, entity_type, target_cpa, cost_threshold, ctr_threshold)</code></h4>
<ul>
<li><strong>Description</strong>: Analyzes a single campaign or ad group entity and identifies issues based on performance metrics.</li>
<li><strong>Parameters</strong>:
<ul>
<li><code>row</code>: The row of data representing the entity.</li>
<li><code>entity_type</code>: Type of entity (‘campaign’ or ‘ad_group’).</li>
<li><code>target_cpa</code>, <code>cost_threshold</code>, <code>ctr_threshold</code>: Threshold values for analysis.</li>
</ul>
</li>
<li><strong>Returns</strong>: A dictionary containing identified issues, recommendations, and performance metrics, or <code>None</code> if no issues are found.</li>
</ul>
<h4 id="get_ai_recommendations_with_fallbackself-entity_type-campaign_type-issues-metrics-1"><code>get_ai_recommendations_with_fallback(self, entity_type, campaign_type, issues, metrics)</code></h4>
<ul>
<li><strong>Description</strong>: Obtains AI-generated recommendations with a fallback to basic recommendations in case of failure.</li>
<li><strong>Parameters</strong>:
<ul>
<li><code>entity_type</code>: Type of entity (‘campaign’ or ‘ad_group’).</li>
<li><code>campaign_type</code>: Type of campaign.</li>
<li><code>issues</code>: List of identified issues.</li>
<li><code>metrics</code>: Dictionary of performance metrics.</li>
</ul>
</li>
<li><strong>Returns</strong>: A list of recommendations.</li>
</ul>
<h4 id="get_ai_recommendationsself-entity_type-campaign_type-issues-metrics-1"><code>get_ai_recommendations(self, entity_type, campaign_type, issues, metrics)</code></h4>
<ul>
<li><strong>Description</strong>: Sends a prompt to OpenAI’s API to receive recommendations for improving ad performance based on identified issues.</li>
<li><strong>Parameters</strong>: Same as <code>get_ai_recommendations_with_fallback</code>.</li>
<li><strong>Returns</strong>: A list of formatted AI-generated recommendations.</li>
</ul>
<h4 id="get_fallback_recommendationsself-entity_type-campaign_type-issues-1"><code>get_fallback_recommendations(self, entity_type, campaign_type, issues)</code></h4>
<ul>
<li><strong>Description</strong>: Provides basic, rule-based recommendations based on identified issues.</li>
<li><strong>Parameters</strong>: Same as <code>get_ai_recommendations_with_fallback</code>.</li>
<li><strong>Returns</strong>: A list of fallback recommendations.</li>
</ul>
<h4 id="format_ai_recommendationsself-ai_response-1"><code>format_ai_recommendations(self, ai_response)</code></h4>
<ul>
<li><strong>Description</strong>: Formats the AI response into a structured list of recommendations.</li>
<li><strong>Parameters</strong>:
<ul>
<li><code>ai_response</code>: Raw response string from the AI API.</li>
</ul>
</li>
<li><strong>Returns</strong>: A structured list of recommendations.</li>
</ul>
<h4 id="format_inrself-amount-2"><code>format_inr(self, amount)</code></h4>
<ul>
<li><strong>Description</strong>: Formats a given amount into Indian Rupees (INR).</li>
<li><strong>Parameters</strong>:
<ul>
<li><code>amount</code>: The numeric amount to format.</li>
</ul>
</li>
<li><strong>Returns</strong>: A string representation of the amount in INR.</li>
</ul>
<p>Here’s a structured documentation for the <code>StopLossAutomation1</code> class, detailing its purpose, methods, and usage. This format follows the standard conventions for API documentation.</p>
<hr>
<h2 id="stoplossautomation"><strong>14. StopLossAutomation</strong></h2>
<p>The <code>StopLossAutomation1</code> class is an API view designed for automating stop-loss strategies in Google Ads campaigns. It identifies underperforming ads based on specified budget and conversion thresholds and provides actionable suggestions to improve ad performance.</p>
<h3 id="post-stop-loss-automation">POST /stop-loss-automation/</h3>
<p><strong>Description</strong>: This method handles the incoming POST request to analyze ad performance and suggest improvements.</p>
<h4 id="request-body-1">Request Body</h4>
<p>The request body should contain the following fields:</p>

<table>
<thead>
<tr>
<th>Field</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>budget_threshold</code></td>
<td>float</td>
<td>The budget threshold in INR to determine underperforming ads.</td>
</tr>
<tr>
<td><code>conversion_threshold</code></td>
<td>int</td>
<td>The maximum number of conversions below which ads are considered underperforming.</td>
</tr>
</tbody>
</table><h4 id="response">Response</h4>
<ul>
<li><strong>200 OK</strong>: Returns a list of underperforming ads with suggestions for improvement.</li>
<li><strong>400 Bad Request</strong>: Returns validation errors or Google Ads errors.</li>
</ul>
<h4 id="example-request-2">Example Request</h4>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
  <span class="token string">"budget_threshold"</span><span class="token punctuation">:</span> <span class="token number">1000</span><span class="token punctuation">,</span>
  <span class="token string">"conversion_threshold"</span><span class="token punctuation">:</span> <span class="token number">5</span>
<span class="token punctuation">}</span>
</code></pre>
<h4 id="example-response-4">Example Response</h4>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">[</span>
  <span class="token punctuation">{</span>
    <span class="token string">"campaign_id"</span><span class="token punctuation">:</span> <span class="token string">"123456789"</span><span class="token punctuation">,</span>
    <span class="token string">"campaign_name"</span><span class="token punctuation">:</span> <span class="token string">"Campaign A"</span><span class="token punctuation">,</span>
    <span class="token string">"ad_group_id"</span><span class="token punctuation">:</span> <span class="token string">"987654321"</span><span class="token punctuation">,</span>
    <span class="token string">"ad_group_name"</span><span class="token punctuation">:</span> <span class="token string">"Ad Group 1"</span><span class="token punctuation">,</span>
    <span class="token string">"ad_id"</span><span class="token punctuation">:</span> <span class="token string">"54321"</span><span class="token punctuation">,</span>
    <span class="token string">"ad_name"</span><span class="token punctuation">:</span> <span class="token string">"Ad Title"</span><span class="token punctuation">,</span>
    <span class="token string">"cost_inr"</span><span class="token punctuation">:</span> <span class="token number">1200.00</span><span class="token punctuation">,</span>
    <span class="token string">"conversions"</span><span class="token punctuation">:</span> <span class="token number">3</span><span class="token punctuation">,</span>
    <span class="token string">"suggestions"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
      <span class="token string">"Consider making the ad name more descriptive"</span><span class="token punctuation">,</span>
      <span class="token string">"Try adding action verbs to make the ad more compelling"</span>
    <span class="token punctuation">]</span>
  <span class="token punctuation">}</span>
<span class="token punctuation">]</span>
</code></pre>
<h4 id="get_underperforming_adsclient-customer_id-budget_threshold-conversion_threshold">get_underperforming_ads(client, customer_id, budget_threshold, conversion_threshold)</h4>
<p><strong>Description</strong>: Retrieves a list of underperforming ads based on the specified budget and conversion thresholds.</p>
<h5 id="parameters-23">Parameters</h5>
<ul>
<li><code>client</code>: An instance of the Google Ads API client.</li>
<li><code>customer_id</code>: The customer ID for the Google Ads account.</li>
<li><code>budget_threshold</code>: The budget threshold to filter ads.</li>
<li><code>conversion_threshold</code>: The conversion threshold to filter ads.</li>
</ul>
<h5 id="returns-24">Returns</h5>
<p>A list of dictionaries, each representing an underperforming ad with its details.</p>
<h4 id="generate_suggestionsads">generate_suggestions(ads)</h4>
<p><strong>Description</strong>: Analyzes ad names using NLP to generate suggestions for improvement.</p>
<h5 id="parameters-24">Parameters</h5>
<ul>
<li><code>ads</code>: A list of dictionaries containing details of underperforming ads.</li>
</ul>
<h5 id="returns-25">Returns</h5>
<p>The input list of ads, enriched with suggestions for each ad.</p>
<h4 id="format_google_ads_errorsexception">format_google_ads_errors(exception)</h4>
<p><strong>Description</strong>: Formats errors from the Google Ads API exception into a list of readable messages.</p>
<h5 id="parameters-25">Parameters</h5>
<ul>
<li><code>exception</code>: An instance of <code>GoogleAdsException</code>.</li>
</ul>
<h5 id="returns-26">Returns</h5>
<p>A list of error messages.</p>
<h2 id="example-usage">Example Usage</h2>
<ol>
<li><strong>Send a POST request</strong> to the <code>/stop-loss-automation/</code> endpoint with the necessary parameters.</li>
<li><strong>Receive a response</strong> containing the details of underperforming ads and suggestions for improving their performance.</li>
</ol>
<p>Here’s a structured documentation for the <code>AIBuiddingOpenTarget</code> class, detailing its purpose, methods, parameters, and usage. This documentation follows standard API documentation practices.</p>
<hr>
<h2 id="ai-buidding-opentarget"><strong>15. AI Buidding OpenTarget</strong></h2>
<h2 id="overview-5">Overview</h2>
<p>The <code>AIBuiddingOpenTarget</code> class is an API view designed to analyze the performance of Google Ads campaigns. It retrieves performance data for enabled campaigns, performs data analysis, and provides actionable insights based on the analysis.</p>
<h2 id="methods-9">Methods</h2>
<h3 id="post-ai-building-open-target">POST /ai-building-open-target/</h3>
<p><strong>Description</strong>: This method handles the incoming POST request to fetch campaign performance data and return analysis results.</p>
<h4 id="request-body-2">Request Body</h4>
<p>The POST request does not require a specific request body but should include authentication as necessary.</p>
<h4 id="response-1">Response</h4>
<ul>
<li><strong>200 OK</strong>: Returns a list of analyzed campaign performance data.</li>
<li><strong>400 Bad Request</strong>: Returns an error message if the customer ID is not configured.</li>
<li><strong>500 Internal Server Error</strong>: Returns an error message if there is a failure in fetching or processing the campaign data.</li>
</ul>
<h4 id="example-response-200-ok">Example Response (200 OK)</h4>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">[</span>
  <span class="token punctuation">{</span>
    <span class="token string">"campaign_id"</span><span class="token punctuation">:</span> <span class="token string">"123456789"</span><span class="token punctuation">,</span>
    <span class="token string">"campaign_name"</span><span class="token punctuation">:</span> <span class="token string">"Campaign A"</span><span class="token punctuation">,</span>
    <span class="token string">"ad_group_id"</span><span class="token punctuation">:</span> <span class="token string">"987654321"</span><span class="token punctuation">,</span>
    <span class="token string">"ad_group_name"</span><span class="token punctuation">:</span> <span class="token string">"Ad Group 1"</span><span class="token punctuation">,</span>
    <span class="token string">"impressions"</span><span class="token punctuation">:</span> <span class="token number">1000</span><span class="token punctuation">,</span>
    <span class="token string">"clicks"</span><span class="token punctuation">:</span> <span class="token number">50</span><span class="token punctuation">,</span>
    <span class="token string">"cost_micros"</span><span class="token punctuation">:</span> <span class="token number">500000</span><span class="token punctuation">,</span>
    <span class="token string">"ctr"</span><span class="token punctuation">:</span> <span class="token number">0.05</span><span class="token punctuation">,</span>
    <span class="token string">"cost_inr"</span><span class="token punctuation">:</span> <span class="token number">0.5</span><span class="token punctuation">,</span>
    <span class="token string">"cpc_inr"</span><span class="token punctuation">:</span> <span class="token number">0.01</span><span class="token punctuation">,</span>
    <span class="token string">"segment"</span><span class="token punctuation">:</span> <span class="token number">0</span><span class="token punctuation">,</span>
    <span class="token string">"performance"</span><span class="token punctuation">:</span> <span class="token string">"Below Average"</span><span class="token punctuation">,</span>
    <span class="token string">"recommendation"</span><span class="token punctuation">:</span> <span class="token string">"Review ad copy and targeting to improve CTR"</span>
  <span class="token punctuation">}</span>
<span class="token punctuation">]</span>
</code></pre>
<h4 id="get_campaign_performanceclient-customer_id-max_retries3-retry_delay5">get_campaign_performance(client, customer_id, max_retries=3, retry_delay=5)</h4>
<p><strong>Description</strong>: Retrieves performance data for enabled Google Ads campaigns over the last 30 days.</p>
<h5 id="parameters-26">Parameters</h5>
<ul>
<li><code>client</code>: An instance of the Google Ads API client.</li>
<li><code>customer_id</code>: The customer ID for the Google Ads account.</li>
<li><code>max_retries</code>: The maximum number of retry attempts in case of failures (default: 3).</li>
<li><code>retry_delay</code>: The delay (in seconds) between retry attempts (default: 5).</li>
</ul>
<h5 id="returns-27">Returns</h5>
<p>A list of dictionaries, each containing details of campaign performance metrics including impressions, clicks, and cost.</p>
<h5 id="raises">Raises</h5>
<ul>
<li><strong>GoogleAdsException</strong>: If the API call fails after maximum retries.</li>
<li><strong>Exception</strong>: If unable to fetch campaign performance data after all retries.</li>
</ul>
<h4 id="data_analysiscampaign_data">data_analysis(campaign_data)</h4>
<p><strong>Description</strong>: Analyzes campaign performance data to compute metrics, categorize performance, and provide recommendations.</p>
<h5 id="parameters-27">Parameters</h5>
<ul>
<li><code>campaign_data</code>: A list of dictionaries containing raw campaign performance data.</li>
</ul>
<h5 id="returns-28">Returns</h5>
<p>A pandas DataFrame containing the analyzed campaign performance data, including metrics such as CTR, CPC, segmentation, performance categorization, and recommendations.</p>
<h3 id="example-usage-1">Example Usage</h3>
<ol>
<li><strong>Send a POST request</strong> to the <code>/ai-building-open-target/</code> endpoint without a body.</li>
<li><strong>Receive a response</strong> containing the analyzed campaign performance data along with actionable insights.</li>
</ol>
<h2 id="dependencies">Dependencies</h2>
<ul>
<li><strong>Django REST Framework</strong>: Required for building the API.</li>
<li><strong>Google Ads API</strong>: Required for interacting with Google Ads data.</li>
<li><strong>Pandas</strong>: Used for data manipulation and analysis.</li>
<li><strong>NumPy</strong>: Used for numerical operations.</li>
<li><strong>Scikit-learn</strong>: Used for machine learning algorithms like KMeans.</li>
<li><strong>Logging</strong>: Used for error logging.</li>
</ul>
<p>Here’s the structured documentation for the <code>BudgetRecommendationView</code> class, following the same format as the previous documentation.</p>
<hr>
<h1 id="budget-recommendation"><strong>17. Budget Recommendation</strong></h1>
<h2 id="overview-6">Overview</h2>
<p>The <code>BudgetRecommendationView</code> class is an API view designed to generate budget recommendations for Google Ads campaigns based on their performance metrics. It analyzes the current Return on Advertising Spend (ROAS) and suggests adjustments to the campaign budgets to optimize advertising effectiveness.</p>
<h3 id="post-budget-recommendation">POST /budget-recommendation/</h3>
<p><strong>Description</strong>: This method handles the incoming POST request to generate budget recommendations for active Google Ads campaigns based on the provided target ROAS and conversion value.</p>
<h4 id="request-body-3">Request Body</h4>
<ul>
<li><code>target_roas</code> (optional, default: <code>2.0</code>): The target Return on Advertising Spend.</li>
<li><code>conversion_value_inr</code> (required): The monetary value of conversions in Indian Rupees.</li>
</ul>
<h4 id="response-2">Response</h4>
<ul>
<li><strong>200 OK</strong>: Returns a list of budget recommendations for each active campaign.</li>
<li><strong>400 Bad Request</strong>: Returns an error message if <code>conversion_value_inr</code> is missing or not a valid number.</li>
<li><strong>500 Internal Server Error</strong>: Returns an error message if there is a failure in the Google Ads API call.</li>
</ul>
<h4 id="example-request-3">Example Request</h4>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
  <span class="token string">"target_roas"</span><span class="token punctuation">:</span> <span class="token number">2.5</span><span class="token punctuation">,</span>
  <span class="token string">"conversion_value_inr"</span><span class="token punctuation">:</span> <span class="token number">1000</span>
<span class="token punctuation">}</span>
</code></pre>
<h4 id="example-response-200-ok-1">Example Response (200 OK)</h4>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">[</span>
  <span class="token punctuation">{</span>
    <span class="token string">"campaign_id"</span><span class="token punctuation">:</span> <span class="token string">"1234567890"</span><span class="token punctuation">,</span>
    <span class="token string">"campaign_name"</span><span class="token punctuation">:</span> <span class="token string">"Campaign 1"</span><span class="token punctuation">,</span>
    <span class="token string">"current_budget"</span><span class="token punctuation">:</span> <span class="token string">"₹5000.00"</span><span class="token punctuation">,</span>
    <span class="token string">"recommended_budget"</span><span class="token punctuation">:</span> <span class="token string">"₹4500.00"</span><span class="token punctuation">,</span>
    <span class="token string">"current_roas"</span><span class="token punctuation">:</span> <span class="token string">"2.00"</span><span class="token punctuation">,</span>
    <span class="token string">"recommendation"</span><span class="token punctuation">:</span> <span class="token string">"Decrease budget from ₹5000.00 to ₹4500.00"</span>
  <span class="token punctuation">}</span><span class="token punctuation">,</span>
  <span class="token punctuation">{</span>
    <span class="token string">"campaign_id"</span><span class="token punctuation">:</span> <span class="token string">"0987654321"</span><span class="token punctuation">,</span>
    <span class="token string">"campaign_name"</span><span class="token punctuation">:</span> <span class="token string">"Campaign 2"</span><span class="token punctuation">,</span>
    <span class="token string">"current_budget"</span><span class="token punctuation">:</span> <span class="token string">"₹3000.00"</span><span class="token punctuation">,</span>
    <span class="token string">"recommended_budget"</span><span class="token punctuation">:</span> <span class="token string">"₹3300.00"</span><span class="token punctuation">,</span>
    <span class="token string">"current_roas"</span><span class="token punctuation">:</span> <span class="token string">"2.50"</span><span class="token punctuation">,</span>
    <span class="token string">"recommendation"</span><span class="token punctuation">:</span> <span class="token string">"Increase budget from ₹3000.00 to ₹3300.00"</span>
  <span class="token punctuation">}</span>
<span class="token punctuation">]</span>
</code></pre>
<h3 id="private-methods-1">Private Methods</h3>
<h4 id="initialize_client">initialize_client()</h4>
<p><strong>Description</strong>: Initializes the Google Ads client using the configuration stored in the specified YAML file.</p>
<h5 id="returns-29">Returns</h5>
<ul>
<li><code>GoogleAdsClient</code>: An instance of the Google Ads API client.</li>
</ul>
<h4 id="get_active_campaignsclient-customer_id">get_active_campaigns(client, customer_id)</h4>
<p><strong>Description</strong>: Retrieves a list of all active campaigns for the specified customer ID.</p>
<h5 id="parameters-28">Parameters</h5>
<ul>
<li><code>client</code>: An instance of the Google Ads API client.</li>
<li><code>customer_id</code>: The customer ID for the Google Ads account.</li>
</ul>
<h5 id="returns-30">Returns</h5>
<ul>
<li><code>response</code>: A list of active campaigns.</li>
</ul>
<h4 id="get_campaign_performanceclient-customer_id-campaign_id-date_range">get_campaign_performance(client, customer_id, campaign_id, date_range)</h4>
<p><strong>Description</strong>: Retrieves performance metrics for a specific campaign over a specified date range.</p>
<h5 id="parameters-29">Parameters</h5>
<ul>
<li><code>client</code>: An instance of the Google Ads API client.</li>
<li><code>customer_id</code>: The customer ID for the Google Ads account.</li>
<li><code>campaign_id</code>: The ID of the campaign to retrieve performance metrics for.</li>
<li><code>date_range</code>: A tuple containing the start and end dates for the performance data.</li>
</ul>
<h5 id="returns-31">Returns</h5>
<ul>
<li><code>response</code>: The performance metrics for the specified campaign.</li>
</ul>
<h4 id="generate_budget_recommendationsclient-customer_id-target_roas-conversion_value_inr">generate_budget_recommendations(client, customer_id, target_roas, conversion_value_inr)</h4>
<p><strong>Description</strong>: Generates budget recommendations for active campaigns based on their performance and the specified target ROAS.</p>
<h5 id="parameters-30">Parameters</h5>
<ul>
<li><code>client</code>: An instance of the Google Ads API client.</li>
<li><code>customer_id</code>: The customer ID for the Google Ads account.</li>
<li><code>target_roas</code>: The target Return on Advertising Spend.</li>
<li><code>conversion_value_inr</code>: The monetary value of conversions in Indian Rupees.</li>
</ul>
<h5 id="returns-32">Returns</h5>
<ul>
<li><code>recommendations</code>: A list of budget recommendations for each active campaign.</li>
</ul>
<h3 id="example-usage-2">Example Usage</h3>
<ol>
<li><strong>Send a POST request</strong> to the <code>/budget-recommendation/</code> endpoint with the required body.</li>
<li><strong>Receive a response</strong> containing budget recommendations for each active campaign.</li>
</ol>
<h2 id="dependencies-1">Dependencies</h2>
<ul>
<li><strong>Django REST Framework</strong>: Required for building the API.</li>
<li><strong>Google Ads API</strong>: Required for retrieving campaign data and performance metrics.</li>
<li><strong>Datetime</strong>: Used for handling date calculations.</li>
</ul>
<p>Sure! Here’s a comprehensive documentation for the <code>pauseLosingAdsToday</code> class in a similar style as the previous one you provided:</p>
<hr>
<h2 id="pause-losing-ads-today"><strong>17.Pause Losing Ads Today</strong></h2>
<p>The <code>pauseLosingAdsToday</code> class is an API view that analyzes ad groups from Google Ads data over the last 30 days and provides recommendations to pause ads that are underperforming based on return on investment (ROI) analysis.</p>
<h3 id="methods-10">Methods</h3>
<h4 id="getself-request-6"><code>get(self, request)</code></h4>
<p>Handles GET requests to analyze ad group performance and generate recommendations.</p>
<ul>
<li>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>request</code>: The HTTP request object.</li>
</ul>
</li>
<li>
<p><strong>Returns:</strong></p>
<ul>
<li>A JSON response containing recommendations for ad groups based on their performance metrics.</li>
<li>Status code <code>200 OK</code> on success.</li>
<li>Status code <code>400 Bad Request</code> if there is an error in processing the Google Ads data.</li>
</ul>
</li>
<li>
<p><strong>Process:</strong></p>
<ol>
<li>Initializes the Google Ads client using credentials from the YAML file.</li>
<li>Fetches ad group performance data for the past 30 days.</li>
<li>Calls <code>process_data()</code> to structure the response data.</li>
<li>Calls <code>generate_recommendations()</code> to analyze the performance and generate recommendations based on ROI.</li>
</ol>
</li>
</ul>
<h4 id="process_dataself-response"><code>process_data(self, response)</code></h4>
<p>Processes the Google Ads response to structure ad group data.</p>
<ul>
<li>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>response</code>: The response object returned from the Google Ads API.</li>
</ul>
</li>
<li>
<p><strong>Returns:</strong></p>
<ul>
<li>A dictionary containing structured ad group data including costs, revenues, ROIs, impressions, clicks, and conversions.</li>
</ul>
</li>
<li>
<p><strong>Process:</strong></p>
<ol>
<li>Iterates through the response data.</li>
<li>Converts costs from micros to INR.</li>
<li>Calculates ROI and compiles data for each ad group.</li>
</ol>
</li>
</ul>
<h4 id="generate_recommendationsself-ad_group_data"><code>generate_recommendations(self, ad_group_data)</code></h4>
<p>Generates recommendations based on processed ad group data.</p>
<ul>
<li>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>ad_group_data</code>: A dictionary containing structured data for each ad group.</li>
</ul>
</li>
<li>
<p><strong>Returns:</strong></p>
<ul>
<li>A list of recommendations for each ad group.</li>
</ul>
</li>
<li>
<p><strong>Process:</strong></p>
<ol>
<li>Iterates over each ad group.</li>
<li>Calls <code>analyze_ad_group()</code> to analyze the ad group’s performance.</li>
<li>Generates a summary using <code>generate_summary()</code>.</li>
</ol>
</li>
</ul>
<h4 id="analyze_ad_groupself-data"><code>analyze_ad_group(self, data)</code></h4>
<p>Analyzes the performance of an individual ad group and generates a recommendation based on ROI and anomaly detection.</p>
<ul>
<li>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>data</code>: A dictionary containing performance data for a single ad group.</li>
</ul>
</li>
<li>
<p><strong>Returns:</strong></p>
<ul>
<li>A string with the recommendation based on the analysis.</li>
</ul>
</li>
<li>
<p><strong>Process:</strong></p>
<ol>
<li>Converts data into a DataFrame for time series analysis.</li>
<li>Performs exponential smoothing for ROI forecasting.</li>
<li>Detects anomalies using Isolation Forest.</li>
<li>Generates a recommendation based on forecasted ROI and anomaly percentage.</li>
</ol>
</li>
</ul>
<h4 id="generate_summaryself-data"><code>generate_summary(self, data)</code></h4>
<p>Generates a summary of performance metrics for a given ad group.</p>
<ul>
<li>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>data</code>: A dictionary containing performance data for a single ad group.</li>
</ul>
</li>
<li>
<p><strong>Returns:</strong></p>
<ul>
<li>A dictionary summarizing the ad group’s total cost, revenue, impressions, clicks, conversions, average cost per click (CPC), average cost per acquisition (CPA), and return on ad spend (ROAS).</li>
</ul>
</li>
<li>
<p><strong>Process:</strong></p>
<ol>
<li>Sums up the costs, revenues, impressions, clicks, and conversions.</li>
<li>Calculates average CPC and CPA.</li>
<li>Computes ROAS.</li>
</ol>
</li>
</ul>
<h3 id="exception-handling-2">Exception Handling</h3>
<p>If a <code>GoogleAdsException</code> occurs during the API call, the class captures the error message and returns a response with status code <code>400 Bad Request</code>, including details about the error.</p>
<p>Here’s a structured documentation for your <code>UnderPerformingAds</code> class, following a similar style as your previous documentation:</p>
<hr>
<h2 id="under-performing-ads-class-">**18. Under Performing Ads Class **</h2>
<h2 id="overview-7">Overview</h2>
<p>The <code>UnderPerformingAds</code> class is an API view that retrieves and analyzes Google Ads data to identify underperforming ads based on cost-per-acquisition (CPA). It provides tailored recommendations for improving ad performance. This class utilizes the Google Ads API and employs machine learning techniques to generate insights.</p>
<h2 id="endpoints">Endpoints</h2>
<h3 id="get-underperforming-ads">GET /underperforming-ads</h3>
<p>Retrieves a list of underperforming ads over a specified number of days.</p>
<h4 id="query-parameters-2">Query Parameters</h4>
<ul>
<li><strong>days</strong> (optional): An integer representing the number of days to look back for ad performance data. Defaults to 30 if not provided.</li>
</ul>
<h4 id="response-3">Response</h4>
<ul>
<li><strong>200 OK</strong>: Returns a JSON object containing recommendations for underperforming ads.</li>
<li><strong>400 Bad Request</strong>: If the <code>days</code> parameter is invalid or not an integer.</li>
<li><strong>500 Internal Server Error</strong>: If an error occurs while processing the request, including Google Ads API errors.</li>
</ul>
<h2 id="methods-11">Methods</h2>
<h3 id="getself-request-7"><code>get(self, request)</code></h3>
<p>Handles GET requests to fetch underperforming ads.</p>
<h4 id="parameters-31">Parameters</h4>
<ul>
<li><strong>request</strong>: The incoming HTTP request object.</li>
</ul>
<h4 id="returns-33">Returns</h4>
<ul>
<li><strong>Response</strong>: A Response object containing either the recommendations for underperforming ads or an error message.</li>
</ul>
<h3 id="mainself-client-customer_id-days"><code>main(self, client, customer_id, days)</code></h3>
<p>The main method that orchestrates the data fetching, preprocessing, model training, and recommendation generation.</p>
<h4 id="parameters-32">Parameters</h4>
<ul>
<li><strong>client</strong>: The Google Ads client instance.</li>
<li><strong>customer_id</strong>: The Google Ads customer ID.</li>
<li><strong>days</strong>: The number of days to retrieve data for.</li>
</ul>
<h4 id="returns-34">Returns</h4>
<ul>
<li><strong>dict</strong>: A dictionary containing recommendations and (optionally) visualizations.</li>
</ul>
<h3 id="get_google_ads_dataself-client-customer_id-days"><code>get_google_ads_data(self, client, customer_id, days)</code></h3>
<p>Fetches Google Ads data for the specified customer ID and date range.</p>
<h4 id="parameters-33">Parameters</h4>
<ul>
<li><strong>client</strong>: The Google Ads client instance.</li>
<li><strong>customer_id</strong>: The Google Ads customer ID.</li>
<li><strong>days</strong>: The number of days to retrieve data for.</li>
</ul>
<h4 id="returns-35">Returns</h4>
<ul>
<li><strong>List[Dict[str, Any]]</strong>: A list of dictionaries containing ad performance metrics.</li>
</ul>
<h3 id="preprocess_dataself-data"><code>preprocess_data(self, data)</code></h3>
<p>Preprocesses the raw Google Ads data into a Pandas DataFrame and computes additional metrics.</p>
<h4 id="parameters-34">Parameters</h4>
<ul>
<li><strong>data</strong>: A list of dictionaries containing raw Google Ads data.</li>
</ul>
<h4 id="returns-36">Returns</h4>
<ul>
<li><strong>pd.DataFrame</strong>: A DataFrame containing preprocessed ad performance data.</li>
</ul>
<h3 id="train_modelself-df"><code>train_model(self, df)</code></h3>
<p>Trains a Random Forest model to predict CPA based on historical ad performance data.</p>
<h4 id="parameters-35">Parameters</h4>
<ul>
<li><strong>df</strong>: A DataFrame containing preprocessed ad performance data.</li>
</ul>
<h4 id="returns-37">Returns</h4>
<ul>
<li><strong>GridSearchCV</strong>: The trained GridSearchCV object containing the best model and hyperparameters.</li>
</ul>
<h3 id="get_tailored_recommendationself-ad"><code>get_tailored_recommendation(self, ad)</code></h3>
<p>Generates tailored recommendations for a specific ad based on its performance metrics.</p>
<h4 id="parameters-36">Parameters</h4>
<ul>
<li><strong>ad</strong>: A Pandas Series containing ad performance metrics.</li>
</ul>
<h4 id="returns-38">Returns</h4>
<ul>
<li><strong>str</strong>: A string containing recommendations for improving ad performance.</li>
</ul>
<h3 id="generate_recommendationsself-df-model-threshold_multiplier1.2"><code>generate_recommendations(self, df, model, threshold_multiplier=1.2)</code></h3>
<p>Generates recommendations for underperforming ads based on predicted CPA.</p>
<h4 id="parameters-37">Parameters</h4>
<ul>
<li><strong>df</strong>: A DataFrame containing preprocessed ad performance data.</li>
<li><strong>model</strong>: The trained Random Forest model.</li>
<li><strong>threshold_multiplier</strong>: A multiplier for determining the threshold of underperformance.</li>
</ul>
<h4 id="returns-39">Returns</h4>
<ul>
<li><strong>List[Dict[str, Any]]</strong>: A list of dictionaries containing recommendations for underperforming ads.</li>
</ul>
<h3 id="handle_google_ads_exceptionself-ex"><code>handle_google_ads_exception(self, ex)</code></h3>
<p>Handles exceptions raised by the Google Ads API and formats the error message for easier understanding.</p>
<h4 id="parameters-38">Parameters</h4>
<ul>
<li><strong>ex</strong>: The GoogleAdsException object.</li>
</ul>
<h4 id="returns-40">Returns</h4>
<ul>
<li><strong>str</strong>: A formatted error message describing the exception.</li>
</ul>
<h3 id="format_inrself-amount-3"><code>format_inr(self, amount)</code></h3>
<p>Formats a given amount as Indian Rupees.</p>
<h4 id="parameters-39">Parameters</h4>
<ul>
<li><strong>amount</strong>: A float representing the amount to be formatted.</li>
</ul>
<h4 id="returns-41">Returns</h4>
<ul>
<li><strong>str</strong>: A string formatted in Indian Rupees.</li>
</ul>
<h2 id="logging-2">Logging</h2>
<p>The class uses the <code>logger</code> to record significant events and errors throughout its methods, aiding in debugging and monitoring.</p>
<h2 id="dependencies-2">Dependencies</h2>
<ul>
<li><strong>Google Ads API</strong>: For fetching ad performance data.</li>
<li><strong>Pandas</strong>: For data manipulation and preprocessing.</li>
<li><strong>Scikit-learn</strong>: For machine learning model training and evaluation.</li>
<li><strong>NumPy</strong>: For numerical operations.</li>
</ul>
<p>Sure! Here’s a structured documentation for the <code>MLEnhancedCampaignRecommender</code> class, which outlines its purpose, methods, and the data flow.</p>
<hr>
<h2 id="scale-your-winners"><strong>Scale Your Winners</strong></h2>
<h3 id="overview-8">Overview</h3>
<p>The <code>Scale Your Winners</code> class is designed to interact with the Google Ads API to fetch active campaign data, process the data for machine learning analysis, and generate recommendations for enhancing campaign performance. This is achieved through the use of various machine learning techniques, including regression and clustering.</p>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>*args</code>: Variable length argument list.</li>
<li><code>**kwargs</code>: Arbitrary keyword arguments.</li>
</ul>
<h2 id="methods-12">Methods</h2>
<h3 id="get_campaignsself"><code>get_campaigns(self)</code></h3>
<p>Fetches active Google Ads campaigns from the account.</p>
<p><strong>Returns:</strong></p>
<ul>
<li><code>active_campaigns</code> (List[Dict]): A list of dictionaries containing details of active campaigns, including ID, name, budget, impressions, clicks, conversions, and enhanced CPC status.</li>
</ul>
<p><strong>Exceptions:</strong></p>
<ul>
<li>Raises <code>GoogleAdsException</code> if the API request fails.</li>
</ul>
<h3 id="preprocess_dataself-campaigns"><code>preprocess_data(self, campaigns)</code></h3>
<p>Prepares the fetched campaign data for machine learning analysis.</p>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>campaigns</code> (List[Dict]): A list of campaign data fetched from the Google Ads API.</li>
</ul>
<p><strong>Returns:</strong></p>
<ul>
<li><code>df</code> (DataFrame): A Pandas DataFrame containing processed campaign data.</li>
<li><code>numeric_columns</code> (List[str]): A list of numeric feature column names.</li>
<li><code>categorical_columns</code> (List[str]): A list of categorical feature column names.</li>
</ul>
<h3 id="train_modelsself-df-numeric_columns"><code>train_models(self, df, numeric_columns)</code></h3>
<p>Trains machine learning models on the processed campaign data.</p>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>df</code> (DataFrame): The processed campaign DataFrame.</li>
<li><code>numeric_columns</code> (List[str]): A list of numeric feature column names.</li>
</ul>
<p><strong>Returns:</strong></p>
<ul>
<li><code>rf_model</code>: Trained Random Forest model.</li>
<li><code>gb_model</code>: Trained Gradient Boosting model.</li>
<li><code>scaler</code>: Scikit-learn StandardScaler used for feature scaling.</li>
<li><code>features</code> (List[str]): A list of feature names used for training.</li>
</ul>
<h3 id="get_feature_importanceself-model-features"><code>get_feature_importance(self, model, features)</code></h3>
<p>Retrieves the feature importance scores from a trained model.</p>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>model</code>: A trained machine learning model (Random Forest or Gradient Boosting).</li>
<li><code>features</code> (List[str]): A list of feature names.</li>
</ul>
<p><strong>Returns:</strong></p>
<ul>
<li><code>feature_importance</code> (List[Tuple[str, float]]): A list of tuples containing feature names and their corresponding importance scores.</li>
</ul>
<h3 id="cluster_campaignsself-df-numeric_columns"><code>cluster_campaigns(self, df, numeric_columns)</code></h3>
<p>Clusters the campaigns based on relevant features using KMeans clustering.</p>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>df</code> (DataFrame): The processed campaign DataFrame.</li>
<li><code>numeric_columns</code> (List[str]): A list of numeric feature column names.</li>
</ul>
<p><strong>Returns:</strong></p>
<ul>
<li><code>df</code> (DataFrame): The updated DataFrame with cluster assignments.</li>
<li><code>kmeans</code>: The KMeans model used for clustering.</li>
</ul>
<h3 id="generate_recommendationsself-campaigns"><code>generate_recommendations(self, campaigns)</code></h3>
<p>Generates performance improvement recommendations for the fetched campaigns.</p>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>campaigns</code> (List[Dict]): A list of campaign data fetched from the Google Ads API.</li>
</ul>
<p><strong>Returns:</strong></p>
<ul>
<li><code>recommendations</code> (List[Dict]): A list of recommendations, each containing details such as campaign ID, name, current budget, predicted conversions, cluster, top features, and suggestions for improvement.</li>
</ul>
<h3 id="postself-request-1"><code>post(self, request)</code></h3>
<p>Handles the POST request to fetch campaigns and generate recommendations.</p>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>request</code>: The incoming HTTP request.</li>
</ul>
<p><strong>Returns:</strong></p>
<ul>
<li><code>Response</code>: A JSON response containing either the recommendations or an error message.</li>
</ul>
<p><strong>Exceptions:</strong></p>
<ul>
<li>Handles <code>GoogleAdsException</code> and general exceptions, returning appropriate error messages.</li>
</ul>
<h2 id="logging-3">Logging</h2>
<ul>
<li>The class logs various actions and errors using a logger to facilitate troubleshooting and monitoring.</li>
</ul>
<p>Here’s a comprehensive documentation outline for your <code>MLEnhancedCampaignRecommender</code> and <code>PerformanceAnalysisView</code> classes, which can be added as comments in the code or as a separate markdown file.</p>
<hr>
<h2 id="low-performing-resource-reallocation"><strong>Low Performing Resource Reallocation</strong></h2>
<h2 id="overview-9">Overview</h2>
<p>This module provides functionalities to analyze the performance of Google Ads campaigns and generate recommendations based on specified performance metrics for machine learning-based recommendations and <code>Low Performing Resource Reallocation</code> for analyzing ad spend performance.</p>
<h4 id="methods-13">Methods</h4>
<ul>
<li>
<p><strong><code>__init__(self, *args, **kwargs)</code></strong></p>
<ul>
<li>Initializes the recommender with Google Ads client settings.</li>
<li><strong>Parameters:</strong>
<ul>
<li><code>*args</code>: Variable length argument list.</li>
<li><code>**kwargs</code>: Arbitrary keyword arguments.</li>
</ul>
</li>
</ul>
</li>
<li>
<p><strong><code>get_campaigns(self)</code></strong></p>
<ul>
<li>Fetches all active Google Ads campaigns.</li>
<li><strong>Returns:</strong>
<ul>
<li>A list of active campaigns with details like ID, name, budget, impressions, clicks, and conversions.</li>
</ul>
</li>
</ul>
</li>
<li>
<p><strong><code>preprocess_data(self, campaigns)</code></strong></p>
<ul>
<li>Prepares the campaign data for machine learning by performing feature engineering and data cleaning.</li>
<li><strong>Parameters:</strong>
<ul>
<li><code>campaigns</code>: List of campaign data dictionaries.</li>
</ul>
</li>
<li><strong>Returns:</strong>
<ul>
<li>A DataFrame of processed data, list of numeric columns, and list of categorical columns.</li>
</ul>
</li>
</ul>
</li>
<li>
<p><strong><code>train_models(self, df, numeric_columns)</code></strong></p>
<ul>
<li>Trains machine learning models (Random Forest and Gradient Boosting) on the campaign data.</li>
<li><strong>Parameters:</strong>
<ul>
<li><code>df</code>: DataFrame containing the campaign data.</li>
<li><code>numeric_columns</code>: List of numeric feature names.</li>
</ul>
</li>
<li><strong>Returns:</strong>
<ul>
<li>The trained Random Forest and Gradient Boosting models, the scaler, and the features used for training.</li>
</ul>
</li>
</ul>
</li>
<li>
<p><strong><code>get_feature_importance(self, model, features)</code></strong></p>
<ul>
<li>Retrieves the feature importance from the trained model.</li>
<li><strong>Parameters:</strong>
<ul>
<li><code>model</code>: The trained model.</li>
<li><code>features</code>: List of feature names.</li>
</ul>
</li>
<li><strong>Returns:</strong>
<ul>
<li>A sorted list of features and their importance scores.</li>
</ul>
</li>
</ul>
</li>
<li>
<p><strong><code>cluster_campaigns(self, df, numeric_columns)</code></strong></p>
<ul>
<li>Clusters campaigns based on selected numeric features using KMeans clustering.</li>
<li><strong>Parameters:</strong>
<ul>
<li><code>df</code>: DataFrame of campaign data.</li>
<li><code>numeric_columns</code>: List of numeric feature names.</li>
</ul>
</li>
<li><strong>Returns:</strong>
<ul>
<li>The DataFrame with cluster labels and the KMeans model.</li>
</ul>
</li>
</ul>
</li>
<li>
<p><strong><code>generate_recommendations(self, campaigns)</code></strong></p>
<ul>
<li>Generates recommendations based on the campaign data and trained models.</li>
<li><strong>Parameters:</strong>
<ul>
<li><code>campaigns</code>: List of campaign data dictionaries.</li>
</ul>
</li>
<li><strong>Returns:</strong>
<ul>
<li>A list of recommendations for each campaign.</li>
</ul>
</li>
</ul>
</li>
<li>
<p><strong><code>post(self, request)</code></strong></p>
<ul>
<li>Handles POST requests to analyze campaigns and generate recommendations.</li>
<li><strong>Parameters:</strong>
<ul>
<li><code>request</code>: The HTTP request object.</li>
</ul>
</li>
<li><strong>Returns:</strong>
<ul>
<li>A Response containing recommendations or error messages.</li>
</ul>
</li>
</ul>
</li>
</ul>
<h3 id="performanceanalysisview">PerformanceAnalysisView</h3>
<p>This class provides an API endpoint to analyze the performance of Google Ads campaigns based on a user-defined performance threshold.</p>
<h4 id="methods-14">Methods</h4>
<ul>
<li><strong><code>post(self, request)</code></strong>
<ul>
<li>Handles POST requests for performance analysis of Google Ads campaigns.</li>
<li><strong>Parameters:</strong>
<ul>
<li><code>request</code>: The HTTP request object containing the <code>performance_threshold</code>.</li>
</ul>
</li>
<li><strong>Returns:</strong>
<ul>
<li>A Response containing recommendations or error messages.</li>
</ul>
</li>
</ul>
</li>
</ul>
<hr>
<h2 id="usage">Usage</h2>
<ol>
<li><strong>Fetch Active Campaigns</strong>: The <code>get_campaigns</code> method retrieves all currently active Google Ads campaigns.</li>
<li><strong>Analyze Performance</strong>: The <code>get_campaign_performance</code> method retrieves the performance data (clicks, impressions, CTR, and ad spend) for a specified campaign.</li>
<li><strong>Generate Recommendations</strong>: The <code>generate_ad_spend_recommendation</code> method generates recommendations based on the campaign’s CTR compared to the performance threshold.</li>
<li><strong>Run Performance Analysis</strong>: The <code>run_performance_analysis</code> method integrates the previous methods to fetch active campaigns, analyze their performance, and return recommendations.</li>
<li><strong>API Integration</strong>: The <code>PerformanceAnalysisView</code> class exposes the functionality through a RESTful API, allowing users to submit a performance threshold and receive recommendations.</li>
</ol>
<h2 id="error-handling-8">Error Handling</h2>
<ul>
<li>The system handles <code>GoogleAdsException</code> for errors related to the Google Ads API, and it will print the error message to the console.</li>
<li>The API response includes appropriate status codes (e.g., <code>400 Bad Request</code> for invalid input) to inform the user about any issues.</li>
</ul>
<h2 id="example-request-4">Example Request</h2>
<h3 id="post-low-performing-resource-reallocation">POST /low-performing-resource-reallocation/</h3>
<p><strong>Request Body:</strong></p>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
    <span class="token string">"performance_threshold"</span><span class="token punctuation">:</span> <span class="token number">0.05</span>
<span class="token punctuation">}</span>
</code></pre>
<p><strong>Response:</strong></p>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
    <span class="token string">"recommendations"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
        <span class="token punctuation">{</span>
            <span class="token string">"campaign_id"</span><span class="token punctuation">:</span> <span class="token string">"123456"</span><span class="token punctuation">,</span>
            <span class="token string">"campaign_name"</span><span class="token punctuation">:</span> <span class="token string">"Spring Sale"</span><span class="token punctuation">,</span>
            <span class="token string">"current_ad_spend"</span><span class="token punctuation">:</span> <span class="token number">5000</span><span class="token punctuation">,</span>
            <span class="token string">"recommended_ad_spend"</span><span class="token punctuation">:</span> <span class="token number">4500</span><span class="token punctuation">,</span>
            <span class="token string">"reason"</span><span class="token punctuation">:</span> <span class="token string">"CTR (4.50%) is below threshold (5.00%)"</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">]</span>
<span class="token punctuation">}</span>
</code></pre>
<p>Here’s a detailed documentation outline for your <code>AdGroupRecommendationsView</code> class. This documentation can be included as comments in the code or as a separate markdown file.</p>
<hr>
<h2 id="kill-losing-ad-groups"><strong>19. Kill Losing Ad Groups</strong></h2>
<h2 id="overview-10">Overview</h2>
<p>The <code>Kill Losing Ad Groups</code> class provides an API endpoint for generating recommendations for ad groups based on their performance metrics in Google Ads. It utilizes two helper classes, <code>AdGroupProfiler</code> and <code>AdGroupRecommender</code>, to analyze ad group performance and generate actionable insights.</p>
<h2 id="class-adgrouprecommendationsview">Class: AdGroupRecommendationsView</h2>
<h3 id="inheritance-1">Inheritance</h3>
<ul>
<li>Inherits from <code>APIView</code>, which is part of the Django REST framework.</li>
</ul>
<h3 id="attributes">Attributes</h3>
<ul>
<li><strong><code>parser_classes</code></strong>: Specifies the parser for incoming requests. Here, it uses <code>JSONParser</code> to handle JSON data.</li>
</ul>
<h3 id="methods-15">Methods</h3>
<h4 id="postself-request-2"><code>post(self, request)</code></h4>
<p>Handles POST requests to generate ad group recommendations based on the specified time frame and ROI threshold.</p>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>request</code>: The HTTP request object containing the following data in JSON format:
<ul>
<li><code>days</code> (optional): An integer indicating the number of days for performance analysis (default is 30).</li>
<li><code>roi_threshold</code> (optional): A float representing the return on investment (ROI) threshold for recommendations (default is 0).</li>
</ul>
</li>
</ul>
<p><strong>Returns:</strong></p>
<ul>
<li>
<p>On success:</p>
<ul>
<li><code>Response</code>: A JSON response containing the list of recommendations generated.</li>
</ul>
</li>
<li>
<p>On error:</p>
<ul>
<li><code>Response</code>: A JSON response with an error message and corresponding HTTP status code.</li>
</ul>
</li>
</ul>
<p><strong>Error Handling:</strong></p>
<ul>
<li><strong>Invalid Input</strong>: If <code>days</code> or <code>roi_threshold</code> cannot be converted to the appropriate type, it returns a <code>400 Bad Request</code> with an error message.</li>
<li><strong>Google Ads Client Error</strong>: If the Google Ads client fails to load, it logs the error and returns a <code>500 Internal Server Error</code> with a corresponding message.</li>
<li><strong>Google Ads API Error</strong>: If there are errors during performance retrieval or recommendation generation, it captures detailed error messages from the Google Ads API and returns a <code>400 Bad Request</code>.</li>
<li><strong>General Error</strong>: Any other exceptions encountered during processing are logged and result in a <code>500 Internal Server Error</code>.</li>
</ul>
<h3 id="usage-1">Usage</h3>
<ol>
<li><strong>Send a POST Request</strong>: The client sends a POST request to the endpoint associated with this view, providing the desired <code>days</code> and <code>roi_threshold</code> values.</li>
<li><strong>Process Request</strong>: The view processes the request:
<ul>
<li>Validates and converts the input parameters.</li>
<li>Loads the Google Ads client.</li>
<li>Retrieves performance data for active ad groups using the <code>AdGroupProfiler</code> class.</li>
<li>Calculates profitability metrics.</li>
<li>Generates recommendations using the <code>AdGroupRecommender</code> class.</li>
</ul>
</li>
<li><strong>Response</strong>: The server responds with either a list of recommendations or an error message.</li>
</ol>
<h3 id="example-request-5">Example Request</h3>
<h4 id="post-kill_losing_ad_groups">POST /Kill_Losing_Ad_Groups/</h4>
<p><strong>Request Body:</strong></p>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
    <span class="token string">"days"</span><span class="token punctuation">:</span> <span class="token number">30</span><span class="token punctuation">,</span>
    <span class="token string">"roi_threshold"</span><span class="token punctuation">:</span> <span class="token number">1.5</span>
<span class="token punctuation">}</span>
</code></pre>
<p><strong>Successful Response:</strong></p>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">[</span>
    <span class="token punctuation">{</span>
        <span class="token string">"ad_group_id"</span><span class="token punctuation">:</span> <span class="token string">"1234567890"</span><span class="token punctuation">,</span>
        <span class="token string">"ad_group_name"</span><span class="token punctuation">:</span> <span class="token string">"Ad Group 1"</span><span class="token punctuation">,</span>
        <span class="token string">"recommended_action"</span><span class="token punctuation">:</span> <span class="token string">"Increase budget by 20%"</span><span class="token punctuation">,</span>
        <span class="token string">"expected_roi"</span><span class="token punctuation">:</span> <span class="token number">2.0</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
    <span class="token punctuation">{</span>
        <span class="token string">"ad_group_id"</span><span class="token punctuation">:</span> <span class="token string">"0987654321"</span><span class="token punctuation">,</span>
        <span class="token string">"ad_group_name"</span><span class="token punctuation">:</span> <span class="token string">"Ad Group 2"</span><span class="token punctuation">,</span>
        <span class="token string">"recommended_action"</span><span class="token punctuation">:</span> <span class="token string">"Reduce budget by 15%"</span><span class="token punctuation">,</span>
        <span class="token string">"expected_roi"</span><span class="token punctuation">:</span> <span class="token number">0.8</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">]</span>
</code></pre>
<p><strong>Error Response Example:</strong></p>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
    <span class="token string">"error"</span><span class="token punctuation">:</span> <span class="token string">"Invalid days or roi_threshold parameter"</span>
<span class="token punctuation">}</span>
</code></pre>
<hr>
<h2 id="logging-4">Logging</h2>
<p>The view uses logging to capture important events and errors:</p>
<ul>
<li>Logs the number of generated recommendations for audit purposes.</li>
<li>Logs errors encountered during processing, including specific Google Ads API errors and general exceptions.</li>
</ul>
<p>Here’s a detailed documentation outline for your <code>AdsAnalysisView</code> class. This documentation can be included as comments in the code or as a separate markdown file.</p>
<hr>
<h2 id="mark-high-ctr">Mark High Ctr</h2>
<h2 id="overview-11">Overview</h2>
<p>The <code>mark-high-ctr</code> class provides an API endpoint for analyzing ad performance data from Google Ads and generating recommendations based on the analysis. It utilizes clustering and anomaly detection techniques to identify high-performing ads.</p>
<h2 id="class-adsanalysisview">Class: AdsAnalysisView</h2>
<h3 id="inheritance-2">Inheritance</h3>
<ul>
<li>Inherits from <code>APIView</code>, which is part of the Django REST framework.</li>
</ul>
<h3 id="methods-16">Methods</h3>
<h4 id="get_ad_performance_dataself-client-customer_id-str---listdict"><code>get_ad_performance_data(self, client, customer_id: str) -&gt; List[Dict]</code></h4>
<p>Retrieves ad performance data from Google Ads.</p>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>client</code>: An instance of the Google Ads client used to make API calls.</li>
<li><code>customer_id</code> (str): The Google Ads customer ID for which to retrieve ad performance data.</li>
</ul>
<p><strong>Returns:</strong></p>
<ul>
<li><code>List[Dict]</code>: A list of dictionaries containing ad performance metrics.</li>
</ul>
<p><strong>Error Handling:</strong></p>
<ul>
<li>Logs an error message and returns an empty list if an exception occurs.</li>
</ul>
<h4 id="preprocess_dataself-ads_data-listdict---np.ndarray"><code>preprocess_data(self, ads_data: List[Dict]) -&gt; np.ndarray</code></h4>
<p>Preprocesses the retrieved ad data for further analysis.</p>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>ads_data</code>: A list of dictionaries containing ad performance metrics.</li>
</ul>
<p><strong>Returns:</strong></p>
<ul>
<li><code>np.ndarray</code>: A scaled array of features (CTR, clicks, impressions, cost) suitable for clustering.</li>
</ul>
<h4 id="identify_high_performing_adsself-x_scaled-np.ndarray-ads_data-listdict---listdict"><code>identify_high_performing_ads(self, X_scaled: np.ndarray, ads_data: List[Dict]) -&gt; List[Dict]</code></h4>
<p>Identifies high-performing ads using clustering and anomaly detection techniques.</p>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>X_scaled</code>: A scaled array of features to analyze.</li>
<li><code>ads_data</code>: A list of dictionaries containing ad performance metrics.</li>
</ul>
<p><strong>Returns:</strong></p>
<ul>
<li><code>List[Dict]</code>: A list of dictionaries containing high-performing ads along with the reason for their classification.</li>
</ul>
<h4 id="generate_recommendationsself-high_performing_ads-listdict---listdict"><code>generate_recommendations(self, high_performing_ads: List[Dict]) -&gt; List[Dict]</code></h4>
<p>Generates performance-based recommendations for the identified high-performing ads.</p>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>high_performing_ads</code>: A list of dictionaries containing high-performing ad data.</li>
</ul>
<p><strong>Returns:</strong></p>
<ul>
<li><code>List[Dict]</code>: A list of recommendations for improving ad performance.</li>
</ul>
<h4 id="getself-request-8"><code>get(self, request)</code></h4>
<p>Handles GET requests to analyze ad performance and generate recommendations.</p>
<p><strong>Parameters:</strong></p>
<ul>
<li><code>request</code>: The HTTP request object.</li>
</ul>
<p><strong>Returns:</strong></p>
<ul>
<li>
<p>On success:</p>
<ul>
<li><code>Response</code>: A JSON response containing a list of recommendations.</li>
</ul>
</li>
<li>
<p>On error:</p>
<ul>
<li><code>Response</code>: A JSON response with an error message and corresponding HTTP status code.</li>
</ul>
</li>
</ul>
<p><strong>Error Handling:</strong></p>
<ul>
<li>If no ad data is retrieved, it returns a <code>404 Not Found</code> response.</li>
<li>Catches general exceptions and returns a <code>500 Internal Server Error</code> response with the error message.</li>
</ul>
<h3 id="usage-2">Usage</h3>
<ol>
<li><strong>Send a GET Request</strong>: The client sends a GET request to the endpoint associated with this view.</li>
<li><strong>Process Request</strong>: The view processes the request:
<ul>
<li>Loads the Google Ads client.</li>
<li>Retrieves ad performance data using the <code>get_ad_performance_data</code> method.</li>
<li>Preprocesses the data using the <code>preprocess_data</code> method.</li>
<li>Identifies high-performing ads using the <code>identify_high_performing_ads</code> method.</li>
<li>Generates recommendations using the <code>generate_recommendations</code> method.</li>
</ul>
</li>
<li><strong>Response</strong>: The server responds with either a list of recommendations or an error message.</li>
</ol>
<h3 id="example-request-6">Example Request</h3>
<h4 id="get-mark-high-ctr">GET /mark-high-ctr/</h4>
<p><strong>Successful Response:</strong></p>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
    <span class="token string">"recommendations"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
        <span class="token punctuation">{</span>
            <span class="token string">"ad_id"</span><span class="token punctuation">:</span> <span class="token string">"1234567890"</span><span class="token punctuation">,</span>
            <span class="token string">"ad_name"</span><span class="token punctuation">:</span> <span class="token string">"Ad 1"</span><span class="token punctuation">,</span>
            <span class="token string">"ad_group"</span><span class="token punctuation">:</span> <span class="token string">"Ad Group 1"</span><span class="token punctuation">,</span>
            <span class="token string">"campaign"</span><span class="token punctuation">:</span> <span class="token string">"Campaign 1"</span><span class="token punctuation">,</span>
            <span class="token string">"performance"</span><span class="token punctuation">:</span> <span class="token string">"Best Cluster"</span><span class="token punctuation">,</span>
            <span class="token string">"recommendations"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
                <span class="token string">"Consider increasing budget for this high-CTR ad"</span>
            <span class="token punctuation">]</span>
        <span class="token punctuation">}</span><span class="token punctuation">,</span>
        <span class="token punctuation">{</span>
            <span class="token string">"ad_id"</span><span class="token punctuation">:</span> <span class="token string">"0987654321"</span><span class="token punctuation">,</span>
            <span class="token string">"ad_name"</span><span class="token punctuation">:</span> <span class="token string">"Ad 2"</span><span class="token punctuation">,</span>
            <span class="token string">"ad_group"</span><span class="token punctuation">:</span> <span class="token string">"Ad Group 2"</span><span class="token punctuation">,</span>
            <span class="token string">"campaign"</span><span class="token punctuation">:</span> <span class="token string">"Campaign 2"</span><span class="token punctuation">,</span>
            <span class="token string">"performance"</span><span class="token punctuation">:</span> <span class="token string">"Anomaly"</span><span class="token punctuation">,</span>
            <span class="token string">"recommendations"</span><span class="token punctuation">:</span> <span class="token punctuation">[</span>
                <span class="token string">"Optimize ad copy to increase clicks"</span><span class="token punctuation">,</span>
                <span class="token string">"Monitor and optimize bidding strategy to control costs"</span>
            <span class="token punctuation">]</span>
        <span class="token punctuation">}</span>
    <span class="token punctuation">]</span>
<span class="token punctuation">}</span>
</code></pre>
<p><strong>Error Response Example:</strong></p>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
    <span class="token string">"error"</span><span class="token punctuation">:</span> <span class="token string">"No ad data retrieved. Please check your account and try again."</span>
<span class="token punctuation">}</span>
</code></pre>
<hr>
<h2 id="logging-5">Logging</h2>
<p>The view logs important events and errors during processing:</p>
<ul>
<li>Logs errors encountered while retrieving ad performance data.</li>
<li>Returns clear error messages in the response for troubleshooting.</li>
</ul>
<p>Sure! Here’s a structured documentation for the <code>ReviveRecommendationView</code> class in a textual format, which you can use for your API documentation or internal documentation purposes.</p>
<hr>
<h2 id="revive-ad-group-recommendations">21.Revive Ad-Group Recommendations</h2>
<h3 id="overview-12">Overview</h3>
<p>The <code>revive-ad-grouprecommendations</code> is a Django REST Framework API view that generates advertising recommendations based on Google Ads performance metrics. This view utilizes the Google Ads API to retrieve ad performance data and provide actionable insights to improve ad campaign effectiveness.</p>
<h3 id="endpoint-1">Endpoint</h3>
<ul>
<li><strong>POST</strong> <code>/api/revive-ad-grouprecommendations/</code></li>
</ul>
<h3 id="request">Request</h3>
<ul>
<li><strong>Method:</strong> <code>POST</code></li>
<li><strong>Headers:</strong>
<ul>
<li><code>Content-Type: application/json</code></li>
</ul>
</li>
<li><strong>Body:</strong> No specific body parameters are required. The request can be empty.</li>
</ul>
<h3 id="response-4">Response</h3>
<ul>
<li>
<p><strong>Success Response:</strong></p>
<ul>
<li><strong>Status Code:</strong> <code>200 OK</code></li>
<li><strong>Body:</strong><pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">[</span>
  <span class="token punctuation">{</span>
    <span class="token string">"campaign_id"</span><span class="token punctuation">:</span> <span class="token string">"123456"</span><span class="token punctuation">,</span>
    <span class="token string">"campaign_name"</span><span class="token punctuation">:</span> <span class="token string">"Campaign Name"</span><span class="token punctuation">,</span>
    <span class="token string">"ad_group_id"</span><span class="token punctuation">:</span> <span class="token string">"789012"</span><span class="token punctuation">,</span>
    <span class="token string">"ad_group_name"</span><span class="token punctuation">:</span> <span class="token string">"Ad Group Name"</span><span class="token punctuation">,</span>
    <span class="token string">"clicks"</span><span class="token punctuation">:</span> <span class="token number">5</span><span class="token punctuation">,</span>
    <span class="token string">"impressions"</span><span class="token punctuation">:</span> <span class="token number">2000</span><span class="token punctuation">,</span>
    <span class="token string">"ctr"</span><span class="token punctuation">:</span> <span class="token number">0.0025</span><span class="token punctuation">,</span>
    <span class="token string">"cpa"</span><span class="token punctuation">:</span> <span class="token number">150.00</span><span class="token punctuation">,</span>
    <span class="token string">"recommendation"</span><span class="token punctuation">:</span> <span class="token string">"Low clicks with high impressions"</span><span class="token punctuation">,</span>
    <span class="token string">"action"</span><span class="token punctuation">:</span> <span class="token string">"Consider increasing bids by 20% to improve visibility"</span><span class="token punctuation">,</span>
    <span class="token string">"score"</span><span class="token punctuation">:</span> <span class="token number">10</span>
  <span class="token punctuation">}</span><span class="token punctuation">,</span>
  <span class="token operator">...</span>
<span class="token punctuation">]</span>
</code></pre>
</li>
<li><strong>Description:</strong> Returns a list of the top advertising recommendations, sorted by their score.</li>
</ul>
</li>
<li>
<p><strong>Error Response:</strong></p>
<ul>
<li><strong>Status Code:</strong> <code>500 Internal Server Error</code></li>
<li><strong>Body:</strong><pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
  <span class="token string">"error"</span><span class="token punctuation">:</span> <span class="token string">"Error message detailing what went wrong"</span>
<span class="token punctuation">}</span>
</code></pre>
</li>
<li><strong>Description:</strong> Returns an error message if there is an issue with generating recommendations or fetching data.</li>
</ul>
</li>
</ul>
<h3 id="methods-17">Methods</h3>
<h4 id="postrequest-2">1. <code>post(request)</code></h4>
<ul>
<li><strong>Description:</strong> Handles POST requests to generate and return advertising recommendations.</li>
<li><strong>Parameters:</strong>
<ul>
<li><code>request</code>: The HTTP request object containing user input or parameters (not utilized in this method).</li>
</ul>
</li>
<li><strong>Returns:</strong> A JSON response containing the top advertising recommendations or an error message.</li>
</ul>
<h4 id="get_google_ads_client">2. <code>get_google_ads_client()</code></h4>
<ul>
<li><strong>Description:</strong> Initializes and returns a Google Ads client based on configuration settings.</li>
<li><strong>Returns:</strong> An instance of <code>GoogleAdsClient</code> configured with the settings defined in the project.</li>
</ul>
<h4 id="generate_recommendationsclient-customer_id">3. <code>generate_recommendations(client, customer_id)</code></h4>
<ul>
<li><strong>Description:</strong> Fetches ad performance data and generates recommendations based on specified criteria.</li>
<li><strong>Parameters:</strong>
<ul>
<li><code>client</code>: An instance of <code>GoogleAdsClient</code>.</li>
<li><code>customer_id</code>: The Google Ads customer ID for which recommendations are generated.</li>
</ul>
</li>
<li><strong>Returns:</strong> A list of recommendations based on ad performance metrics.</li>
</ul>
<h4 id="process_rowrow">4. <code>process_row(row)</code></h4>
<ul>
<li><strong>Description:</strong> Processes a single row of ad performance data and generates a recommendation if applicable.</li>
<li><strong>Parameters:</strong>
<ul>
<li><code>row</code>: A row object containing metrics from the Google Ads API.</li>
</ul>
</li>
<li><strong>Returns:</strong> A structured recommendation dictionary if criteria are met, otherwise <code>None</code>.</li>
</ul>
<h4 id="create_recommendationcampaign-ad_group-clicks-impressions-ctr-cpa-recommendation-action-score">5. <code>create_recommendation(campaign, ad_group, clicks, impressions, ctr, cpa, recommendation, action, score)</code></h4>
<ul>
<li><strong>Description:</strong> Creates a structured recommendation dictionary based on ad performance metrics.</li>
<li><strong>Parameters:</strong>
<ul>
<li><code>campaign</code>: The campaign object associated with the ad.</li>
<li><code>ad_group</code>: The ad group object associated with the ad.</li>
<li><code>clicks</code>: Number of clicks received by the ad.</li>
<li><code>impressions</code>: Number of impressions received by the ad.</li>
<li><code>ctr</code>: Click-through rate of the ad.</li>
<li><code>cpa</code>: Cost per acquisition for the ad.</li>
<li><code>recommendation</code>: The recommendation text generated.</li>
<li><code>action</code>: Suggested action to improve ad performance.</li>
<li><code>score</code>: The score assigned to the recommendation based on performance metrics.</li>
</ul>
</li>
<li><strong>Returns:</strong> A dictionary containing the structured recommendation details.</li>
</ul>
<h4 id="get_top_recommendationsrecommendations-n20">6. <code>get_top_recommendations(recommendations, n=20)</code></h4>
<ul>
<li><strong>Description:</strong> Sorts recommendations by score and returns the top N recommendations.</li>
<li><strong>Parameters:</strong>
<ul>
<li><code>recommendations</code>: A list of recommendation dictionaries.</li>
<li><code>n</code>: The number of top recommendations to return (default is 20).</li>
</ul>
</li>
<li><strong>Returns:</strong> A list of the top N recommendations sorted by score.</li>
</ul>
<h3 id="usage-3">Usage</h3>
<ul>
<li>The endpoint is used by clients (e.g., front-end applications or other services) to retrieve recommendations for optimizing Google Ads campaigns. No input parameters are required in the request body, making it straightforward to integrate.</li>
</ul>
<h3 id="exception-handling-3">Exception Handling</h3>
<ul>
<li>The view handles exceptions related to Google Ads API requests and returns a meaningful error message with a <code>500 Internal Server Error</code> status code if any error occurs.</li>
</ul>
<p>Below is the structured documentation for the <code>ReviveAdRecommendationView</code> class. This includes details about the class methods, inputs, outputs, and functionality, formatted for use as a comprehensive guide or API documentation.</p>
<hr>
<h2 id="revive-ad-recommendations">Revive-Ad-Recommendations</h2>
<h3 id="overview-13">Overview</h3>
<p>The <code>revive-ad-recommendations</code> is a Django REST Framework API view designed to generate recommendations for Google Ads campaigns based on performance data. It retrieves relevant ad metrics from the Google Ads API and generates insights and actionable steps to improve ad effectiveness.</p>
<h3 id="endpoint-2">Endpoint</h3>
<ul>
<li><strong>POST</strong> <code>/api/revive-ad-recommendations/</code></li>
</ul>
<h3 id="request-1">Request</h3>
<ul>
<li><strong>Method:</strong> <code>POST</code></li>
<li><strong>Headers:</strong>
<ul>
<li><code>Content-Type: application/json</code></li>
</ul>
</li>
<li><strong>Body:</strong> No request body is required.</li>
</ul>
<h3 id="response-5">Response</h3>
<ul>
<li>
<p><strong>Success Response:</strong></p>
<ul>
<li><strong>Status Code:</strong> <code>200 OK</code></li>
<li><strong>Body:</strong><pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">[</span>
  <span class="token punctuation">{</span>
    <span class="token string">"campaign_id"</span><span class="token punctuation">:</span> <span class="token string">"123456"</span><span class="token punctuation">,</span>
    <span class="token string">"campaign_name"</span><span class="token punctuation">:</span> <span class="token string">"Campaign Name"</span><span class="token punctuation">,</span>
    <span class="token string">"ad_group_id"</span><span class="token punctuation">:</span> <span class="token string">"789012"</span><span class="token punctuation">,</span>
    <span class="token string">"ad_group_name"</span><span class="token punctuation">:</span> <span class="token string">"Ad Group Name"</span><span class="token punctuation">,</span>
    <span class="token string">"ad_id"</span><span class="token punctuation">:</span> <span class="token string">"345678"</span><span class="token punctuation">,</span>
    <span class="token string">"ad_name"</span><span class="token punctuation">:</span> <span class="token string">"Ad Name"</span><span class="token punctuation">,</span>
    <span class="token string">"ad_status"</span><span class="token punctuation">:</span> <span class="token string">"ENABLED"</span><span class="token punctuation">,</span>
    <span class="token string">"clicks"</span><span class="token punctuation">:</span> <span class="token number">5</span><span class="token punctuation">,</span>
    <span class="token string">"impressions"</span><span class="token punctuation">:</span> <span class="token number">2000</span><span class="token punctuation">,</span>
    <span class="token string">"ctr"</span><span class="token punctuation">:</span> <span class="token number">0.0025</span><span class="token punctuation">,</span>
    <span class="token string">"cpa"</span><span class="token punctuation">:</span> <span class="token number">150.00</span><span class="token punctuation">,</span>
    <span class="token string">"recommendation"</span><span class="token punctuation">:</span> <span class="token string">"Low clicks with high impressions"</span><span class="token punctuation">,</span>
    <span class="token string">"action"</span><span class="token punctuation">:</span> <span class="token string">"Review ad copy and consider increasing bids"</span><span class="token punctuation">,</span>
    <span class="token string">"score"</span><span class="token punctuation">:</span> <span class="token number">10</span>
  <span class="token punctuation">}</span><span class="token punctuation">,</span>
  <span class="token operator">...</span>
<span class="token punctuation">]</span>
</code></pre>
</li>
<li><strong>Description:</strong> Returns a list of top advertising recommendations, sorted by their score.</li>
</ul>
</li>
<li>
<p><strong>Error Response:</strong></p>
<ul>
<li><strong>Status Code:</strong> <code>500 Internal Server Error</code></li>
<li><strong>Body:</strong><pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">{</span>
  <span class="token string">"error"</span><span class="token punctuation">:</span> <span class="token string">"Error message explaining what went wrong"</span>
<span class="token punctuation">}</span>
</code></pre>
</li>
<li><strong>Description:</strong> Returns an error message if there is an issue with generating recommendations or interacting with the Google Ads API.</li>
</ul>
</li>
</ul>
<h3 id="class-methods">Class Methods</h3>
<h4 id="postrequest-3"><code>post(request)</code></h4>
<ul>
<li><strong>Description:</strong> Handles <code>POST</code> requests to generate and return Google Ads recommendations.</li>
<li><strong>Parameters:</strong>
<ul>
<li><code>request</code>: The HTTP request object. No specific request body is required.</li>
</ul>
</li>
<li><strong>Returns:</strong> A JSON response containing the top recommendations or an error message.</li>
<li><strong>Error Handling:</strong> Catches <code>GoogleAdsException</code> and returns a <code>500 Internal Server Error</code> with a message.</li>
</ul>
<h4 id="get_google_ads_client-1"><code>get_google_ads_client()</code></h4>
<ul>
<li><strong>Description:</strong> Initializes and returns a <code>GoogleAdsClient</code> instance using the Google Ads configuration defined in a YAML file.</li>
<li><strong>Implementation:</strong>
<ul>
<li>Reads the Google Ads configuration from the YAML file specified in <code>settings.GOOGLE_ADS_YAML_PATH</code>.</li>
<li>Loads the client using the <code>GoogleAdsClient.load_from_dict()</code> method.</li>
</ul>
</li>
<li><strong>Returns:</strong> A configured instance of <code>GoogleAdsClient</code>.</li>
</ul>
<h4 id="generate_ad_recommendationsclient-customer_id"><code>generate_ad_recommendations(client, customer_id)</code></h4>
<ul>
<li><strong>Description:</strong> Retrieves ad performance data for a given customer from the Google Ads API and generates recommendations based on specified criteria.</li>
<li><strong>Parameters:</strong>
<ul>
<li><code>client</code>: An instance of <code>GoogleAdsClient</code> for making API requests.</li>
<li><code>customer_id</code>: The customer ID of the Google Ads account.</li>
</ul>
</li>
<li><strong>Returns:</strong> A list of recommendations based on ad performance data.</li>
<li><strong>Error Handling:</strong> If an error occurs while querying the API, a <code>GoogleAdsException</code> is raised and handled by the <code>post</code> method.</li>
</ul>
<h4 id="process_ad_rowrow"><code>process_ad_row(row)</code></h4>
<ul>
<li><strong>Description:</strong> Processes a single row of Google Ads performance data and generates a recommendation if applicable.</li>
<li><strong>Parameters:</strong>
<ul>
<li><code>row</code>: A row object containing campaign, ad group, ad, and performance metrics.</li>
</ul>
</li>
<li><strong>Returns:</strong> A structured recommendation dictionary if conditions are met, otherwise returns <code>None</code>.</li>
<li><strong>Logic:</strong>
<ul>
<li>Evaluates various performance metrics such as clicks, impressions, CTR (click-through rate), CPA (cost per acquisition), and ad status.</li>
<li>Generates recommendations based on the following conditions:
<ul>
<li><strong>Paused Ads:</strong> If the ad is paused, suggests reactivation and assigns a high priority score.</li>
<li><strong>Low Clicks/High Impressions:</strong> If the clicks are below a threshold and impressions are high, recommends reviewing the ad copy or adjusting bids.</li>
<li><strong>Low CTR:</strong> If the CTR is below 1%, suggests improving ad relevance and adjusting targeting.</li>
<li><strong>High CPA:</strong> If CPA is high (greater than 100), recommends optimizing for conversions.</li>
</ul>
</li>
</ul>
</li>
<li><strong>Returns:</strong> A structured dictionary containing the recommendation and related performance metrics.</li>
</ul>
<h4 id="create_ad_recommendationcampaign-ad_group-ad-clicks-impressions-ctr-cpa-status-recommendation-action-score"><code>create_ad_recommendation(campaign, ad_group, ad, clicks, impressions, ctr, cpa, status, recommendation, action, score)</code></h4>
<ul>
<li><strong>Description:</strong> Creates and structures a recommendation dictionary using the provided ad performance data and analysis.</li>
<li><strong>Parameters:</strong>
<ul>
<li><code>campaign</code>: The campaign object associated with the ad.</li>
<li><code>ad_group</code>: The ad group object associated with the ad.</li>
<li><code>ad</code>: The ad object.</li>
<li><code>clicks</code>: Number of clicks received by the ad.</li>
<li><code>impressions</code>: Number of impressions received by the ad.</li>
<li><code>ctr</code>: Click-through rate of the ad.</li>
<li><code>cpa</code>: Cost per acquisition for the ad.</li>
<li><code>status</code>: The status of the ad.</li>
<li><code>recommendation</code>: The recommendation message generated for the ad.</li>
<li><code>action</code>: Suggested action to improve ad performance.</li>
<li><code>score</code>: The score assigned to the recommendation based on performance metrics.</li>
</ul>
</li>
<li><strong>Returns:</strong> A dictionary containing the structured recommendation details.</li>
</ul>
<h4 id="get_top_recommendationsrecommendations-n20-1"><code>get_top_recommendations(recommendations, n=20)</code></h4>
<ul>
<li><strong>Description:</strong> Sorts the list of recommendations by their score and returns the top <code>n</code> recommendations.</li>
<li><strong>Parameters:</strong>
<ul>
<li><code>recommendations</code>: A list of recommendation dictionaries generated from <code>process_ad_row()</code>.</li>
<li><code>n</code>: Number of top recommendations to return. Default is 20.</li>
</ul>
</li>
<li><strong>Returns:</strong> A list of the top <code>n</code> recommendations, sorted in descending order by score.</li>
</ul>
<h3 id="example-usage-3">Example Usage</h3>
<ol>
<li>
<p><strong>Request:</strong></p>
<ul>
<li><strong>POST</strong> <code>/api/ad-recommendations/</code></li>
<li>No body is required.</li>
</ul>
</li>
<li>
<p><strong>Response:</strong></p>
<pre class=" language-json"><code class="prism  language-json"><span class="token punctuation">[</span>
  <span class="token punctuation">{</span>
    <span class="token string">"campaign_id"</span><span class="token punctuation">:</span> <span class="token string">"123456"</span><span class="token punctuation">,</span>
    <span class="token string">"campaign_name"</span><span class="token punctuation">:</span> <span class="token string">"Campaign Name"</span><span class="token punctuation">,</span>
    <span class="token string">"ad_group_id"</span><span class="token punctuation">:</span> <span class="token string">"789012"</span><span class="token punctuation">,</span>
    <span class="token string">"ad_group_name"</span><span class="token punctuation">:</span> <span class="token string">"Ad Group Name"</span><span class="token punctuation">,</span>
    <span class="token string">"ad_id"</span><span class="token punctuation">:</span> <span class="token string">"345678"</span><span class="token punctuation">,</span>
    <span class="token string">"ad_name"</span><span class="token punctuation">:</span> <span class="token string">"Ad Name"</span><span class="token punctuation">,</span>
    <span class="token string">"ad_status"</span><span class="token punctuation">:</span> <span class="token string">"ENABLED"</span><span class="token punctuation">,</span>
    <span class="token string">"clicks"</span><span class="token punctuation">:</span> <span class="token number">5</span><span class="token punctuation">,</span>
    <span class="token string">"impressions"</span><span class="token punctuation">:</span> <span class="token number">2000</span><span class="token punctuation">,</span>
    <span class="token string">"ctr"</span><span class="token punctuation">:</span> <span class="token number">0.0025</span><span class="token punctuation">,</span>
    <span class="token string">"cpa"</span><span class="token punctuation">:</span> <span class="token number">150.00</span><span class="token punctuation">,</span>
    <span class="token string">"recommendation"</span><span class="token punctuation">:</span> <span class="token string">"Low clicks with high impressions"</span><span class="token punctuation">,</span>
    <span class="token string">"action"</span><span class="token punctuation">:</span> <span class="token string">"Review ad copy and consider increasing bids"</span><span class="token punctuation">,</span>
    <span class="token string">"score"</span><span class="token punctuation">:</span> <span class="token number">10</span>
  <span class="token punctuation">}</span>
<span class="token punctuation">]</span>
</code></pre>
</li>
</ol>
<h3 id="error-handling-9">Error Handling</h3>
<ul>
<li>The view catches <code>GoogleAdsException</code> errors and returns a <code>500 Internal Server Error</code> with an error message detailing the issue.</li>
</ul>

    </div>
  </div>
</body>

</html>
