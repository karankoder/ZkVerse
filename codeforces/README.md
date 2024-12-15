# zkPass Hackathon Submission: Codeforces Schema Integration

---

## **Overview**

This project leverages the zkPass protocol to integrate Codeforces, a leading competitive programming platform, into the zkPass ecosystem. By creating a secure and privacy-preserving schema, our solution enables users to verify their Codeforces ratings, rank, and maximum rating without revealing additional sensitive data. This integration showcases zkPass's potential to enhance Web3 applications by enabling zero-knowledge-based verifications for developers, recruiters, and competitive communities.

---

## **Schema Highlights**

### **Features of the Schema:**

1. **Data Source:** Codeforces API
2. **Verified Metrics:**
   - **Rating**: Confirms user rating (e.g., ≥ 1900).
   - **Rank**: Verifies that the user’s rank is "Expert" or higher.
   - **Max Rating**: Ensures the user’s highest rating is ≥ 2000.
3. **Zero-Knowledge Proofs:**
   - Ensures verification conditions are met without exposing raw data.
4. **Human Readable Conditions:** Clear assertions like "Codeforces user with rating >= 1900" for intuitive proof validation.
5. **Integration Tips:** Provides user-friendly instructions for initiating the verification process.

---

## **Schema Configuration (Example)**

```json
{
  "issuer": "Codeforces",
  "desc": "Codeforces is a platform for competitive programming and contests, providing user ratings and rankings.",
  "website": "https://codeforces.com/api/user.info",
  "APIs": [
    {
      "host": "codeforces.com",
      "intercept": {
        "url": "/api/user.info",
        "method": "GET",
        "query": [
          {
            "key": "handles",
            "value": "{{user_handle}}",
            "verify": true
          }
        ]
      },
      "assert": [
        {
          "key": "result|0|rating",
          "value": "1900",
          "operation": ">="
        },
        {
          "key": "result|0|rank",
          "value": "expert",
          "operation": "in"
        },
        {
          "key": "result|0|maxRating",
          "value": "2000",
          "operation": ">="
        }
      ],
      "nullifier": "result|0|handle"
    }
  ],
  "HRCondition": [
    "Codeforces user with rating >= 1900",
    "Current rank in expert or higher",
    "Achieved a max rating of 2000 or more"
  ],
  "tips": {
    "message": "Log in to your Codeforces account and allow access to fetch your verified statistics."
  }
}
```

---

## **Use Cases**

1. **Decentralized Job Platforms:** Enable recruiters to validate competitive programming skills without compromising user privacy.
2. **Hackathon/Contest Applications:** Allow participants to verify eligibility through their Codeforces profile.
3. **Educational Platforms:** Integrate verifications into coding communities to foster transparency and competition.

---

## **Technical Details**

### **Schema Components**

- **Issuer:** Codeforces
- **API Endpoint:** `/api/user.info`
- **Nullifier:** `result|0|handle`
- **Assertions:** Rating, Rank, and Max Rating are verified with conditions like `>=` and `in`.
- **Integration with zkPass:** Built to comply with zkPass’s zkTLS and privacy-preserving standards.

### **Implementation Steps**

1. Define the schema JSON configuration.
2. Utilize Codeforces API to fetch user data.
3. Generate zero-knowledge proofs for the assertions.
4. Submit the proofs for validation through zkPass.

---

## **Evaluation Criteria**

### **Adherence to zkPass Guidelines**

Our schema complies fully with zkPass schema creation standards and integrates seamlessly with zkTLS.

### **Innovation**

The project enables competitive programmers to securely and privately showcase their accomplishments, unlocking new potential use cases for zkPass.

### **Technical Quality**

- Schema follows best practices for efficiency and scalability.
- Zero-knowledge verification ensures security without compromising user data.

### **Documentation**

Comprehensive documentation ensures ease of understanding and scalability for developers.

### **Feasibility**

The schema is practically deployable using real-world Codeforces API data.

### **Impact**

The integration broadens zkPass’s use cases, bringing competitive programming credentials into Web3 applications.

---

## **Future Roadmap**

1. Expand support to additional competitive programming platforms (e.g., AtCoder, LeetCode).
2. Incorporate advanced metrics such as participation frequency and problem-solving efficiency.
3. Develop a user-friendly dashboard for proof generation and validation.

---

## **Acknowledgements**

- **zkPass Team:** For providing the framework and guidelines.
- **Codeforces:** For making APIs accessible for integration.
- **Hackathon Organizers:** For the opportunity to participate.

---

## **Contact**

For inquiries or feedback, feel free to reach out:

**Team Name:** zkVerse
**Project Lead:** Karan Kumar Das  
**Email:** karankr.das.cse22@iitbhu.ac.in
