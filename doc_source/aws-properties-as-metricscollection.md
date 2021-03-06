# Amazon EC2 Auto Scaling AutoScalingGroup MetricsCollection<a name="aws-properties-as-metricscollection"></a>

The `MetricsCollection` is a property of the [AWS::AutoScaling::AutoScalingGroup](aws-properties-as-group.md) resource that describes the group metrics that an Amazon EC2 Auto Scaling group sends to Amazon CloudWatch\. These metrics describe the group rather than any of its instances\. For more information, see [EnableMetricsCollection](https://docs.aws.amazon.com/autoscaling/ec2/APIReference/API_EnableMetricsCollection.html) in the *Amazon EC2 Auto Scaling API Reference*\.

## Syntax<a name="w2922ab1c21c10c38c13c42b5"></a>

### JSON<a name="aws-properties-as-metricscollection-syntax.json"></a>

```
{
  "[Granularity](#cfn-as-metricscollection-granularity)" : String,
  "[Metrics](#cfn-as-metricscollection-metrics)" : [ String, ... ]
}
```

### YAML<a name="aws-properties-as-metricscollection-syntax.yaml"></a>

```
[Granularity](#cfn-as-metricscollection-granularity): String
[Metrics](#cfn-as-metricscollection-metrics):
  - String
```

## Properties<a name="w2922ab1c21c10c38c13c42b7"></a>

`Granularity`  <a name="cfn-as-metricscollection-granularity"></a>
The frequency at which Amazon EC2 Auto Scaling sends aggregated data to CloudWatch\. The only valid value is `1Minute`\.  
*Required*: Yes  
*Type*: String

`Metrics`  <a name="cfn-as-metricscollection-metrics"></a>
The list of metrics to collect\. If you don't specify any metrics, all metrics are enabled\.  
*Required*: No  
*Type*: List of String values