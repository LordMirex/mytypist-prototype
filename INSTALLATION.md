# Installation Guide

## Prerequisites

The system requires AbiWord for PDF conversion. Installation varies by platform:

### Windows
1. Download AbiWord installer from [AbiWord's official website](http://www.abisource.com/download/)
2. Install AbiWord (default location should be `C:\Program Files (x86)\AbiWord\` or `C:\Program Files\AbiWord\`)
3. Add AbiWord's bin directory to your system PATH (optional but recommended)

### Linux (Ubuntu/Debian)
```bash
sudo apt-get update
sudo apt-get install abiword xvfb
```

### PythonAnywhere
1. Open a Bash console in PythonAnywhere
2. Install AbiWord and Xvfb:
```bash
pip3 install --user pythonanywhere
pa_install_abiword_on_pythonanywhere
```

## Python Dependencies
Install Python dependencies using:
```bash
pip install -r requirements.txt
```

## Verifying Installation

After installation, you can verify the setup by:

1. Running the Flask application
2. Going to the admin section
3. Uploading a test DOCX template
4. Generating a PDF document

If you encounter any issues:

### Windows
- Verify AbiWord is installed in one of these locations:
  - `C:\Program Files (x86)\AbiWord\bin\AbiWord.exe`
  - `C:\Program Files\AbiWord\bin\AbiWord.exe`
- Try running AbiWord from command prompt to ensure it's accessible

### Linux/PythonAnywhere
- Verify AbiWord installation: `which abiword`
- Verify Xvfb installation: `which xvfb-run`
- Check if the process has proper permissions to execute AbiWord

## Troubleshooting

### Windows
If PDF conversion fails:
1. Ensure AbiWord is properly installed
2. Try running AbiWord manually from command prompt
3. Check system PATH includes AbiWord's bin directory

### Linux/PythonAnywhere
If PDF conversion fails:
1. Check if both AbiWord and Xvfb are installed
2. Verify permissions are correct
3. Check system logs for any AbiWord or Xvfb errors

For PythonAnywhere specific issues:
1. Ensure you're using the correct Python version
2. Check if AbiWord is properly installed in your account
3. Verify Xvfb is available and running properly

## Support

If you encounter any issues:
1. Check the application logs for specific error messages
2. Verify all prerequisites are properly installed
3. Ensure proper permissions for file access
4. Try generating a test document to isolate the issue