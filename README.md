# Strangler Core

Strangler Core is a functional "Bridge Architecture" blueprint (skeleton prototype) designed to evolve legacy Ruby on Rails monoliths into high-scale, AI-native ecosystems.

Inspired by the Strangler Fig pattern, this project demonstrates how to decouple the "Productivity Engine" (Rails) from the "Computational Brain" (Python/AI) using a unified GraphQL data access layer.

## Data Flow

1. React Frontend: Dispatches the GetPropertyAnalysis query.

2. Rails GraphQL Layer: Fetches the name and address from the PostgreSQL database using ActiveRecord. When it hits the smartSummary field, it pauses to call the Bridge Resolver.

3. The Resolver (The Bridge): The Ruby resolver bundles the property's historical data (e.g., "Lease expires in 3 months," "Tenant has 2 late payments") into a JSON payload and invokes the AWS Lambda.

4. Python Lambda: Uses Pydantic to validate the incoming property context. It simulates an AI analysis—calculating a leaseHealthScore and generating a tactical actionItem (e.g., "Initiate renewal sequence immediately").

5. Rails Gateway: Receives the Python JSON, validates that it matches the SmartSummaryType definition, and merges it with the property data to send a single, unified response back to the React client.
