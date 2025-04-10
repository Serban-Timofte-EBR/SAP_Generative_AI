# Developing Basic Prompts for Common Queries

## Business Scenario

**Identify the Facility Management Scenario**

Facility Solutions Company is a premier provider of comprehensive facility management, maintenance, and cleaning services tailored for both residential and commercial properties. Their mission is to ensure that your environment remains safe, efficient, and impeccably maintained, allowing you to focus on your core activities without the hassle of facility upkeep.

Their target markets are luxury residential complexes, apartments, and individual homes. They also serve commercial Properties like office buildings, retail spaces, industrial facilities, and educational institutions.

**Business Problem:**

Facility solutions company receives thousands of mails pertaining to customers’ requests, complaints, and other messages. The company maintains internal applications to address customer requests and complaints and prioritize them to address these requests in a timely and correct manner.

However, categorizing these mails include manual process to transfer data from mails to internal applications, categorizing, and then prioritizing these tasks.

They turn towards generative AI hub to address this problem.

We will provide stepwise solutions to this problem in this learning journey.

**Solving the Problem:**

1. Develop basic prompt

We'll start with a basic prompt and then develop the prompt, finding an output that can be used by application within the company.

The first prompt is:

```python
Giving the following message:
---
Subject: Urgent HVAC System Repair Needed

Dear Support Team,

I hope this message finds you well. My name is [Sender], and I am reaching out to you from [Residential Complex Name], where I have been residing for the past few years. I have always appreciated the meticulous care and attention your team provides in maintaining our facilities.

However, I am currently facing a pressing issue with the HVAC system in my apartment. Over the past few days, the system has been malfunctioning, resulting in inconsistent temperatures and, at times, complete shutdowns. Given the current weather conditions, this has become quite unbearable and is affecting my daily routine significantly.

I have attempted to troubleshoot the problem by resetting the system and checking the thermostat settings, but these efforts have not yielded any improvement. The situation seems to be beyond my control and requires professional intervention.

I kindly request that a repair team be dispatched immediately to address this urgent issue. The urgency of the matter cannot be overstated, as it is impacting not only my comfort but also my ability to carry out daily activities effectively.

Thank you for your prompt attention to this matter. I look forward to your swift response and resolution.

Best regards,
[Sender]
---
Your task is to extract
- urgency
- sentiment
"
```

- Open-source LLMs reduce costs, offer transparency and allow customization

2. Assign values to urgency and sentiment

We will now assign some basic urgency and sentiment values and execute the prompt.

```python
Giving the following message:
---
Subject: Urgent HVAC System Repair Needed

Dear Support Team,

I hope this message finds you well. My name is [Sender], and I am reaching out to you from [Residential Complex Name], where I have been residing for the past few years. I have always appreciated the meticulous care and attention your team provides in maintaining our facilities.

However, I am currently facing a pressing issue with the HVAC system in my apartment. Over the past few days, the system has been malfunctioning, resulting in inconsistent temperatures and, at times, complete shutdowns. Given the current weather conditions, this has become quite unbearable and is affecting my daily routine significantly.

I have attempted to troubleshoot the problem by resetting the system and checking the thermostat settings, but these efforts have not yielded any improvement. The situation seems to be beyond my control and requires professional intervention.

I kindly request that a repair team be dispatched immediately to address this urgent issue. The urgency of the matter cannot be overstated, as it is impacting not only my comfort but also my ability to carry out daily activities effectively.

Thank you for your prompt attention to this matter. I look forward to your swift response and resolution.

Best regards,
[Sender]
---
Your task is to extract:
- "urgency" as one of `low`, `medium`, `high`
- "sentiment" as one of `positive`, `neutral`, `negative`
```

3. Generate JSON output

We need the output of these values in a format that can be used as an input for a software. We decide to use the JSON output.

JSON offers a simple, language-independent, and lightweight solution for efficient data exchange. It can handle complex structures while remaining easy to parse and generate. JSON's widespread use in APIs and web services ensures interoperability, reduces bandwidth and storage requirements, and simplifies the development process.

```python
Giving the following message:
---
Subject: Urgent HVAC System Repair Needed

Dear Support Team,

I hope this message finds you well. My name is [Sender], and I am reaching out to you from [Residential Complex Name], where I have been residing for the past few years. I have always appreciated the meticulous care and attention your team provides in maintaining our facilities.

However, I am currently facing a pressing issue with the HVAC system in my apartment. Over the past few days, the system has been malfunctioning, resulting in inconsistent temperatures and, at times, complete shutdowns. Given the current weather conditions, this has become quite unbearable and is affecting my daily routine significantly.

I have attempted to troubleshoot the problem by resetting the system and checking the thermostat settings, but these efforts have not yielded any improvement. The situation seems to be beyond my control and requires professional intervention.

I kindly request that a repair team be dispatched immediately to address this urgent issue. The urgency of the matter cannot be overstated, as it is impacting not only my comfort but also my ability to carry out daily activities effectively.

Thank you for your prompt attention to this matter. I look forward to your swift response and resolution.

Best regards,
[Sender]
---
Extract and return a json with the following keys and values:
- "urgency" as one of `low`, `medium`, `high`
- "sentiment" as one of `positive`, `neutral`, `negative`
Your complete message should be a valid json string that can be read directly and only contain the keys mentioned in the list above. / Your complete message should be a valid json string that can be read directly and only contain the keys mentioned in the list above. Never enclose it in ```json...```, no newlines, no unnecessary whitespaces.
```

4. Improve the prompt

- Assign a list best matching support category tags to the message: `facility_management_issues`, `cleaning_services_scheduling`, `general_inquiries`, `specialized_cleaning_services`, `routine_maintenance_requests`, `emergency_repair_services`, `sustainability_and_environmental_practices`, `training_and_support_requests`, `quality_and_safety_concerns`, `customer_feedback_and_complaints`

- Example of proper return requirements

```python
Extract and return a json with the following keys and values:
- "urgency" as one of `low`, `medium`, `high`
- "sentiment" as one of `positive`, `neutral`, `negative`
- "categories" list of the best matching support category tags from: `facility_management_issues`, `cleaning_services_scheduling`, `general_inquiries`, `specialized_cleaning_services`, `routine_maintenance_requests`, `emergency_repair_services`, `sustainability_and_environmental_practices`, `training_and_support_requests`, `quality_and_safety_concerns`, `customer_feedback_and_complaints`
Your complete message should be a valid json string that can be read directly and only contain the keys mentioned in the list above. Never enclose it in ```json...```, no newlines, no unnecessary whitespaces.
```