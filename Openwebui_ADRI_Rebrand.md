
# OpenWebUI ADRI Rebrand Instructions

This guide walks you through locally rebranding OpenWebUI for ADRI, including logos, favicon, and interface text, using Cursor IDE. It ends with steps to redeploy the customized version to your MicroK8s server.

---

## 🖥️ Step 1: Clone and Prepare Locally

```bash
git clone https://github.com/open-webui/open-webui.git
cd open-webui
```

> Optional: create a new Git branch
```bash
git checkout -b adri-rebrand
```

---

## 🎨 Step 2: Replace Logos with ADRI Branding

### 2.1 Logo Replacement
Replace the following files:
- `public/logo.svg`
- `public/logo-dark.svg` (if dark mode is used)

Paste your own logos into these paths with the same file names.

### 2.2 ADRI Favicon
Replace `public/favicon.ico` with ADRI's favicon. You can generate one from a PNG using:
```bash
convert adri-icon.png -resize 32x32 public/favicon.ico
```

---

## ✏️ Step 3: Update Branding Text

Edit `src/constants.ts`:

```ts
export const APP_NAME = "ADRI AI";
export const APP_DESCRIPTION = "ADRI AI Assistant powered by LLM";
```

Update mentions of “Open WebUI” in:
- `src/pages/Settings.tsx`
- `src/components/Sidebar.tsx`
- `src/pages/About.tsx`

Use VSCode/Cursor search: `cmd+shift+F` → search for “Open WebUI”

---

## ⚙️ Step 4: Build the Custom Version

```bash
npm install
npm run build
```

---

## 📦 Step 5: Dockerize Locally (Optional)

If you want to test your build in Docker:

```bash
docker build -t adri-webui:latest .
docker run -d -p 3000:3000 adri-webui:latest
```

---

## 🚢 Step 6: Move to Server and Deploy

1. **Copy Files**
```bash
scp -r ./build adriadmin@your-server:/data/webui/adri
```

2. **Adjust your Kubernetes `deployment.yaml`** to point to the `adri-webui` image or static `/data/webui/adri` path depending on your hosting method.

---

## ✅ Validation
- Visit the service on its internal IP or via Ingress.
- Confirm logos, favicon, and name are all ADRI branded.

---

Made for ADRI. Rebrand once, deploy many 🚀
