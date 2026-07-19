# Project Setup

This guide explains how to configure and run the Neo4j GraphRAG portfolio project.

## Prerequisites

You need:

* Python 3.10 or later
* A Neo4j database
* A supported LLM API key
* Git
* Access to a terminal or GitHub Codespace

## 1. Create a Neo4j Database

Create a Neo4j database using Neo4j Aura or a local Neo4j installation.

Make a note of the following connection details:

* Neo4j URI
* Neo4j username
* Neo4j password

The examples require a graph containing data that can be queried using Cypher.

Some examples may also require a Neo4j vector index and stored embeddings.

## 2. Create a Virtual Environment

From the repository root, run:

```bash
python -m venv .venv
source .venv/bin/activate
```

On Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

## 3. Install Dependencies

```bash
pip install --upgrade pip
pip install -r requirements.txt
```

## 4. Configure Environment Variables

Copy the example environment file:

```bash
cp .env.example .env
```

Update `.env` with your own credentials:

```env
NEO4J_URI=neo4j+s://your-instance.databases.neo4j.io
NEO4J_USERNAME=neo4j
NEO4J_PASSWORD=your-password
OPENAI_API_KEY=your-api-key
```

Do not surround values with placeholder brackets.

Do not commit the `.env` file.

## 5. Verify the Environment

Run:

```bash
python graphrag_app/test_environment.py
```

The validation script should confirm that:

* Environment variables are available
* The Neo4j driver can connect
* The required Python packages are installed
* The configured LLM provider can be accessed

## 6. Run the GraphRAG Examples

Vector retrieval:

```bash
python graphrag_app/vector_retriever.py
```

Vector GraphRAG:

```bash
python graphrag_app/vector_rag.py
```

Vector and Cypher GraphRAG:

```bash
python graphrag_app/vector_cypher_rag.py
```

Text-to-Cypher GraphRAG:

```bash
python graphrag_app/text2cypher_rag.py
```

## 7. Run Tests

```bash
pytest
```

## Troubleshooting

### Missing environment variables

Confirm that the `.env` file exists in the repository root:

```bash
ls -la
```

### Neo4j authentication failure

Check:

* `NEO4J_URI`
* `NEO4J_USERNAME`
* `NEO4J_PASSWORD`

Confirm that the database is running and accessible.

### Vector index not found

List the indexes in Neo4j:

```cypher
SHOW INDEXES;
```

Confirm that the index name used by the Python code matches the index in your database.

### Missing Python package

Reinstall the dependencies:

```bash
pip install -r requirements.txt
```

### LLM authentication failure

Confirm that the API key is valid and that the variable name matches the LLM provider used by the application.

## Security Notes

Before committing changes, run:

```bash
git status
git diff
git ls-files | grep -E '(^|/)\.env$'
```

The last command should not display your `.env` file.
