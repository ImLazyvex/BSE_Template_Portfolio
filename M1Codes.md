# Extracting Text From a PDF
```python
import pdfplumber

def extract_text_from_pdf(pdf_path):
    text = ""
    with pdfplumber.open(pdf_path) as pdf:
        for page in pdf.pages:
            text += page.extract_text() + "\n"
    return text

textbook_text = extract_text_from_pdf("TextbookUniversalHistory.pdf")
```

# Splitting PDF to Pieces as Big Textbooks are Hard To Handle
```python
import pymupdf as fitz
import os

def split_pdf(pdf_path, output_folder="output_pdfs", num_splits=20):
    # Open the PDF file
    doc = fitz.open(pdf_path)
    total_pages = len(doc)

    # Calculate pages per split
    pages_per_split = total_pages // num_splits
    remainder = total_pages % num_splits

    # Ensure output folder exists
    os.makedirs(output_folder, exist_ok=True)

    start_page = 0
    for i in range(num_splits):
        end_page = start_page + pages_per_split + (1 if i < remainder else 0)  # Distribute extra pages
        split_doc = fitz.open()  # Create new PDF
        
        # Add pages to the new split PDF
        for page_num in range(start_page, end_page):
            split_doc.insert_pdf(doc, from_page=page_num, to_page=page_num)

        # Save the split PDF
        split_pdf_path = os.path.join(output_folder, f"split_part_{i+1}.pdf")
        split_doc.save(split_pdf_path)
        split_doc.close()

        print(f"Saved: {split_pdf_path}")
        start_page = end_page  # Update start page for next split

    print("Splitting complete!")

# Example Usage
split_pdf("TextbookUniversalHistory.pdf")
```
