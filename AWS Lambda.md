# AWS Lambda – Serverless Computing

A learning guide to understanding **AWS Lambda**, a serverless compute service provided by Amazon Web Services (AWS).

## 1. What is AWS Lambda?

AWS Lambda is a serverless computing service that allows developers to run code without managing or maintaining servers.

You upload your code, configure a trigger, and AWS Lambda automatically executes your function when an event occurs.

### Key Benefits

- **Serverless:** No need to manage servers or infrastructure.
- **Automatic Scaling:** Automatically scales based on incoming requests.
- **Event-Driven:** Executes code in response to events.
- **Pay-per-Use:** Pay based on requests and execution duration.
- **Multiple Runtimes:** Supports Python, Node.js, Java, and other programming languages.

## 2. How AWS Lambda Works

AWS Lambda follows an event-driven execution model.

1. An event occurs.
2. The event triggers a Lambda function.
3. Lambda executes the function.
4. The function processes the event.
5. The result is returned or sent to another AWS service.

**Example:**

When a user uploads an image to Amazon S3, a Lambda function can automatically resize the image and save the processed version.

## 3. Important AWS Lambda Components

| Component | Description |
|---|---|
| Function | The code executed by Lambda. |
| Trigger | An event that invokes the function. |
| Runtime | The programming language environment. |
| Execution Role | IAM permissions assigned to the function. |
| Event | Data passed to the function when invoked. |
| Concurrency | Number of function executions running simultaneously. |

## 4. Common AWS Lambda Triggers

| AWS Service | Purpose |
|---|---|
| Amazon S3 | Trigger when files are uploaded or modified. |
| API Gateway | Execute Lambda through HTTP API requests. |
| Amazon DynamoDB | React to database changes. |
| Amazon EventBridge | Execute scheduled or event-based functions. |
| Amazon SQS | Process messages from queues. |
| Amazon SNS | Respond to notifications. |

## 5. AWS Lambda vs Traditional Servers

| Feature | Traditional Servers | AWS Lambda |
|---|---|---|
| Server Management | Required | AWS managed |
| Scaling | Manual or configured | Automatic |
| Payment | Server running time | Requests and execution duration |
| Execution | Continuously running applications | Event-triggered functions |
| Infrastructure | Developer managed | AWS managed |

## 6. AWS Lambda Limitations

- Maximum execution time is 15 minutes per invocation.
- Cold starts can introduce additional execution latency.
- Requires proper IAM permissions.
- Not suitable for long-running processes.
- Memory and temporary storage have configurable limits.

## 7. Practical Use Cases

- Backend API development.
- Image and file processing.
- Automated scheduled tasks.
- Database event processing.
- Email and notification automation.
- Event-driven microservices.

## 8. Important Concepts

- **Cold Start:** Initial startup delay when Lambda creates a new execution environment.
- **Concurrency:** Number of function executions running simultaneously.
- **Invocation:** The process of executing a Lambda function.
- **Event Source:** A service or event that triggers a Lambda function.
- **IAM Role:** Defines what AWS resources a Lambda function can access.

## 9. Key Takeaway

AWS Lambda allows developers to focus on writing and executing code rather than managing infrastructure. It is particularly useful for building scalable, event-driven applications using a serverless architecture.

**Remember:** Serverless does not mean there are no servers. It means AWS manages the underlying infrastructure for you.

## 10. Official Learning Resources

- [AWS Lambda Documentation](https://docs.aws.amazon.com/lambda/)
- [AWS Lambda Getting Started](https://docs.aws.amazon.com/lambda/latest/dg/getting-started.html)
- [AWS Serverless Applications](https://aws.amazon.com/serverless/)
- [AWS Lambda Pricing](https://aws.amazon.com/lambda/pricing/)
