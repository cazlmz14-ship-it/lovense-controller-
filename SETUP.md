# Lovense + Lovable setup

## 1. Create credentials

Create an application in the official [Lovense Developer Portal](https://developer.lovense.com/) and follow the current [Lovense API documentation](https://developer.lovense.com/docs) for the applicable authorization and device-connection flow.

Do not use a token or endpoint copied from an unverified template. Lovense integrations can require different flows depending on the product and use case.

## 2. Store secrets securely

Add these as encrypted backend/edge-function secrets in Lovable/Supabase—not as frontend variables:

```text
LOVENSE_CLIENT_ID
LOVENSE_CLIENT_SECRET
LOVENSE_API_TOKEN
LOVENSE_API_BASE_URL
```

Only define the values required by the official flow you selected. Never commit a real token or secret.

## 3. Use the backend proxy

The browser should call the edge function at `supabase/functions/lovense-proxy`. The function reads secrets server-side and calls Lovense. Keep client secrets and long-lived tokens out of browser code.

Before deploying, replace the marked request construction in the function with the exact authentication and endpoint format from the official Lovense documentation.

## 4. If a token was exposed

Immediately revoke or rotate it in the Lovense developer portal, remove it from code and logs, and update the backend secret with the replacement.

## References

- https://developer.lovense.com/
- https://developer.lovense.com/docs
