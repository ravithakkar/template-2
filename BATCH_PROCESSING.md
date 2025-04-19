# Anthropic Batch Processing Integration

InsightPulse uses Anthropic's Batch Processing API to efficiently process multiple alert queries in a cost-effective manner. This document explains how the system works and how to configure it.

## Benefits of Batch Processing

- **Cost Savings**: Batch processing is charged at 50% of the standard API price
- **Higher Throughput**: Process up to 100,000 messages in a single batch
- **Efficient Processing**: Perfect for alert systems that don't require immediate responses

## How It Works

1. **Request Collection**: Alert processing requests are collected in a queue
2. **Batch Triggering**: A batch is processed when either:
   - The queue size reaches the configured threshold (`ANTHROPIC_BATCH_SIZE`)
   - The maximum wait time is reached (`ANTHROPIC_BATCH_WAIT_MS`)
3. **Asynchronous Processing**: The system sends the batch to Anthropic's API and polls for completion
4. **Result Distribution**: When results are ready, they are distributed to the corresponding alerts

## Configuration

Configure batch processing through the following environment variables:

| Variable | Description | Default |
|----------|-------------|---------|
| `ANTHROPIC_USE_BATCH` | Enable or disable batch processing | `false` |
| `ANTHROPIC_MODEL` | The Claude model to use | `claude-3-7-sonnet-20250219` |
| `ANTHROPIC_BATCH_SIZE` | Number of requests to collect before processing | `20` |
| `ANTHROPIC_BATCH_WAIT_MS` | Maximum time to wait before processing a batch | `60000` (1 minute) |

## Enabling Batch Processing

To enable batch processing, set `ANTHROPIC_USE_BATCH=true` in your environment variables.

## Adjusting Batch Parameters

### Batch Size

The `ANTHROPIC_BATCH_SIZE` parameter controls how many requests are collected before a batch is automatically processed. A larger batch size is more cost-effective but may increase the wait time for individual alerts.

Recommended settings:
- Production: 50-100 requests
- Development: 5-10 requests

### Wait Time

The `ANTHROPIC_BATCH_WAIT_MS` parameter sets the maximum time (in milliseconds) to wait before processing a batch, even if it hasn't reached the size threshold.

Recommended settings:
- Production: 60000-300000 ms (1-5 minutes)
- Development: 10000-30000 ms (10-30 seconds)

## Implementation Notes

- In-memory storage is used for simplicity in the current implementation
- For production use, consider implementing a more robust storage solution:
  - Redis for temporary batch storage
  - Database for tracking batch status and results
- Error handling includes fallback to individual processing when batch processing fails

## Monitoring

Monitor batch processing performance by looking for these log messages:
- `Added request [ID] to batch queue. Current batch size: [SIZE]`
- `Processing batch of [SIZE] requests`
- `Created batch [ID] with [SIZE] requests`
- `Batch [ID] status: [STATUS], completed: [COMPLETED]/[TOTAL]`

## Cost Considerations

With batch processing enabled, you'll see approximately 50% cost reduction in Anthropic API usage. For example:

| API Usage | Standard Cost | Batch Cost |
|-----------|---------------|------------|
| 10,000 requests | $100 | $50 |
| 100,000 requests | $1,000 | $500 |

(Actual costs will vary based on token usage and model selection) 