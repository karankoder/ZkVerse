# LeetCode Profiles Integration Schema

## Project Overview

This project integrates **LeetCode Profiles** into the zkPass ecosystem, enabling users to verify their programming competency without exposing their entire profile. By leveraging zkPass’s zkTLS technology, users can securely share proof of their programming achievements (such as contest rankings, problem-solving stats, or badges) with third parties, maintaining complete privacy and security.

## Features

- **Privacy-Preserving Verification**: Users can share proof of specific achievements without revealing their full LeetCode profile.
- **Customizable Verification**: Choose what data (e.g., problem-solving stats, contest ratings, or badges) to verify based on third-party requirements.
- **Ease of Integration**: Built using zkPass schema standards, ensuring seamless integration with the zkPass infrastructure.

## Schema Details

```json
{
  "issuer": "LeetCode",
  "desc": "Verify programming achievements and competency securely using LeetCode profile data.",
  "website": "https://leetcode.com/",
  "APIs": [
    {
      "host": "leetcode.com",
      "intercept": {
        "url": "/api/user/profile",
        "method": "GET",
        "query": [
          {
            "q": "userName",
            "verify": true
          }
        ]
      },
      "assert": [
        {
          "key": "data|user|contestRank",
          "value": "<5000",
          "operation": "<"
        },
        {
          "key": "data|user|totalSolved",
          "value": ">300",
          "operation": ">"
        }
      ],
      "nullifier": "data|user|userId"
    }
  ],
  "HRCondition": [
    "Top 5k in LeetCode contests",
    "Solved more than 300 problems"
  ],
  "tips": {
    "message": "Please log in to your LeetCode account and allow verification to begin."
  }
}
```

### Key Fields in the Schema

- **issuer**: "LeetCode", the source of the data.
- **desc**: Explains the purpose of the schema.
- **website**: Official LeetCode URL.
- **APIs**:
  - **host**: The base host for LeetCode API.
  - **intercept**: Defines the API for extracting user profile data.
  - **assert**: Specifies the validation criteria (e.g., contest rank < 5000, total problems solved > 300).
  - **nullifier**: Unique user identifier field.
- **HRCondition**: Human-readable conditions for verification.
- **tips**: Instructions for the user during the verification process.

## Usage

1. Navigate to the zkPass portal and select the LeetCode schema.
2. Log in to your LeetCode account and initiate the verification process.
3. Share the zkPass verification proof with third-party platforms.

## Evaluation Criteria

This project is designed to meet the zkPass hackathon evaluation criteria:

- **Adherence to Guidelines**: Fully complies with zkPass schema creation standards.
- **Innovation**: Leverages LeetCode data to unlock use cases like job recruitment and programming community recognition.
- **Technical Quality**: Clean, modular, and efficient schema implementation.
- **Documentation**: Comprehensive README and in-line comments for scalability and future integration.
- **Feasibility**: Fully functional with real-world data sources.
- **Impact**: Adds value to zkPass’s ecosystem by enabling privacy-preserving verification for developers.

## Future Enhancements

- Expand the schema to include additional LeetCode stats, such as **Badges** and **Streaks**.
- Integrate support for team-based achievements or regional rankings.
- Collaborate with hiring platforms to automate competency validation workflows.

## **Contact**

For inquiries or feedback, feel free to reach out:

**Team Name:** zkVerse
**Project Lead:** Karan Kumar Das  
**Email:** karankr.das.cse22@iitbhu.ac.in
