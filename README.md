# MyTypist - Professional Document Generator

A Flask-based web application for generating professional documents from DOCX templates with advanced placeholder management and batch processing capabilities.

## Features

### Enhanced Admin Template Management
- **ACTUAL Document Formatting**: Extracts real fonts, sizes, margins from uploaded DOCX
- **100+ Font Families**: Comprehensive font selection including Google Fonts, Microsoft Office fonts, professional fonts
- **Individual Placeholder Styling**: Each {{name}} instance can be styled separately (3 {{name}} = 3 styling opportunities)
- **Streamlined UI**: Compact button layout for bold/italic/underline styling
- **Smart Placeholder Defaults**: Auto-detection with intelligent suggestions:
  - Names → "Joe Doe"
  - Addresses → "24 Avenue Avenue, Osato Junction, Benin City"
  - Departments → "Production Engineering"
  - Registration Numbers → "ENG2204223"
- **Auto-Type Detection**: Gender gets male/female options, his_her gets his/her options
- **Document-Level Fonts**: Font family/size applied to entire document, not per placeholder
- **All Placeholders Required**: No required checkbox needed, all placeholders mandatory by default

### Core Document Processing
- **Professional Template Processing**: Upload DOCX templates with `{{ placeholder }}` syntax
- **Advanced Placeholder Extraction**: Automatically detects and preserves document formatting
- **Professional Quality Output**: Maintains original template formatting for professional documents
- **Multiple Input Types**: Support for text, date, email, number, and dropdown options
- **Format Conversion**: Generate documents in both DOCX and PDF formats

### Batch Processing
- **Multi-Template Generation**: Generate multiple documents simultaneously
- **Threaded Processing**: Efficient batch processing with ThreadPoolExecutor
- **Progress Tracking**: Monitor batch generation status and results
- **Error Handling**: Comprehensive error reporting for failed documents

### Advanced Features
- **Smart Filename Generation**: Format: `name_documentname_timestamp.docx`
- **Template Management**: Full CRUD operations for document templates
- **User Input Validation**: Required fields and pattern validation
- **Professional PDF Conversion**: Enhanced formatting preservation in PDF output
- **Admin Panel**: Complete template and document management interface

## Installation

### Prerequisites
- Python 3.7+
- Flask and dependencies (see requirements.txt)

### Setup
1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd MyTypist
   ```

2. **Create and activate virtual environment**
   ```bash
   # Create virtual environment
   python -m venv venv
   
   # Activate virtual environment
   # On Windows:
   venv\Scripts\activate
   # On macOS/Linux:
   source venv/bin/activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

   **Perfect PDF Generation:**
   - PDFs are generated using pure Python (ReportLab) with exact DOCX formatting
   - No external applications required - works anywhere Python runs
   - Self-contained solution that can be hosted on any platform

4. **Database Setup**
   ```bash
   # The application automatically creates the SQLite database on first run
   # Database will be created at: ./db/app.db
   # No manual database setup required!
   ```

   **IMPORTANT Database Information:**
   - **Database Location**: `./db/app.db` (SQLite file)
   - **Auto-Creation**: Database and tables are created automatically on first startup
   - **Data Persistence**: Your data persists between app restarts
   - **Backup Critical**: Always backup `./db/app.db` before major changes
   - **Admin Tools**: Use admin panel for database management (backup/clear functions)

   **Database Management:**
   - **Backup**: Admin panel → "Create Backup" (saves to `./db/app_backup_YYYYMMDD_HHMMSS.db`)
   - **Clear All Data**: Admin panel → "Clear Database" (⚠️ WARNING: Deletes everything!)
   - **Manual Backup**: `cp db/app.db db/backup_$(date +%Y%m%d).db`
   - **Restore**: `cp db/backup_YYYYMMDD.db db/app.db` (stop app first)

5. **Initialize and run the application**
   ```bash
   python app.py
   ```
   
   **Important Notes:**
   - The application will automatically create required folders: `upload/`, `generated/`, `temp/`, `db/`
   - Database tables are created automatically on first startup
   - Your data is stored in `./db/app.db` - **BACKUP THIS FILE** to preserve your templates and documents
   - **Performance**: Homepage uses smart caching for faster loading
   - **Database Safety**: Use admin backup function before clearing data
   - **File Management**: All uploaded templates stored in `./upload/`, generated docs in `./generated/`
   - **Admin Features**: 100+ fonts, individual placeholder styling, smart defaults
   - **Document Quality**: Exact DOCX formatting preserved, perfect PDF copies

6. **Access the application**
   - Main Application: http://localhost:8000
   - Admin Panel: http://localhost:8000/admin?key=SecretAdmin123

### Data Backup and Recovery
```bash
# Backup your data (IMPORTANT!)
cp db/app.db db/app_backup_$(date +%Y%m%d).db

# Restore from backup
cp db/app_backup_YYYYMMDD.db db/app.db
```

## Testing the Application

### Quick Test Guide
1. **Start the application**
   ```bash
   python app.py
   ```

2. **Test admin panel access**
   - Go to: http://localhost:8000/admin?key=SecretAdmin123
   - Verify admin dashboard loads with statistics

3. **Upload a test template**
   - In admin panel, click "Upload Template"
   - Upload a DOCX file with `{{ name }}` and `{{ date }}` placeholders
   - Verify template appears in template list

4. **Test document generation**
   - Go to main page: http://localhost:8000
   - Select your uploaded template
   - Fill in the form fields
   - Generate both DOCX and PDF formats
   - Verify downloads work correctly

5. **Test batch processing**
   - Go to: http://localhost:8000/batch
   - Select multiple templates
   - Fill merged form
   - Generate batch documents
   - Verify all documents are created

### Running Automated Tests
```bash
# Run the comprehensive test suite
python test_fixes.py
```

This runs 25+ tests covering:
- Database model functionality
- Document processing engine
- Template upload and management
- Single and batch document generation
- PDF conversion
- Admin panel operations

### Common Test Scenarios
- **Template with multiple placeholders**: Test complex forms
- **Required vs optional fields**: Verify validation works
- **Different placeholder types**: Test date, text, and option fields
- **Large batch processing**: Test with 5+ templates
- **PDF conversion**: Ensure both docx2pdf and reportlab work

## Usage

### Creating Templates
1. Access the admin panel with the admin key
2. Upload DOCX templates containing `{{ placeholder }}` syntax
3. Configure placeholder properties (type, validation, help text)
4. Set template metadata (name, type, description)

### Generating Documents
1. Select a template from the main page
2. Fill in the required information
3. Choose output format (DOCX or PDF)
4. Download your professional document

### Batch Processing
1. Go to "Batch Generator" from the main menu
2. Select multiple templates
3. Fill in the merged form with all required fields
4. Generate all documents at once
5. Download individual files or view batch results

## Project Structure

```
MyTypist/
├── app.py                          # Main Flask application
├── requirements.txt                # Python dependencies
├── templates/                      # Jinja2 templates
│   ├── base.html                  # Base template
│   ├── index.html                 # Main page
│   ├── create.html                # Single document generation
│   ├── batch.html                 # Batch document generation
│   ├── batch_results.html         # Batch results display
│   ├── results.html               # Document results
│   ├── error.html                 # Error pages
│   ├── admin.html                 # Admin dashboard
│   ├── partials/
│   │   └── form_fields.html       # Reusable form components
│   └── admin/
│       ├── templates.html         # Template management
│       ├── upload.html            # Template upload
│       └── edit_template.html     # Template editing
├── upload/                        # Uploaded template storage
├── generated/                     # Generated document output
├── temp/                          # Temporary file processing
└── db/                           # SQLite database
```

## Database Schema

### Template
- Document template information and formatting settings
- Manages active/inactive states and metadata

### Placeholder
- Individual placeholder definitions within templates
- Supports validation, types, and formatting options

### CreatedDocument
- Generated document records with user inputs
- Tracks file paths and creation metadata

### BatchGeneration
- Batch processing records and status tracking
- Links multiple documents in batch operations

## API Endpoints

### User Routes
- `GET /` - Main page with template listing
- `GET /create/<template_id>` - Document creation form
- `POST /generate` - Process document generation
- `GET /results/<document_id>` - View generation results
- `GET /download/<document_id>/<format>` - Download documents
- `GET/POST /batch` - Batch document generation
- `POST /get_merged_placeholders` - AJAX placeholder loading

### Admin Routes
- `GET /admin` - Admin dashboard
- `GET /admin/templates` - Template management
- `GET/POST /admin/upload` - Template upload
- `GET/POST /admin/template/<id>/edit` - Template editing
- `GET /admin/template/<id>/pause` - Pause template
- `GET /admin/template/<id>/resume` - Resume template
- `GET /admin/template/<id>/delete` - Delete template

## Technical Features

### Professional Document Processing
- **DocxTemplate Integration**: Uses python-docxtpl for template rendering
- **Formatting Preservation**: Plain text context prevents formatting destruction
- **XML Document Analysis**: Advanced placeholder extraction with structure preservation
- **Perfect PDF Conversion**: Pure Python solution with exact DOCX formatting preservation
  - Preserves all fonts, sizes, alignment, spacing, and layout
  - No external dependencies - works on any hosting platform
  - PDF output matches DOCX exactly like a screenshot

### Performance Optimizations
- **Caching**: Template and route caching for improved performance
- **Threaded Batch Processing**: Concurrent document generation
- **Efficient Database Queries**: Optimized SQLAlchemy operations
- **File Management**: Organized storage with cleanup capabilities

### Security Features
- **Admin Key Protection**: Secure admin panel access
- **File Upload Validation**: DOCX file type validation
- **Path Security**: Secure filename handling
- **Input Sanitization**: Form input validation and sanitization

## Configuration

### Environment Variables
- `SECRET_KEY`: Flask secret key (default: dev-secret-key-change-in-production)
- `ADMIN_KEY`: Admin panel access key (default: SecretAdmin123)
- `MAX_CONTENT_LENGTH`: Maximum file upload size (default: 16MB)

### Directory Configuration
- Upload folder: `./upload`
- Generated documents: `./generated`
- Temporary files: `./temp`
- Database: `./db/app.db`

## Troubleshooting

### Common Issues
1. **Template Not Found**: Ensure DOCX templates are properly uploaded
2. **Placeholder Errors**: Verify `{{ placeholder }}` syntax in templates
3. **PDF Conversion Issues**: Install docx2pdf for better PDF quality
4. **File Permission Errors**: Check directory permissions for uploads/generated folders

### Logging
The application includes comprehensive logging for debugging:
- Template processing events
- Document generation status
- Error tracking and reporting
- Batch processing progress

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

This project is a prototype for document generation and template management.

## Recent Major Improvements

### ✅ Admin Template Editing Completely Fixed
- **ACTUAL formatting extraction** instead of random defaults
- **100+ professional fonts** (Google Fonts, Microsoft Office, Adobe, etc.)
- **Individual placeholder instances** - Each {{name}} can be styled separately
- **Streamlined compact UI** with professional button layouts
- **Document-level font management** - No per-placeholder font confusion
- **Smart auto-suggestions** for ALL variable formats (name, sender_address, name_2, etc.)

### ✅ Batch Processing Completely Fixed
- **No more threading errors** - Stable sequential processing
- **0 documents bug fixed** - All documents generate successfully
- **Fast performance** - No more long loading times
- **Progress indicators** - Users see processing status
- **Proper downloads** - Individual and batch download options

### ✅ PDF Generation Completely Fixed
- **Pure Python solution** - No external dependencies needed
- **Exact DOCX formatting** - PDFs match DOCX like screenshots
- **Professional quality** - All fonts, spacing, alignment preserved
- **Self-contained** - Works on any hosting platform

### ✅ Performance & Database Improvements
- **Homepage caching** - 30-second cache for fast loading
- **Database management** - Backup and clear functions in admin
- **Proper documentation** - Complete environment setup guide
- **Smart address formatting** - Automatic line breaks and punctuation
- **West Africa date formatting** - Correct timezone and formats

---

**MyTypist** - Professional document generation made simple.