
#  **How to Deploy a Static Website on GitHub Pages** 
#### *A step-by-step guide for beginners*

**Author:** Vanitha C N  
**Date:** 29/11/2025 

## **Overview**
GitHub Pages is a free hosting service that allows you to publish static websites directly from a GitHub repository.  
It is ideal for portfolios, documentation sites, and simple HTML/CSS/JS projects.

This guide walks you through deploying your site from scratch.

## **Prerequisites**
Before you begin, ensure you have:

- A **GitHub account**
- Basic understanding of:
  - Creating a repository  
  - Uploading files  
  - HTML/CSS (optional but helpful)

## **1. Prepare Your Project**
Create a folder on your computer containing:

- `index.html` (required)
- Any additional files (CSS, JS, images)

Example structure:

```
/my-website
|-- index.html
|-- style.css
|-- script.js
|__ images/
      |__  banner.png 

```

> **Note:** Your homepage must be named `index.html` for GitHub Pages to display it automatically.

## **2. Create a New Repository on GitHub**

1. Log in to GitHub.
2. Click **New Repository**.
3. Enter a name (e.g., `portfolio` or `my-site`).
4. Keep it **Public**.
5. Click **Create Repository**.

##  **3. Upload Your Website Files**

### **Option A - Drag & Drop**
1. In your repository, click **Add file -> Upload files**.
2. Drag your entire project folder contents.
3. Click **Commit changes**.

### **Option B - Using Git (optional for beginners)**
```bash
git init
git add .
git commit -m "Initial upload"
git branch -M main
git remote add origin https://github.com/<username>/<repo>.git
git push -u origin main
```

##  **4. Enable GitHub Pages**
1. Go to your repository  
2. Click **Settings**  
3. Scroll to **Pages**  
4. Under **Source**:
   - Select **Branch: main**
   - Select **Folder: /(root)**
5. Click **Save**

You should now see a message like:

**"Your site is live at https://<username>.github.io/<repository>"**

##  **5. Wait for Build (1-5 minutes)**
GitHub Pages needs a few minutes to build your site.

You may see a **404 page** temporarily-this is normal.

##  **6. Test Your Live Website**
Open the link shown under GitHub Pages settings.

Typical format:

```
https://<your-username>.github.io/<repository-name>/
```

If your `index.html` loads correctly, your site is live!

##  **7. Updating the Website**
Whenever you modify your site:

1. Upload or push updated files  
2. GitHub Pages automatically rebuilds  
3. Refresh your browser after 1-2 minutes  

##  **Common Errors & Fixes**

### **404 Not Found**
- Ensure file name is **index.html**  
- Confirm Pages settings: branch = **main**, folder = **root**  

### **Save button greyed out**
- You haven't committed files yet  
- You're viewing mobile GitHub (UI bug)  
- Repo has no `main` branch  

### **CSS or images not loading**
Use **relative paths**:
```html
<link rel="stylesheet" href="style.css">
<img src="images/banner.png">
```

##  **Conclusion**
You now have a live website hosted for free using GitHub Pages!  
This setup is perfect for technical portfolios, resumes, documentation, and tutorials.

##  **Optional Add-ons**
Enhancements:

- Custom domain (`CNAME`)
- GitHub Actions for auto-building
- Markdown-to-HTML converters
