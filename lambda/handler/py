import json
import boto3
from datetime import datetime

# Initialize the CloudWatch client
cloudwatch = boto3.client('cloudwatch')

def lambda_handler(event, context):
    """
    AWS Lambda entry point.
    Expects event JSON with keys 'error_rate' (float) and/or 'LatencyMs' (int).
    Sends custom metrics to CloudWatch under the 'MyService' namespace.
    """
    ts = datetime.utcnow()  # current timestamp in UTC
    metric_data = []

    # If the event includes an error_rate, add that metric
    if 'error_rate' in event:
        metric_data.append({
            'MetricName': 'ErrorRate',
            'Timestamp': ts,
            'Value': event['error_rate'],
            'Unit': 'Percent'
        })

    # If the event includes a latency measurement, add that too
    if 'LatencyMs' in event:
        metric_data.append({
            'MetricName': 'LatencyMs',
            'Timestamp': ts,
            'Value': event['LatencyMs'],
            'Unit': 'Milliseconds'
        })

    # Push the metrics to CloudWatch
    cloudwatch.put_metric_data(
        Namespace='MyService',
        MetricData=metric_data
    )

    # Return a simple success response
    return {
        'statusCode': 200,
        'body': json.dumps(f"Recorded {len(metric_data)} metrics")
    }
