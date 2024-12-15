# GitHub Contributions Integration: Proof of Developer Activity

## Overview

This project integrates GitHub's public APIs into the zkPass ecosystem to provide **verifiable proof of contributions or activities** while preserving user privacy. This can be used for open-source validation, hackathon submissions, or developer incentives.

## Problem Statement

Proving activity or contributions on platforms like GitHub often requires sharing extensive logs or sensitive repository details. Our schema leverages zero-knowledge proofs to validate specific events or contributions without exposing unrelated or private data.

## Features

- Verifies specific GitHub events, such as pushes or repository activity.
- Preserves privacy with zkTLS and zero-knowledge proofs.
- Compatible with public GitHub APIs, ensuring easy integration.

## Use Case

Open-source programs, hackathons, and recruiters can validate contributions to specific repositories or activities without compromising a developer’s privacy.

## Integration Details

### Data Source

**GitHub**: The integration uses publicly accessible GitHub APIs to fetch user activity logs.

### API Details

- **Endpoint**: `https://api.github.com/users/{username}/events`
- **Data Points**:
  - Event Type (e.g., PushEvent, ForkEvent)
  - Repository Name
  - Event ID

### Schema Configuration

```json
{
  "issuer": "GitHub",
  "desc": "Verify contributions or activity on GitHub without exposing private repository details.",
  "website": "https://api.github.com",
  "APIs": [
    {
      "host": "api.github.com",
      "intercept": {
        "url": "/users/{username}/events",
        "method": "GET",
        "query": [],
        "header": []
      },
      "assert": [
        {
          "key": "type",
          "value": "PushEvent",
          "operation": "="
        },
        {
          "key": "repo.name",
          "value": "<SPECIFIC_REPO>",
          "operation": "contains"
        }
      ],
      "nullifier": "id"
    }
  ],
  "HRCondition": ["Made a Push Event to the Specified Repository"],
  "tips": {
    "message": "Enter your GitHub username to retrieve and verify your activity log."
  }
}
```

## Workflow

1. **User Authentication**: Users provide their GitHub username to fetch public activity data.
2. **Data Interception**: The schema uses the GitHub API to retrieve the user’s activity log.
3. **Zero-Knowledge Verification**: zkPass verifies specific events (e.g., pushes to a repository) without exposing sensitive details.
4. **Validation**: The verified proof is used for validation or rewards programs.

## Resources

- [GitHub API Documentation](https://docs.github.com/en/rest)
- [zkPass Developer Guide](https://zkpass.org/developer-guide)
- [Zero-Knowledge Proofs Overview](https://zkpass.org/zkp-overview)

## **Contact**

For inquiries or feedback, feel free to reach out:

**Team Name:** zkVerse
**Project Lead:** Karan Kumar Das  
**Email:** karankr.das.cse22@iitbhu.ac.in

---

By integrating GitHub contributions with zkPass, this project enhances trust and validation in developer ecosystems while prioritizing user privacy.
