# Solid Green — Net Zero (Modelled) Review Portal

A lightweight Streamlit web app that automates Solid Green's Net Zero Carbon (Modelled) report reviews.

## What it does
- Upload a Net Zero (Modelled) report (PDF)
- Automatically scores a strict checklist (1/0) via keyword heuristics
- Generates:
  - An **Excel** checklist with auto-scoring
  - A **PDF** infographic certificate with final score and required updates

> Note: This uses heuristic text checks. It's designed for rapid internal QA. You can extend the keyword sets or wire in the OpenAI API for deeper semantic checks.

## Quickstart (local)
```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
streamlit run app.py
```
Open the URL shown in your terminal (usually http://localhost:8501).

---

## 🚀 Deploying to Render

### Prerequisites
- A [Render account](https://render.com) (free tier available)
- Your code pushed to a Git repository (GitHub, GitLab, or Bitbucket)

### Step-by-Step Deployment Guide

#### 1. Prepare Your Repository
Ensure your repository contains:
- ✅ `app.py` - Your Streamlit application
- ✅ `requirements.txt` - Python dependencies
- ✅ `render.yaml` - Render configuration file (already created)
- ✅ `.streamlit/config.toml` - Streamlit configuration (already created)

#### 2. Push to Git (if not already done)
```bash
# Initialize git repository (if needed)
git init

# Add all files
git add .

# Commit changes
git commit -m "Initial commit - Ready for Render deployment"

# Add remote repository (replace with your repo URL)
git remote add origin https://github.com/yourusername/your-repo-name.git

# Push to main branch
git push -u origin main
```

#### 3. Deploy on Render

##### Option A: Using Blueprint (Recommended - Automatic)
1. Log in to [Render Dashboard](https://dashboard.render.com)
2. Click **"New +"** → **"Blueprint"**
3. Connect your Git repository
4. Render will automatically detect the `render.yaml` file
5. Click **"Apply"** to deploy
6. Wait 5-10 minutes for the build to complete

##### Option B: Manual Web Service Setup
1. Log in to [Render Dashboard](https://dashboard.render.com)
2. Click **"New +"** → **"Web Service"**
3. Connect your Git repository
4. Configure the service:
   - **Name**: `solidgreen-netzero-portal` (or your choice)
   - **Environment**: `Python 3`
   - **Region**: Choose closest to your users
   - **Branch**: `main`
   - **Build Command**: `pip install -r requirements.txt`
   - **Start Command**: `streamlit run app.py --server.port $PORT --server.address 0.0.0.0`
5. Click **"Create Web Service"**

#### 4. Monitor Deployment
- Watch the build logs in real-time on Render dashboard
- Once deployed, Render will provide a public URL like: `https://solidgreen-netzero-portal.onrender.com`
- Free tier services may spin down after inactivity (cold starts)

#### 5. Post-Deployment Configuration

##### Environment Variables (if needed)
If you need to add environment variables:
1. Go to your service dashboard on Render
2. Click **"Environment"** tab
3. Add variables like:
   - `PYTHON_VERSION`: `3.11.0`
   - Any API keys or secrets

##### Custom Domain (Optional)
1. Go to **"Settings"** → **"Custom Domain"**
2. Add your domain and configure DNS records

### 🔧 Troubleshooting

#### Build Fails
- Check `requirements.txt` for version conflicts
- Verify Python version compatibility
- Review build logs for specific errors

#### App Won't Start
- Ensure start command includes `--server.port $PORT --server.address 0.0.0.0`
- Check that all dependencies are in `requirements.txt`
- Verify Streamlit configuration in `.streamlit/config.toml`

#### Slow Performance
- Free tier has limited resources
- Upgrade to paid plan for better performance
- Consider optimizing PDF processing for large files

### 💰 Pricing
- **Free Tier**: 750 hours/month, spins down after 15 min inactivity
- **Starter**: $7/month, always-on, more resources
- Full pricing: https://render.com/pricing

### 🔄 Continuous Deployment
Render automatically redeploys when you push to your connected branch:
```bash
git add .
git commit -m "Update feature"
git push origin main
```

---

## Alternative Deploy Options
- **Streamlit Community Cloud** (free/fast)
- **Docker** to any cloud (AWS, Azure, GCP)
- Your internal server

## Customisation
- Edit `CHECKS` in `app.py` to refine rules/keywords.
- Replace branding or colors inside the certificate generator in `build_certificate()`.

## Security
- Files are processed in-memory and not stored by default.
- Authentication included via streamlit-authenticator
- **Default credentials**:
  - Username: `solidgreen` / Password: `Green@123`
  - Username: `admin` / Password: `admin123`
  - Username: `reviewer` / Password: `reviewer123`
- **⚠️ Important**: Change default passwords before deployment!

## Support
For issues or questions, contact your development team or create an issue in the repository.
