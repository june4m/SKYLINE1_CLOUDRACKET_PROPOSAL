---
title: "Proposal"
date: 2025-10-21T00:00:00Z
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Cloud Racket Platform
## A Unified AWS Serverless Solution for find player sport and court for you

### 1. Executive Summary
The Badminton Court Finder Platform is designed to help badminton players in Ho Chi Minh City easily search for, book, and manage courts in real time. The application is built entirely on an AWS Serverless architecture, integrating technologies such as AI-driven personalized recommendations, sentiment analysis from user reviews, and Google Maps API for locating the nearest courts. It also supports monthly revenue statistics for court owners.

### 2. Problem Statement
### What’s the Problem?
Currently, finding and booking badminton courts mainly relies on manual contact methods (phone or social media). Booking schedules are not updated in real time, and users lack visibility on court coverage and distance estimation. Meanwhile, court owners face difficulties in managing and arranging court schedules as well as generating efficient revenue reports.
### The Solution
This platform automates the entire process of searching, booking, and management for both users and court owners.
Users can find courts near their location using Amazon Location Service, view real-time availability through Amazon DynamoDB, and receive personalized recommendations via Amazon Personalize.
Court owners can register and update court information, receive automated booking confirmation emails through Amazon SES, and view revenue analytics on a custom dashboard built with AWS Amplify, Lambda, and Chart.js using data from DynamoDB/S3.
The web interface is hosted on AWS Amplify with Amazon Cognito handling user authentication.
### Benefits and Return on Investment
+ For Players: Easily find and book suitable courts within seconds, receive personalized recommendations based on behavior and location, and get automated confirmation emails. Court search time is reduced by 90% (from 30 minutes to 3 minutes), and booking confirmation time decreases from 2–24 hours to just 5 minutes.

+ For Court Owners: Automatically manage courts, schedules, and bookings via a centralized dashboard, reducing manual operations by 80%. The system provides visualized reports on revenue, booking frequency, and average ratings to support data-driven decisions.

+ For Developers: Fully serverless architecture ensures minimal operational cost (< $1/month initially, estimated $8–15/month after Free Tier). The system serves as both a practical solution and a valuable learning environment, providing real-world data for research in AI, Vietnamese NLP, and recommendation systems.

### 3. Solution Architecture
The platform adopts an AWS Serverless architecture for stable operations, scalability, and cost efficiency.
User, court, and booking data are stored in Amazon DynamoDB. Components communicate via Amazon API Gateway and AWS Lambda functions. The web and mobile interfaces are deployed on AWS Amplify, while Amazon Cognito ensures secure access control.
Amazon Personalize recommends courts based on user history, and Amazon Comprehend performs sentiment analysis on reviews. A Custom Dashboard visualizes operational data for both users and court owners.
All activities are monitored through Amazon CloudWatch and automated with Amazon EventBridge. 

![Cloud Racket Platform Architecture](/SKYLINE1_CLOUDRACKET_PROPOSAL/images/Proposal/Skyline1_CloudRacket.jpg)

### AWS Services Used
- **AWS Amplify Hosting**: Web/mobile hosting and deployment.

- **Amazon API Gateway**: Connects client and backend services. 

- **AWS Lambda**: Handles business logic and service integration.

- **Amazon DynamoDB**: Stores user, court, and booking data.

- **Amazon Cognito**: Manages authentication and authorization.

- **Amazon SES**: Sends automated booking and notification emails.

- **Amazon S3**: Stores court images and analytical data.

- **Amazon Personalize**: Provides personalized court recommendations.

- **Amazon Comprehend (Optional)**: Sentiment analysis on Vietnamese reviews to enhance overall ratings.

- **Amazon Location Service + DynamoDB GeoLib** : Finds nearby courts based on user location.

- **Custom Dashboard**: Built with AWS Amplify, AWS Lambda, and Chart.js for data visualization using DynamoDB/S3 data.

- **Amplify Admin UI (Admin Portal)**: Manages CRUD operations for courts, moderates reviews, and tracks logs.

- **Amplify CI/CD**: Automates deployment and updates.

- **Amazon CloudWatch**: Monitors logs, performance, and alerts.

- **Amazon EventBridge (Scheduler)**: Automates notifications and data cleanup.

- **AWS IAM  + WAF**: Security management, data encryption, and web attack prevention.

### Component Design
- **User Module**: Amazon Cognito manages registration, login, and profiles; user data (bookings, favorites, history) stored in DynamoDB.
- **Court Module**: Court owners manage court info and images; data stored in DynamoDB and S3; updates via API Gateway + Lambda.
- **Booking Flow**: API Gateway → Lambda → DynamoDB → SES handles booking, checks conflicts, and sends confirmation emails.
- **Recommendation System** : Amazon Personalize analyzes behavior and ratings to suggest courts (70% behavioral + 30% rating-based model).
- **Geo Search**: DynamoDB Geo Library or Amazon Location Service locates nearby courts; integrated with Google Maps for directions.
- **Admin Dashboard**: Visualizes revenue, bookings, and reviews using AWS Amplify + Chart.js, powered by DynamoDB/S3 data through Lambda.
- **Automation Layer**: EventBridge triggers scheduled Lambdas for reminders, retraining models, and data cleanup.


### 4. Technical Implementation
**Implementation Phases**
The project consists of 4 main phases:
- Research & Architecture Design: Develop AWS Serverless architecture diagram, define booking workflows and data flow (Week 1).
- Development & Testing: Build API Gateway + Lambda, integrate DynamoDB and Cognito, conduct functional testing (Weeks 2–3).
- Analytics Integration: Add Personalize recommendations and display analytics via Dashboard (Week 4).
- Deployment & Optimization: Use Amplify CI/CD for automated deployment; configure CloudWatch and EventBridge monitoring (Week 5).

**Technical Requirements**
- Frontend: ReactJS / Next.js (AWS Amplify Hosting)

- Backend: AWS Lambda (Node.js or Python) + Amazon API Gateway

- Database: Amazon DynamoDB (stores users, courts, bookings, ratings; supports Geo queries via DynamoDB Geo Library or AWS Location Service)

- AI Integration: Amazon Personalize (behavioral and rating-based court recommendations)

- Auth & Security: Amazon Cognito, AWS IAM, AWS KMS (encryption), AWS WAF (web protection)

- Email: Amazon SES (booking confirmation, notifications, reminders)

- Analytics: Custom Dashboard (Amplify + Lambda + Chart.js) visualizing DynamoDB/S3 data

- Automation: Amazon EventBridge (Scheduler) for reminders, retraining, and data cleanup

- Maps API: AWS Location Service or Google Maps/Places/Distance Matrix for nearby courts and navigation.
### 5. Timeline & Milestones
**Project Timeline**
Project Duration: 3 months (Internship Period)
Month 1 – Research & Preparation

+ Study AWS services (Amplify, Lambda, DynamoDB, Personalize, SES, Location Service).

+ Set up development environment and hardware configuration.

 Month 2 – System Design & Architecture

+ Design overall system architecture and define main modules.

+ Develop API schema, user roles (Cognito), and CI/CD pipeline.

+ Prepare sample datasets for Personalize and DynamoDB.

Month 3 – Implementation & Deployment

+ Week 1: Finalize architecture, define DynamoDB schema, implement API Gateway + Lambda.

+ Week 2: Develop backend and frontend (ReactJS/Next.js + Amplify Hosting).

+ Week 3: Integrate Amazon Personalize, SES, and Location Service.

+ Week 4: Conduct testing, optimize performance, and fully deploy on AWS Amplify.

### 6. Budget Estimation
You can find the budget estimation on the [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=621f38b12a1ef026842ba2ddfe46ff936ed4ab01).  
Or you can download the [Budget Estimation File](../attachments/budget_estimation.pdf).

### Infrastructure Costs
+ AWS Services:
    - AWS Amplify Hosting: Free Tier: 500 build mins, 5 GB served. After Free Tier: ~$0.01/min × 500 = $5.00/month
    - AWS Lambda: $0.00/month (20,000 requests/day, 128 MB, 200 ms average)
    - Amazon API Gateway: $0.00/month (600,000 requests/month, under Free Tier)
    - Amazon DynamoDB: $0.00/month (5 GB data, 100K read/write per day)
    - Amazon S3 (Image Storage): $0.12/month (10 GB storage, 5,000 GET/PUT requests)
    - Amazon SES (Email): $0.00/month (2,000 emails/month within Free Tier)
    - Amazon Personalize: Free for 2 months (20 GB data, 5 M interactions). After that: ~$8.00/month with batch inference (small dataset + retrain weekly).
    - Custom Dashboard (Amplify + Chart.js): $0.00/month (uses existing Amplify, data from S3/DynamoDB)
    - Amazon Location Service: $0.00/month (10,000 map requests, 1,000 location requests)
    - Amazon EventBridge (Scheduler): $0.00/month (10 trigger rules daily/hourly)
    - AWS IAM + WAF: $0.00/month (authentication, encryption, and basic security)

+ Total: $0.7/month, $8.40/12 months
    - Month 1: $0.12/month (All within Free Tier)
    - Month 2: $5.12/month (Personalize still in Free Tier, Amplify begins charging)
    - After Free Tier expires: $13.12/month, ≈ $157.44/year

### 7. Risk Assessment
#### Risk Matrix
    - Internet connectivity loss: Medium impact, medium probability
    - Unauthorized access: High impact, low probability
    - Budget overrun: Low impact, low probability
    - AI recommendation errors: Medium impact, low probability
#### Mitigation Strategies
- Network: Automatic retry on connection loss
- ecurity: Apply MFA via Cognito, WAF for attack prevention
- Cost: AWS Budgets alerts, optimize query frequency
- AI: Monitor and update Personalize model periodically
#### Contingency Plans
    - Allow temporary offline booking and sync when online
    - Rollback CodePipeline if deployment errors occur or costs exceed budget
### 8. Expected Outcomes
#### Technical Improvements: 
The application provides real-time court search and booking capabilities, personalized recommendations, and visual reports that optimize operations for both players and court owners.
#### Long-term Value
The platform can be expanded to other sports (tennis, basketball, gyms), serving as a framework template for smart sports solutions based on AWS Serverless and AI. Additionally, this is an ideal practice project for students or research groups wanting to apply AWS in developing intelligent systems.