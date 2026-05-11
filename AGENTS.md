---
agents:
  - name: Shopify GraphQL Generator
    location: .vscode/shopify-graphql-generator.agent.md
    triggerPhrases:
      - "create graphql query"
      - "create graphql mutation" 
      - "generate shopify query"
      - "generate shopify mutation"
      - "new gql file"
      - "shopify api query"
      - "shopify api mutation"
    description: Creates GraphQL queries and mutations for Shopify Admin API with proper file structure, variables, and documentation
---

# Workspace Agents

This file registers custom agents for this workspace.

## Available Agents

### Shopify GraphQL Generator
**Purpose**: Automate creation of GraphQL operations for Shopify

**When to use**:
- Need to create new GraphQL query or mutation
- Want to explore Shopify Admin API
- Need properly structured .gql and .json files
- Want scopes and documentation included

**Trigger phrases**:
- "create graphql query for [resource]"
- "generate mutation to [action]"
- "new shopify query for [purpose]"

**Examples**:
```
"Create a GraphQL query to get products with inventory levels"
"Generate a mutation to update customer email"
"New query to fetch orders from last week"
```

**What it does**:
1. Searches Shopify documentation
2. Creates .gql file in correct folder (query/ or mutation/)
3. Creates .json variables file if needed
4. Adds required scopes in comments
5. Follows GraphQL best practices
6. Updates tasks.json if needed

**Output structure**:
```
query/your-query.gql         # GraphQL operation
variables/your-query.json    # Example variables
```
