:warning: In progress

# Supply Chain Hack (version 0.1)

Supply Chain is a very broad topic with many facets of challenges. Each organization's supply chain is different, so its critical to understand the intricacies of each supply chain and its sub systems before recommending a solution.

It's impossible to cover every aspect of supply chain in a single hack or a single solution, so the tactical goal of this hack is to provide a high level introduction to supply chain risk management and some hands on approaches to solve them using both 1st party and 3rd party services.

## Prerequisites

- Check your participation confirmation email for credentials and postman collection files.
- Please use your internal subscription to provision the required resources.


## Challenge 1 - Supply Chain Visibility

### Introduction

Supply chains are complex systems made up of people, processes, and technology that deliver something of value to a customer. You depend on your suppliers to deliver the products and services you need, when you need them. And your customers are counting on you to meet their needs, too. Throughout the supply chain, risk management helps ensure that each company can deliver valuable products and services to their customers, even when things don’t go as planned.

For this challenge our goal is to determine our dependency on vendors and distributors with regards to the products we sell.  Is there a specific vendor/supplier and distributor that we are heavily reliant on.  Do we have any circumstances where we have only one vendor/supplier?  Are they clustered in one area of the country. To determine this, we can evaluate historical data that is captured in our ERP system. The ERP SQL Database and is comprised of 3 key tables:
- Product
    - This contains the finished beer product such as Mastika Saison, etc.
    - This is similar to the product header and also has 2 aggregated fields of ytdProfit and ytdRevenue that are updated based on historical sales information.
- Product Detail
    - This lists all of the bill of materials that go into the finished beer product.  
    - It also has 2 key fields of interest…  componentDistributor and componentSupplier.  This contains the CustomerID foreign keys to the Customer table
- Customer Table
    - This lists customers, suppliers, vendors and distributors.  

*Extra Credit - forecast/pipeline data* <BR>
All forecast data resides in Salesforce
- Opportunity
    - The key fields for this are amounts and the custom opportunity product field.  Hint: use this field to tie back to the ERP data
    - We only want data where the Opportunity Product is populated

### Success Criteria

- Build a Data Mart/ Data Warehouse/ Data Lakehouse/ Data Mesh in Azure with pipelines to ingest data from ERP or other SCRM datasources.

- Risk assessment dashboard(s)
    - Geo footprint (map view) of suppliers by product, by component.
    - Top components with single supplier, by product.
    - Top suppliers by product revenue and profit.

### Resources

- Azure Data Factory / Synapse Pipelines
    - https://docs.microsoft.com/en-us/azure/data-factory/copy-activity-overview
    - https://docs.microsoft.com/en-us/azure/data-factory/connector-salesforce 
- Databricks
    - https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-use-databricks-spark
- Synapse Serverless
    - https://docs.microsoft.com/en-us/azure/synapse-analytics/sql/on-demand-workspace-overview
- Power BI
    - https://docs.microsoft.com/en-us/power-bi/visuals/power-bi-map-tips-and-tricks 


## Challenge 2 - Supply Chain Risk Management (Walkthrough)

### Introduction

Now that you have identified a top component (for your product) with single source supplier risk. Lets visualize and mitigate this risk using the RAAD tool. Since this is a partner tool, we will do this challenge as a walkthrough.

### Success Criteria

- RAAD Tool Overview
    - Explore |> Map, Supply Chain Flow
    - Settings |> Assessment Setup
    - Dashboard |> Overall Risk Rating

- Mitigate Single Source Supplier Risk for your Product / Component.
    - Update Quality Source Status for your component to "Single Source"
    - Add New Supplier for your component
    - Update Quality Source Status for your component to "Multiple Sources"

- Review Risk Alerts 

- Create new Scenario for Geo Political / Climate Change Risk
    - Scenarios |> New Scenario
    - Scenarios |> Risk Assessement |> Guided
    - Scenarios |> Mitigation Plans |> New Mitigation Plan

### Resources

- https://raad360.com/

- https://appsource.microsoft.com/en-us/product/web-apps/raad360llc1584725322621.raad_core_1?tab=DetailsAndSupport

## Challenge 3 - Supply Chain Analytics

### Introduction

Now that we have know how to visualize and track the mitigation of risks, we will evaluate the Operational Risk of the new Supplier in Brazil using Forecasting. We will rely on public datasets available for this exercise to build a machine learning model which predicts the consumption in that local region and if the consumption is above a certain threshold, we will create an operational risk scenario and work on the mitigation plan.

### Success Criteria

- Build & deploy a forecasting model using [Sao Paulo Beer Consumption dataset](https://www.kaggle.com/dongeorge/beer-consumption-sao-paulo)

- Get weather forecast for next 7 days
    - Use [openweathermap.org](https://openweathermap.org/) or other weather api's
    - Lat = -22.135925
    - Lon = -51.4437573

- Generate consumption forecast for next 7 days using the ML model

### Resources
- https://docs.microsoft.com/en-us/azure/machine-learning/tutorial-automated-ml-forecast
- https://docs.microsoft.com/en-us/azure/synapse-analytics/machine-learning/tutorial-automl
- https://openweathermap.org/api/one-call-api
- https://docs.microsoft.com/en-us/power-bi/connect-data/service-aml-integrate