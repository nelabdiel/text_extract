### **Extract Service**  

#### **Overview**  
The `extract_service` is a Flask-based API that extracts text, images, OCR content, and tables from **PDF** and **DOCX** files. It processes documents **entirely in-memory** and returns structured JSON data. It takes on average 0.07sec/page. 

---

### **Running the Service**  

#### **Run Locally (Python)**
```bash
python extract_service.py
```

#### **Run in Docker**
```bash
docker build -t extract_service .
docker run -p 5005:5005 extract_service
```

#### **Run with Docker Compose**
```bash
docker-compose up -d
```

---

### **API Usage**  
#### **Upload a File for Extraction**
- **Endpoint:** `POST /extract`  
- **Supported Formats:** `.pdf`, `.docx`  
- **Response:** JSON with extracted text, images (OCR), and tables  

#### **Example - Call from Python**
```python
import requests

files = {"file": open("example.pdf", "rb")}
response = requests.post("http://localhost:5005/extract", files=files)

print(response.json())  # View extracted content
```

#### **Example - Call from Terminal (cURL)**
```bash
curl -X POST -F "file=@example.pdf" http://localhost:5005/extract
```

---

### **Example Response**
```json
{
    "message": "Extraction complete",
    "file_type": "PDF",
    "extracted_text": "Full extracted text here...",
    "ocr_text": "OCR scanned text...",
    "extracted_images": 3,
    "extracted_tables": [
        {
            "table_index": 1,
            "data": [
                {"Column1": "Value1", "Column2": "Value2"},
                {"Column1": "Value3", "Column2": "Value4"}
            ]
        }
    ]
}
```

---

### **Features**
✔ Extracts **text** from PDF & DOCX  
✔ Detects & extracts **tables**  
✔ Extracts **images** & runs **OCR**  
✔ Works **entirely in-memory** (no file storage)  

---

### **Notes**
- **For PDFs**, extracts selectable text, images, and tables.  
- **For DOCX**, extracts text, tables, and images with OCR.  
- **OCR runs automatically on extracted images**.  
