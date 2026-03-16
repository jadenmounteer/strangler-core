# 📋 Functional Requirements (The "What")

Unified GraphQL Entry Point: The system must expose a single GraphQL endpoint (Rails) that can resolve a nested Property query.

Hybrid Data Resolution: The Property object must resolve basic fields (Name, Address) from a local Rails source (ActiveRecord/Mock) and the smartSummary field from an external AWS Lambda.

Cross-Language Handshake: The Rails resolver must successfully serialize a JSON payload, invoke a Python AWS Lambda, and deserialize the response.

Deterministic Validation: The Python Lambda must use Pydantic to validate the incoming Rails payload against a strict schema before execution.

Simulated AI Analysis: The Lambda must return a structured "Smart Summary" containing a leaseHealthScore, aiGeneratedInsight, and an array of actionItems.

Error Transparency: The system must return a partial GraphQL response (Null for the AI field but Success for the Property field) if the Lambda fails or times out.

# 🏗️ Non-Functional Requirements (The "How")

Isolation (The Strangler Rule): The Python Lambda must have no direct access to the Rails Database. It must rely entirely on the context passed via the Bridge.

Type Safety: The GraphQL schema (Ruby) and the Pydantic models (Python) must be synchronized to act as a "Contract" between the two services.

Observability: The Rails bridge must log the "Round Trip" time of the Lambda invocation to demonstrate performance awareness.

Resiliency (Circuit Breaking): The Rails resolver must implement a basic timeout (e.g., 2 seconds) to prevent an AI "hallucination" or delay from blocking the main web thread.

Code Scalability: The Python code must be structured using a "Specialist" pattern (separation of validation logic from execution logic) to allow for future LLM integration.
