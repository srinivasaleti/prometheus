# Prometheus Data Model

Prometheus stores data in a **time-series** format. Each data point represents the state of a system at a specific point in time, making it easy to track changes over time. Below are key components of the Prometheus data model:

## Key Concepts

### 1. **Time Series**
- **Definition:** A time series is a stream of timestamped values belonging to the same metric and labeled dimensions.
- **Structure:** Each time series is uniquely identified by a combination of a metric name and a set of labels (key-value pairs).
- **Example:** `http_requests_total{method="GET", handler="/api"}` where `http_requests_total` is the metric name and the labels describe the attributes of the time series.

### 2. **Metrics Types**
Prometheus supports four primary metric types:

- **Counter:**
  - A monotonically increasing value that represents the number of times something occurred.
  - Example: `http_requests_total` (counting the total number of HTTP requests).
  
- **Gauge:**
  - Represents a value that can go up or down, such as CPU usage or memory consumption.
  - Example: `memory_usage_bytes`.
  
- **Histogram:**
  - Measures the distribution of values (e.g., response times). It includes a count, sum, and a series of buckets representing value ranges.
  - Example: `http_request_duration_seconds`.
  
- **Summary:**
  - Similar to histograms but provides quantiles (e.g., 95th percentile of response time) for aggregated data.
  - Example: `http_request_latency_seconds`.

### 3. **Labels**
- **Labels** are key-value pairs associated with metrics that describe characteristics of the time series.
- **Purpose:** Labels enable filtering, grouping, and aggregating metrics. For example, a label can represent a data center, instance, or environment (`env="production"`, `instance="server-01"`).
- **Usage in Queries:** They are essential for PromQL queries, enabling fine-grained queries such as counting metrics for a specific endpoint or instance.

### 4. **Samples**
- **Definition:** A single data point in a time series, consisting of:
  1. **Timestamp:** When the value was recorded.
  2. **Value:** The observed value (e.g., the count of requests or CPU usage).
- Prometheus periodically samples metrics based on the scrape interval.

### 5. **Metric Name**
- **Metric names** describe what is being measured (e.g., `cpu_usage_seconds`, `http_requests_total`).
- **Naming Convention:** Metric names should be in lowercase and use underscores (`_`) to separate words. They should include a unit suffix when applicable (e.g., `_seconds`, `_bytes`).

## Example Time Series

Here’s an example time series for an HTTP request counter:
```
http_requests_total{method="GET", handler="/api", instance="server-01"}
```
In this case:
- **Metric Name:** `http_requests_total`
- **Labels:** 
  - `method="GET"`
  - `handler="/api"`
  - `instance="server-01"`
- **Sample:** 
  - A timestamp (e.g., `2024-09-23T14:00:00Z`)
  - A value (e.g., `1024` requests).
---

This data model allows Prometheus to efficiently scrape, store, and query large amounts of metrics over time.
