# Vercel Deployment Guide

Follow these steps to deploy the OAuth callback page to Vercel.

## Step 1: Create GitHub Repository

1. Go to [GitHub](https://github.com)
2. Click "New repository"
3. Name it: `luxesupply-oauth-callback`
4. Make it **Public**
5. Don't initialize with README
6. Click "Create repository"

## Step 2: Upload Files to GitHub

1. **Clone the repository**:
   ```bash
   git clone https://github.com/YOUR_USERNAME/luxesupply-oauth-callback.git
   cd luxesupply-oauth-callback
   ```

2. **Copy these files** from the `vercel-deployment` folder:
   - `oauth-callback.html`
   - `vercel.json`
   - `package.json`
   - `README.md`

3. **Commit and push**:
   ```bash
   git add .
   git commit -m "Initial commit"
   git push origin main
   ```

## Step 3: Deploy to Vercel

1. **Go to Vercel**: [vercel.com](https://vercel.com)
2. **Sign up/Login** with your GitHub account
3. **Click "New Project"**
4. **Import your repository**:
   - Select `luxesupply-oauth-callback`
   - Click "Import"
5. **Configure project**:
   - Project name: `luxesupply-oauth-callback` (or any name you prefer)
   - Framework Preset: Other
   - Root Directory: `./`
   - Build Command: `echo "No build needed"`
   - Output Directory: `./`
6. **Click "Deploy"**

## Step 4: Get Your Deployment URL

After deployment, Vercel will give you a URL like:
```
https://luxesupply-oauth-callback.vercel.app
```

Your callback URL will be:
```
https://luxesupply-oauth-callback.vercel.app/oauth-callback.html
```

## Step 5: Update Google Cloud Console

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Navigate to "APIs & Services" > "Credentials"
3. Edit your OAuth 2.0 Client ID
4. **Remove**: `https://auth.expo.io/@dangerst/photographyapp`
5. **Add**: `https://luxesupply-oauth-callback.vercel.app/oauth-callback.html`
6. Save

## Step 6: Update Your App

Update the redirect URI in `utils/googleSheetsService.js`:

```javascript
this.redirectUri = 'https://luxesupply-oauth-callback.vercel.app/oauth-callback.html';
```

## Step 7: Test

1. Clear your app cache: `expo start -c`
2. Test the OAuth flow in your app
3. You should be redirected to your Vercel callback page
4. The page should show "Authentication Successful!"

## Troubleshooting

### If deployment fails:
- Make sure all files are in the repository
- Check that `vercel.json` is properly formatted
- Try redeploying

### If OAuth still fails:
- Double-check the callback URL in Google Cloud Console
- Make sure the URL matches exactly (no extra spaces)
- Clear your app cache and try again

## Success!

Once deployed, your OAuth flow should work without Google verification issues! 🎉 