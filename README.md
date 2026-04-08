🚀 DevOps Capstone Project – Flask CI/CD Pipeline

📌 Project Description

This project demonstrates an **end-to-end CI/CD pipeline** using a Flask web application.
It automates the process from **code commit to deployment** using Jenkins, Docker, and AWS EC2.

---
🏗️ Architecture Diagram

        Developer
            |
            v
         GitHub
            |
            v
        Jenkins
            |
            v
         Docker
            |
            v
        AWS EC2
            |
            v
          Users
---

🛠️ Tech Stack

* Backend: Python (Flask)
* Source Control: Git, GitHub
* CI/CD Tool: Jenkins
* Containerization: Docker
* Cloud Platform: AWS EC2 (Ubuntu)

---

⚙️ Setup Instructions (Local)

1️⃣ Clone Repository

git clone https://github.com/AkilaRajkumar/Capstone_project_Repo.git
cd Capstone_project_Repo


2️⃣ Install Dependencies

pip install -r requirements.txt


3️⃣ Run Application

python app.py


4️⃣ Access Application

http://localhost:5000

---

🔄 CI/CD Pipeline Flow

1. Developer pushes code to GitHub
2. Jenkins triggers automatically using webhook
3. Jenkins pulls latest code
4. Docker image is built
5. Image is pushed to Docker Hub
6. Application is deployed on AWS EC2
7. Users access the application via EC2 Public IP

---

⚠️ Challenges Faced

Docker container deployment issues
Jenkins pipeline configuration errors
Monitoring setup troubleshooting

---

📚 Learnings

Hands-on experience with CI/CD pipelines
Docker containerization and deployment
Cloud hosting using AWS EC2
Real-time monitoring using Prometheus and Grafana

---

✅ Conclusion

This project demonstrates how DevOps tools enable **automation, faster deployment, and scalability**.

---
