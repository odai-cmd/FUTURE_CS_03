🔒 Secure File Portal

A Flask-based secure file storage portal that allows users to upload and download files with end-to-end encryption.
The system ensures that files are encrypted before storage and decrypted upon retrieval, making data safe from unauthorized access.

✨ Features
📂 Upload & Download files via API or command line
🔑 Envelope Encryption using AES-GCM (Data Encryption Key wrapped with a Key Encryption Key)
🗄 SQLite Database for storing encrypted file metadata and keys
🌐 HTTPS server (self-signed adhoc SSL)
⚡ Compatible with PowerShell curl.exe for testing

📁 Project Structure
secure-file-portal/
│── app.py            # Main Flask application
│── crypto.py         # Encryption & decryption logic (AES-GCM + KEK/DEK)
│── storage.py        # Handles saving and retrieving files from DB
│── database.py       # SQLAlchemy models and DB migration
│── config.py         # Configuration (DB URL, KEK key, etc.)
│── requirements.txt  # Python dependencies
│── README.md         # Project documentation.

⚙️ Installation
1️⃣ Clone the Repository
git clone https://github.com/<your-username>/secure-file-portal.git
cd secure-file-portal

2️⃣ Create Virtual Environment & Install Dependencies
python -m venv venv
venv\Scripts\activate   # On Windows
source venv/bin/activate  # On Linux/Mac

pip install -r requirements.txt

3️⃣ Setup Database
python -c "from database import migrate; migrate()"

4️⃣ Generate a KEK (Key Encryption Key)
python - <<EOF
import base64, os
print(base64.b64encode(os.urandom(32)).decode())
EOF

Copy this value into your config.py as:
KEK_BASE64 = "<your-generated-key>"

🚀 Running the Server: 
         python app.py

You’ll see:
 * Running on https://127.0.0.1:8080

📤 Upload a File
curl.exe -k -F "file=@test.txt" https://127.0.0.1:8080/upload

Response:
{"file_id":"729d14ad-05f2-4540-b364-45069762cc72"}

📥 Download a File
curl.exe -k -o downloaded.txt https://127.0.0.1:8080/download/<file_id>
<<The file will be decrypted automatically before saving.>>

📌 Example Workflow
1.Start server → python app.py
2.Upload test.txt → receive file_id
3.Download file using file_id → saved as downloaded.txt
4.Open and verify → ✅ decrypted file matches original

🔮 Future Improvements
🌐 Simple Web UI for upload & download
🔐 User authentication (JWT / OAuth)
☁️ Cloud storage backend (S3, Azure Blob, GCP Storage)
📊 File audit logs


👨‍💻 Author
Developed by Odai wahib as part of an internship project. 🚀
