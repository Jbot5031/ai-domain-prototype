# Initialize git
git init
git branch -M main

# Add your GitHub repo (your username is already set)
git remote add origin https://github.com/JessieGonzalez/ai-domain-prototype.git

# Stage and commit all files
git add .
git commit -m "First commit - AI Domain Prototype"

# Push to GitHub
# ⚠️ Replace YOUR_TOKEN with your actual PAT before running
git push https://JessieGonzalez:YOUR_TOKEN@github.com/JessieGonzalez/ai-domain-prototype.git main