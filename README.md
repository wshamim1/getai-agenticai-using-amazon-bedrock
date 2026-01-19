# Multi-Agent AI System with Amazon Bedrock

A production-ready multi-agent AI system built with Amazon Bedrock, featuring intelligent agent collaboration, knowledge base integration, and a modern Streamlit interface.

> **Note**: This is a complete rewrite with modular architecture. Old implementation files are archived in `TO_BE_DELETED/` folder.

## 🌟 Features

- **Multi-Agent Collaboration**: Supervisor agent intelligently routes queries to specialized collaborator agents
- **Specialized Agents**:
  - 🌤️ **Weather Agent**: Real-time weather information
  - 📈 **Stock Agent**: Stock market data and analysis
  - 📰 **News Agent**: Latest news and updates
- **Knowledge Base Integration**: RAG-powered information retrieval with OpenSearch
- **Interactive UI**: Modern Streamlit interface for easy interaction
- **Production-Ready**: Comprehensive error handling, logging, and monitoring

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    Streamlit UI                          │
└────────────────────┬────────────────────────────────────┘
                     │
┌────────────────────▼────────────────────────────────────┐
│              Supervisor Agent                            │
│         (Intelligent Request Routing)                    │
└─────┬──────────────┬──────────────┬─────────────────────┘
      │              │              │
┌─────▼─────┐  ┌────▼─────┐  ┌────▼─────┐
│  Weather  │  │  Stock   │  │   News   │
│   Agent   │  │  Agent   │  │  Agent   │
└─────┬─────┘  └────┬─────┘  └────┬─────┘
      │              │              │
┌─────▼──────────────▼──────────────▼─────┐
│         AWS Lambda Functions             │
└──────────────────────────────────────────┘
```

## 📋 Prerequisites

- Python 3.11+
- AWS Account with Bedrock access
- AWS CLI configured with appropriate credentials
- Model access enabled for:
  - Llama 3.3 70B Instruct (`meta.llama3-3-70b-instruct-v1:0`)
  - Amazon Titan Embed Text v1 (for embeddings)

## 🚀 Quick Start

### 1. Install Dependencies

```bash
pip install -r requirements.txt
```

### 2. Configure AWS Credentials

```bash
aws configure
# Enter your AWS Access Key ID, Secret Access Key, and Region (us-east-1)
```

### 3. Deploy the System

```bash
python main.py
```

This will:
- Create IAM roles and policies
- Set up S3 buckets
- Deploy Lambda functions
- Create OpenSearch collection
- Set up Knowledge Base
- Deploy all agents (supervisor + collaborators)
- Associate collaborators with supervisor

### 4. Run the Streamlit App

```bash
streamlit run streamlit_app.py
```

Open your browser to `http://localhost:8501`

## 📁 Project Structure

```
.
├── core/                      # Core modules
│   ├── agent_manager.py      # Agent management
│   ├── iam_manager.py        # IAM roles and policies
│   ├── storage_manager.py    # S3 operations
│   ├── lambda_manager.py     # Lambda functions
│   ├── opensearch_manager.py # OpenSearch setup
│   └── knowledge_base_manager.py # Knowledge Base
├── config.py                  # Configuration
├── agents_config.py          # Agent definitions
├── orchestrator.py           # System orchestration
├── main.py                   # Entry point
├── streamlit_app.py          # UI application
├── cleanup.py                # Resource cleanup
├── diagnose.py               # Diagnostic tool
├── models_config.yaml        # Model configurations
├── README.md                 # This file
├── TROUBLESHOOTING.md        # Troubleshooting guide
├── MIGRATION_GUIDE.md        # Migration guide
├── data/                     # Data files for Knowledge Base
└── TO_BE_DELETED/            # Archived old implementation

```

## 🎯 Usage Examples

### Weather Query
```
User: "What's the weather in New York City?"
System: Routes to Weather Agent → Returns current weather data
```

### Stock Query
```
User: "What's the current price of AAPL?"
System: Routes to Stock Agent → Returns stock information
```

### News Query
```
User: "What's the latest tech news?"
System: Routes to News Agent → Returns recent news articles
```

### Knowledge Base Query
```
User: "Tell me about StreamSets pipelines"
System: Searches Knowledge Base → Returns relevant documentation
```

## 🔧 Configuration

### Change Foundation Model

Edit `config.py`:
```python
foundation_model: str = "meta.llama3-3-70b-instruct-v1:0"
```

### Add New Agent

1. Define agent in `agents_config.py`
2. Add Lambda function code
3. Define function schema
4. Run `python main.py` to deploy

### Customize Agents

Edit `agents_config.py` to modify:
- Agent instructions
- Function definitions
- Lambda code
- Action group descriptions

## 🛠️ Maintenance

### Run Diagnostics

```bash
python diagnose.py
```

### Clean Up Resources

```bash
python cleanup.py
```

**Warning**: This will delete all agents, Lambda functions, S3 buckets, and OpenSearch collections!

## 📊 Monitoring

The system includes comprehensive logging:

```python
import logging
logging.basicConfig(level=logging.INFO)
```

Logs include:
- Agent invocations
- Lambda executions
- Knowledge Base queries
- Error traces

## 🐛 Troubleshooting

See [TROUBLESHOOTING.md](TROUBLESHOOTING.md) for common issues and solutions.

### Common Issues

1. **Model Access Error**: Enable model access in AWS Bedrock Console
2. **IAM Permissions**: Run `python update_iam_policy.py`
3. **OpenSearch Timeout**: Collection creation takes 5-10 minutes
4. **Agent Not Found**: Ensure deployment completed successfully

## 📚 Documentation

- [TROUBLESHOOTING.md](TROUBLESHOOTING.md) - Comprehensive troubleshooting guide
- [MIGRATION_GUIDE.md](MIGRATION_GUIDE.md) - Migration from old implementation
- [AWS Bedrock Documentation](https://docs.aws.amazon.com/bedrock/)
- [Streamlit Documentation](https://docs.streamlit.io/)

## 🔐 Security

- IAM roles follow least privilege principle
- S3 buckets have encryption enabled
- OpenSearch uses AWS IAM authentication
- Lambda functions have minimal permissions

## 💰 Cost Optimization

- Use on-demand pricing for development
- Consider provisioned throughput for production
- Monitor usage with AWS Cost Explorer
- Clean up unused resources regularly

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## 📝 License

This project is licensed under the MIT License.

## 🙏 Acknowledgments

- Amazon Bedrock team for the AI platform
- Streamlit for the UI framework
- AWS for cloud infrastructure

## 📧 Support

For issues and questions:
1. Check [TROUBLESHOOTING.md](TROUBLESHOOTING.md)
2. Run `python diagnose.py`
3. Review logs in the console
4. Contact AWS Support for platform issues

## 🚀 What's Next?

- [ ] Add more specialized agents
- [ ] Implement conversation memory
- [ ] Add user authentication
- [ ] Deploy to production
- [ ] Add monitoring dashboards
- [ ] Implement A/B testing

---

**Built with ❤️ using Amazon Bedrock and Python**