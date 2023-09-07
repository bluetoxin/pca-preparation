<h1>PCA Q&A</h1>
<details>
  <summary>1. What is the preferred approach used by Prometheus to collect metrics from a target?</summary>
  Pull-based
</details>
<details>
  <summary>2. What is RED Method?</summary>
  RED Method consists of: (Request) Rate + (Request) Errors + (Request) Duration
</details>
<details>
  <summary>3. What are the distinctions between SLO, SLI, and SLA?</summary>
  SLO (Service Level Objective) -> Goal<br>
  SLA (Service Level Agreement) -> Contract<br>
  SLI (Service Level Indicator) -> Metrics
</details>
<details>
  <summary>4. In the context of tracing, what is the meaning of a span?</summary>
  Span is a single operation of work within a distributed system 
</details>
<details>
  <summary>5. In which scenarios is tracing less beneficial?</summary>
  Monolith system
</details>
<details>
  <summary>6. Which type of data is monitored by Prometheus?</summary>
  Metrics (numeric value)
</details>
<details>
  <summary>7. What is one advantage of the push model for recording metrics compared to pull models?</summary>
  Time (real-time or near real-time)
</details>
<details>
  <summary>8. What are the 3 core components of observability?</summary>
  Logging, Trace and Metrics
</details>
<details>
  <summary>9. What is Telemetry?</summary>
  Process of collecting and transmitting data from remote sources to a central location
</details>
<details>
  <summary>10. What is the CLI utility tool for Prometheus called?</summary>
  Promtool
</details>
<details>
  <summary>11. Which property configures the timing to scrape metrics from targets?</summary>
  scrape_interval
</details>
<details>
  <summary>12. Which action in the label configuration is used to delete a specific target?</summary>
  scrape_configs -> relabel_configs -> action: drop
</details>
<details>
  <summary>13. How is managed data retention in prometheus?</summary>
  --storage.tsdb.retention.time<br>
  --storage.tsdb.retention.size
</details>
<details>
  <summary>14. What are the essential 3 components of Prometheus?</summary>
  Retrieval, TSDB, HTTP Server
</details>
<details>
  <summary>15. What are 3 methods to restart the Prometheus server?</summary>
  1. Sending a SIGHUP signal<br>
  2. Using the Prometheus API (method: POST/PUT) (path: /-/reload)<br>
  3. Using a service manager (systemctl) or orchestration tool (k8s)
</details>
<details>
  <summary>16. What HTTP method does Prometheus employ for performing scrapes?</summary>
  HTTP GET method
</details>
<details>
  <summary>17. Which SD configuration is recommended for nodes of Elastic Kubernetes Service on AWS?</summary>
  ec2_sd_configs
</details>
<details>
  <summary>18. Which type of database does Prometheus utilize?</summary>
  Time-series database
</details>
<details>
  <summary>19. Which query below will give the 99% quantile of the metric http_requests_total</summary>
  histogram_quantile(0.99, http_requests_total_bucket)
</details>
<details>
  <summary>20. What component is responsible for collecting metrics from an instance and exposing them in a format that Prometheus expects?</summary>
  *-exporter
</details>
<details>
  <summary>21. Which component is suitable for collecting metrics from batch/cron jobs?</summary>
  Pushgateway
</details>
<details>
  <summary>22. When is the configuration option "honor_labels:true" used?</summary>
  "honor_labels" controls how Prometheus handles conflicts between labels that are already present in scraped data. "honor_labels:true" is usually used in conjuction with PushGateway. 
</details>
<details>
  <summary>23. What is the purpose of port 9090/9093/9100/9091/9115 in Prometheus?</summary>
  9090 -> Prometheus itself<br>
  9093 -> Alertmanager<br>
  9100 -> Node Exporter<br>
  9091 -> Pushgateway<br>
  9115 -> BlackBox Exporter
</details>
<details>
  <summary>24. What are 2 default metric labels?</summary>
  "instance" and "job"
</details>
<details>
  <summary>25. Which of the file systems is recommended/supported by Prometheus?</summary>
  ext4, XFS, and NTFS
</details>
<details>
  <summary>26. What is the agent deployment mode of Prometheus?</summary>
  Lightweight mode for device with low compute power (IoT) 
</details>
<details>
  <summary>27. Which CLI command is suitable for unit testing Prometheus rules?</summary>
  promtool test rules file.yml
</details>
<details>
  <summary>28. Which CLI command is suitable for checking validity of the config files?</summary>
  promtool check rules file.yml
</details>
<details>
  <summary>29. How do you define the targets with SD that Prometheus should collect metrics from?</summary>
  scrape_configs and *_sd_configs on per-job basis
</details>
<details>
  <summary>30. How can you delete the specific time series metrics of Prometheus?</summary>
  First, start the Prometheus with "Admin API" enabled. Flag: <code>--web.enable-admin-api</code>. Then, send a request:<br>
  <code>curl -XPOST -g 'http://localhost:9090/api/v1/admin/tsdb/delete_series?match[]={__name__="node_memory_MemAvailable_bytes", instance="node01:9100", job="pythonhost"}'</code>
</details>
<details>
  <summary>31. How can you clean disk?</summary>
  First, start the Prometheus with "Admin API" enabled. Flag: <code>--web.enable-admin-api</code>. Then, send a request:<br>
  <code>curl -XPOST -g 'http://localhost:9090/api/v1/admin/tsdb/clean_tombstones'</code>
</details>
<details>
  <summary>32. Which 4 data types are used in PromQL?</summary>
  Scalar, String (deprecated), Instant Vector, Range Vector
</details>
<details>
  <summary>33. Which PromQL function is used to estimate the value of a time series at a future time</summary>
  predict-linear
</details>
<details>
  <summary>34. Which function can be used to calculate the average of a range vector in Prometheus?</summary>
  avg_over_time(metrics[x])
</details>
<details>
  <summary>35. What does the term "offset" refer to in Prometheus?</summary>
  offset refers to the past time as duration
</details>
<details>
  <summary>36. What distinguishes the rate(...) and irate(...) query functions in Prometheus?</summary>
  rate(...) calc avg rate of change of a time series over the specified time range, irate(...) calc avg rate of change of a time series at the last 2 data points
</details>
<details>
  <summary>37. What distinguishes the rate(...) and deriv(...) query functions in Prometheus?</summary>
  deriv(...) operates on gauge and rate(...) operates on counter
</details>
<details>
  <summary>38. Which type of metric is suitable for measuring the internal temperature of a server?</summary>
  guage
</details>
<details>
  <summary>39. How many unique series are generated by a histogram metric type?</summary>
  *_bucket, *_sum and *_count
</details>
<details>
  <summary>40. What are the 4 components of the Prometheus metrics data model?</summary>
  metric name, metrics label, timestamp, value
</details>
<details>
  <summary>41. What is the difference between the ceil and floor functions?</summary>
  floor(...) = round a number down, ceil(...) = round a number up
</details>
<details>
  <summary>42. What is the group modifiers?</summary>
  a part of vector matching. on, ignoring + group_left, group_right
</details>
<details>
  <summary>43. What is the dimensional aggregation?</summary>
  sum(), min(), max(), avg(), count()
</details>
<details>
  <summary>44. What is the significance of the double underscore "__" before a label name?</summary>
  The label is a reserved label
</details>
<details>
  <summary>45. Which of the following is not a valid time value to be used in a range selector: <code>2y, 1h15m, 2mo, 200ms, 4w</code></summary>
  2mo
</details>
<details>
  <summary>46. What is the HTTP headers to establish by Prometheus during each scrape?</summary>
  X-Prometheus-Scrape-Timeout-Seconds
</details>
<details>
  <summary>47. Which 2 query parameters are required when configuring a Blackbox Exporter probe?</summary>
  target and module
</details>
<details>
  <summary>48. Where is the version of the Prometheus exporter typically defined?</summary>
  build_info
</details>
<details>
  <summary>49. What is the most suitable exporter for monitoring an HTTP web server endpoint to verify that it returns a 200 status code?</summary>
  Blackbox Exporter
</details>
<details>
  <summary>50. Which Prometheus exporter is recommended for monitoring network devices?</summary>
  SNMP exporter
</details>
<details>
  <summary>51. How to change scrape path?</summary>
  scrape_configs > metrics_path: /metrics
</details>
<details>
  <summary>52. In a scenario where you have a dynamic etcd database containing scrape targets for Prometheus, how should you configure service discovery?</summary>
  file_sd_configs
</details>
<details>
  <summary>53. What are the 2 types of attributes that can be present in the /metrics endpoint?</summary>
  HELP, TYPE
</details>
<details>
  <summary>54. Is there a way to deactivate a specific route in Alertmanager for a specific time frame?</summary>
  time_intervals
</details>
<details>
  <summary>55. What is the good naming convention for the recoring rules?</summary>
  level:metric:operations
</details>
<details>
  <summary>56. What are the 3 statuses of a Prometheus alert?</summary>
  firing, pending, inactive
</details>
<details>
  <summary>57. Which feature of Alertmanager is responsible for formatting and customizing the alerts?</summary>
  notification templates
</details>
<details>
  <summary>58.  What does the term "inhibiting" refer to in the context of Alertmanager?</summary>
  Inhibiting refers to a feature that allows certain alerts to be stopped or prevented from generating notifications
</details>
<details>
<summary>59. What is the significance of the <code>for</code> attribute in a Prometheus alert rule?</summary>
<code>for</code> allows for a delay or threshold before an alert is firing
</details>
<details>
  <summary>60. How can you temporarily mute/snooze/suppress an alert during maintenance in Prometheus?</summary>
  Slience
</details>
<details>
  <summary>61. What is the name of Prometheus native dashboarding and visualization feature?</summary>
  Prometheus Console
</details>
<details>
  <summary>62. How can you coordinate the simultaneous sending of multiple alerts with similar label sets in Prometheus?</summary>
  Grouping
</details>
<details>
<summary>63. What is the purpose of the <code>conitnue</code> attribute in an Alertmanager route configuration?</summary>
  continue: specifies whether to continue processing subsequent routes after sending a notification for an alert
</details>
<details>
  <summary>64. Which 2 attributes of an alerting rule can be used to include extra metadata?</summary>
  annotations and labels
</details>
<details>

<summary>65. What does this <code>relabel_configs</code> do?
<pre><code>relabel_configs:
  - source_labels: [team]
    regex: frontend
    action: drop
</pre></code>
</summary>
Prometheus won’t scrape targets with a label of team: frontend
</details>
<details>
  <summary>66. What is definition of a metric</summary>
   A numeric measurement (“A numeric measurement made over time” is incorrect as this is the definition of a time series)
</details>
<details>
<summary>67. Which one of these <b>label values</b> is <b>incorrect</b>: <code>val</code>, <code>label-value-1</code>, <code>2nd_label_value</code>, <code>$__maybe_valid</code>?</summary>
  Unlike label names, there is no restriction that label values cannot start with a number, dollar sign. Even emojis are valid for use in Prometheus labels since they are Unicode-encoded
</details>
<details>
<summary>68. What query will return the currently firing alerts in Alertmanager?</summary>
  No such query exists
</details>
<details>
<summary>69. Let a Node Exporter scrape job be denoted by the label <code>job="node"</code>. Let there be two static instances for this job, <code>instance="node1"</code> and <code>instance="node2"</code>. Which queries returns a <code>1</code> when both nodes are currently being scraped successfully and a <code>0</code> otherwise?</summary>
<code>min(up{job="node"})</code>
</details>
<details>
<summary>70. You are instrumenting an application called <b>agate</b> for Prometheus. This application has a subsystem called <b>remed</b> that handles automated script-based remediations. You want to define a metric that gives the number of remediation <b>processes</b> currently <b>running</b>. What is the most appropriate “fully-qualified” metric name?</summary>
agate_remed_processes_running
</details>
<details>
  <summary>70. Is symptom or cause correspond to consumer-visible issues?
</summary>
  symptom
</details>
<details>
  <summary>71. What can be used to drop specific targets from a scrape?</summary>
  <code>relabel_configs</code> with action <code>keep</code>
</details>
<details>
  <summary>72. What method of service discovery is BEST for identifying Kubernetes pods to scrape?</summary>
  kubernetes_sd_configs
</details>
<details>
  <summary>73. You are instrumenting an HTTP API with Prometheus metrics. You want to define a metric that tracks the latency of HTTP requests made to your API. You only care about the <b>average latency</b> and do not have a need for percentiles.
Which of the following metric names and types is the MOST appropriate for this scenario?</summary>
http_request_duration_seconds, Summary
</details>
<details>
<summary>74. Let <b>cert_expiry</b> be a <b>gauge</b> metric whose value is a Unix timestamp (epoch time) representing the time a given certificate will expire.
Which of the following queries gives the time in days until certificate expiration?</summary>
(cert_expiry – time()) / 86400
</details>
<details>
  <summary>75. Which of the following is NOT a best practice when it comes to writing a Prometheus exporter?</summary>
  Include a version label on all exported metrics. This is not a best practice as it is recommend to use a designated build_info metric with a version label and dynamically attach it via PromQL grouping as-needed.
</details>
<details>
  <summary>76. What configuration is used to effectively disable grouping of alerts for a particular Alertmanager route?</summary>
  group_by: ['...']
</details>
<details>
  <summary>77. Does summary or histogram  metrics generally cannot be aggregated?</summary>
  Summary metrics generally cannot be aggregated. Summaries do not expose bucketed observations since evaluation happens on the client side.
</details>
<details>
  <summary>78. What is a Service Level Indicator (SLI)?</summary>
  A <b>quantitative</b> measure of some aspect of the level of service that is provided
</details>
<details>
  <summary>79. Which of the following queries contains a temporal aggregation: <code>avg</code>, <code>avg_over_time</code>?</summary>
  <code>avg_over_time(up[5m])</code> is the correct answer. Temporal aggregations are time-based. <code>avg by (instance) (up)</code> is incorrect as this query contains a dimensional aggregation (label-based)
</details>
