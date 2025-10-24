# Aspose.Words Setup Guide

For Linux environments (including PythonAnywhere):

1. Install ICU package:
```bash
sudo apt-get update
sudo apt-get install -y libicu-dev
```

2. Set environment variable in your app:
```python
import os
os.environ["System.Globalization.Invariant"] = "true"
```

3. For PythonAnywhere, add to your WSGI file:
```python
# In your wsgi.py
import os
os.environ["System.Globalization.Invariant"] = "true"
```

4. Install Python dependencies:
```bash
pip install -r requirements.txt
```

## Troubleshooting

If you see errors about ICU or globalization:

1. Ensure libicu-dev is installed
2. Verify the environment variable is set
3. Restart your web app

For Windows environments:
- No additional setup required
- Aspose.Words works out of the box