# Week 9 Workshop; Implementing Secure Database Access in Scripts

## Learning Objectives

- Understand the importance of securing credentials and secrets in ML/AI workflows
- Learn how to store and manage secrets using Azure Key Vault
- Create scripts that securely access a managed database in the cloud
- Test, troubleshoot, and verify secure connectivity from cloud compute to database

---

## Agenda

1. Why Secure Credential Management Matters in ML/AI Projects
2. Introducing Azure Key Vault for Secret Management
3. Step-by-Step; Store and Retrieve Secrets with Key Vault
4. Connecting to a Managed Database; Secure Approaches
5. Hands-on Practical; Secure Script Demo and Exercise
6. Testing, Troubleshooting, and Best Practices
7. Reflection and Assessment Questions
8. Summary and Next Steps

---

## 1. Why Secure Credential Management Matters in ML/AI Projects

- In production, storing plain-text credentials is unsafe; can lead to data breaches
- Many industries require compliance (privacy, auditing, responsible AI)
- Proper secret management supports automation and reproducibility in cloud environments

---

## 2. Introducing Azure Key Vault for Secret Management

- Azure Key Vault stores secrets; manages keys and credentials centrally
- Access controlled by Azure Active Directory and roles
- Common secrets; database passwords, API tokens, ML model keys

---

## 3. Storing and Retrieving Secrets with Azure Key Vault

### Example; Storing a Secret

```python
# This is conceptual; actual creation happens via Azure portal or CLI
# Example: Storing a database password in Key Vault (Azure CLI)
# az keyvault secret set --vault-name "my-keyvault" --name "db-password" --value "SuperSecretPassword!"
```

- Use Azure CLI, portal, or automation
- Assign appropriate permissions to limit who/what can access secrets

### Example; Retrieving a Secret in Python

```python
from azure.identity import DefaultAzureCredential
from azure.keyvault.secrets import SecretClient

key_vault_url = "https://<your-key-vault-name>.vault.azure.net"
secret_name = "db-password"

# Authenticate using managed identity or service principal
credential = DefaultAzureCredential()
client = SecretClient(vault_url=key_vault_url, credential=credential)

retrieved_secret = client.get_secret(secret_name)
db_password = retrieved_secret.value

print("Database password accessed securely from Key Vault.")
```

---

## 4. Connecting to a Managed Database; Secure Approaches

- Managed databases (Azure SQL, PostgreSQL, MySQL) are preferred for reliability and auditing
- Fetch secrets at runtime; avoid hardcoded credentials
- Use environment variables and connection strings for portability

### Example Setup

```python
import os
import psycopg2  # For PostgreSQL

db_user = os.getenv("DB_USER")
db_pass = db_password  # Fetched securely
db_host = os.getenv("DB_HOST")
db_name = os.getenv("DB_NAME")

# Build the connection string securely
conn_str = f"dbname={db_name} user={db_user} password={db_pass} host={db_host}"

conn = psycopg2.connect(conn_str)
print("Database connection established securely.")
```

---

## 5. Hands-on Practical; Secure Script Demo and Exercise

**Task Guidelines**
- Each student will; 
  - Retrieve a test secret from Azure Key Vault using Python
  - Inject secret as an environment variable into a script
  - Connect securely to a sample managed database (provided by instructor or using Azure free tier)

**Exercise Steps (Use dummy/test details if needed)**
1. Follow template Python notebook; update vault and secret names
2. Authenticate using DefaultAzureCredential (works from Azure VMs or with service principal locally)
3. Print secret (simulated password) using script
4. Establish DB connection (simulate using sqlite3 if real database is not possible)
5. Log and verify connection result; never print passwords to logs

---

## 6. Testing, Troubleshooting, and Best Practices

- **Test** your script using invalid credentials; verify access control works as expected
- **Troubleshoot**; Check Key Vault access policies, role assignments, and environment config
- **Best Practices**
  - Never store credentials in code or git
  - Use environment variables and Key Vault for secret management
  - Rotate secrets regularly; monitor access logs
  - Handle connection errors gracefully in scripts

---

## 7. Reflection and Assessment Questions

- Why is it important to avoid hardcoded database credentials in scripts?
- What steps would you take to rotate secrets in a production ML environment?
- How does Azure Key Vault integrate with MLOps pipelines?

---

## 8. Summary and Next Steps

- Today you practiced storing/retrieving secrets with Azure Key Vault and making secure DB connections
- These skills are essential for responsible, production-worthy ML/AI applications
- Next week; Apply PyTorch foundational skills in your first major project, building upon your ability to manage secrets and connections in real workflows

---

### Appendix: Simulated Local Exercise (For students without cloud access)

If Azure or managed DBs are unavailable, simulate with `os.environ` and `sqlite3`:

```python
import os
import sqlite3

os.environ["DB_PASSWORD"] = "DummyPassword123"
db_pass = os.getenv("DB_PASSWORD")
conn = sqlite3.connect(":memory:")  # Ephemeral in-memory DB

print("Simulated database connection established with secure password handling.")
```

---