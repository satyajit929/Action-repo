GitHub Actions – CI/CD Pipeline with Webhook Integration

This repository demonstrates how to automate workflows using GitHub Actions, and trigger a webhook to notify or log events using Flask & MongoDB hosted on AWS EC2.

1) Technologies Used :

   a) GitHub Actions

   b) CI/CD Workflow (.github/workflows/webhook.yml)

   c) Python Webhook 

   d) MongoDB 

   e) AWS EC2

2) Repository Structure :

       action-repo/
       ├── .github/
       │   └── workflows/
       │       └── webhook.yml   # Main CI workflow triggering webhook
3) How It Works :

   a) The webhook.yml file defines a GitHub Actions workflow.

   b) It runs on push events.

   c) On every trigger, it sends a POST request to your deployed Flask webhook endpoint.

   d) That endpoint saves data in MongoDB Atlas.

4) webhook.yml Breakdown :

       yaml

       name: Webhook Trigger

       on:
          push:
               branches:
                       - main

       jobs:
           send-webhook:
                    runs-on: ubuntu-latest
                    steps:
                      - name: Send webhook to Flask server
                      run: |
                          curl -X POST http://<your-ec2-public-ip>:5000/webhook/receiver \
                          -H "Content-Type: application/json" \
                          -d '{"event":"GitHub push", "status":"success"}'
   Replace <your-ec2-public-ip> with your actual EC2 public IP or domain.

5) Features :
   
   a) Triggers automated webhook call on every GitHub push.

   b) Easily integratable with CI/CD, Slack, Discord, or internal systems.

   c) Great for monitoring, logging, or automating actions.

6) Use Cases :
   
   a) Track GitHub activity using your own webhook.

   b) Trigger backend scripts or tools from code events.

   c) Notify external systems (e.g., logging, alerting, deployment).

7) Deployment Steps :
   
   a) Create a webhook endpoint using Flask (see webhook-repo).

   b) Deploy the endpoint on AWS EC2 and open required port.

   c) Update webhook.yml with your endpoint URL.

   d) Push code to trigger the workflow and observe your webhook receiver.


