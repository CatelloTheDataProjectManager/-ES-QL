# ES|QL (Elasticsearch SQL)

<img src="https://github.com/CatelloTheDataProjectManager/Elasticsearch/blob/main/elasticsearch.png" alt="Elasticsearch" width="250"/>

*****Throughout my professional career, I have implemented new data extraction solutions in various companies to address the rapid growth of data. The existing systems often struggled to handle the increasing volume and complexity of information. By adopting these new solutions, I have been able to enhance data management practices, improve query performance, and achieve more robust analytics capabilities. These upgrades have enabled more effective data extraction, processing, and analysis, ultimately driving better business insights and supporting the evolving needs of the organizations.*****

## Overview of My Skills

This document highlights my expertise in using ES|QL (Elasticsearch SQL) to analyze and manipulate large-scale data, along with my experience in the Elasticsearch and Kibana ecosystem.

### 1. **Proficiency in ES|QL**
- Expertise in executing SQL queries on Elasticsearch indices, simplifying data analysis with familiar SQL syntax.
- Skilled in leveraging processing commands such as:
  - **`from`**: Retrieving documents from data streams or indices.
  - **`where`**: Filtering data based on specific conditions.
  - **`eval`**: Creating and manipulating calculated columns.
  - **`rename`**: Renaming fields for clarity and standardization.

### 2. **Advanced Data Transformation**
- Applying transformations like **`dissect`** and **`grok`** to extract complex information from strings.
- Utilizing aggregations such as **`stats...by`** to group and synthesize large datasets.
- Expertise with **`auto_bucket`** for generating dynamic histograms.

```ESQL
from kibana_sample_data_flights
| where FlightDelay
| keep Carrier, FlightNum, DistanceMiles, FlightDelayMin
| eval distance_buckets = auto_bucket(DistanceMiles, 20, 0, 20000)
| stats delay = sum(FlightDelayMin) by distance_buckets, Carrier
| sort Carrier
```

### 3. **Data Enrichment**
- Creating and managing enrichment policies to add metadata from external indices in real-time.
- Seamlessly integrating enrichments into query pipelines for efficient result enhancement.

### 4. **Data Ingestion and Structuring**
- Configuring mappings to structure data according to analytical needs.
- Ingesting large volumes of data using APIs like **_bulk** to optimize performance.

```ESQL
PUT products
    {
        "mappings": {
            "properties": {
            "product_name": {
                "type": "keyword"
            },
            "price": {
                "type": "double"
            }
            }
        }
    }

POST products/_bulk
    {"index": {"_id": "1"}}
    {"name": "apple", "price": 3.50}
    {"index": {"_id": "2"}}
    {"name": "orange", "price": 2.50}
    {"index": {"_id": "3"}}
    {"name": "pineapple", "price": 5.50}
    {"index": {"_id": "4"}}
    {"name": "watermelon", "price": 8.50}

PUT _enrich/policy/enrich-orders-with-price
    {
        "match": {
            "indices": "products",
            "match_field": "name",
            "enrich_fields": [
                "price"
            ]
        }
    }

POST _enrich/policy/enrich-orders-with-price/_execute
```

### 5. **Visualization and Exploration in Kibana**
- Proficient in using **Kibana Discover** for interactive data exploration and visualization.
- Saving and reusing ES|QL queries in Kibana to create custom dashboards.
- Building powerful visualizations by combining ES|QL with advanced Kibana features.

![kibana_image](https://github.com/CatelloTheDataProjectManager/Elasticsearch/blob/main/image_kibana.png)

### 6. **Big Data Project Management**
- Integrating ES|QL into complex analytical pipelines to address Big Data use cases, such as log analysis, performance monitoring, and anomaly detection.
- Optimizing query and transformation performance to handle large-scale datasets efficiently.

---

## Why Choose ES|QL?
ES|QL is a powerful tool that combines the familiarity of SQL with the flexibility of Elasticsearch. With my expertise, I can leverage its features to:
- Quickly meet data analysis needs.
- Build robust ingestion and enrichment pipelines.
- Create meaningful visualizations that drive better decision-making.
