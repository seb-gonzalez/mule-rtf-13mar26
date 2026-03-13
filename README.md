
```markdown
# rtf-mule-deploy-2026-03-13

A lightweight Mule 4 Greeting API designed for Runtime Fabric (RTF) deployment. This application demonstrates property-driven greetings, DataWeave transformations, and detailed attribute logging for Ingress verification.

## 🚀 API Specification
* **Endpoint:** `GET /`
* **Port:** `8081`
* **Response Format:** `application/json`

### Logic Flow
1. **Listener:** Accepts `GET` requests on the root path `/`.
2. **Variable Injection:** Captures the `${message}` property into `vars.welcomeMessage`.
3. **Transformation:** Concatenates `"Welcome "` with your property value.
4. **Logging:** Dumps all `message.attributes` (including your **Host Headers**) to the logs for troubleshooting.

---

## 🛠 Required Configuration

### 1. External Properties
The app requires an `application.properties` file in `src/main/resources`. To change the message during deployment without a rebuild, set this in the **Anypoint Runtime Manager** properties tab:

| Property Key | Description | Example Value |
| :--- | :--- | :--- |
| `message` | The text appended to the greeting | `MuleSoft Training User` |

### 2. Deployment Settings (RTF)
Ensure your deployment uses these minimums to avoid memory pressure:
* **Reserved CPU:** 0.5 vCPU
* **Reserved Memory:** 1.0 GB (Covers Mule Runtime + Monitoring Sidecar)

---

## 🔍 Testing & Verification

Because this app uses an RTF Ingress, you must pass the specific **Host Header** to route traffic correctly.

### Execute Test
Run this command from your terminal:
```bash
curl -v -H "Host: unified-app.mulesoft-training.com" http://<YOUR_RTF_LB_ADDRESS>/

```

### Expected Output

```json
{
  "message": "Welcome MuleSoft Training User"
}

```

---

## 📂 Troubleshooting Logs

The application logs metadata under the category `com.mulesoft.training.greetings`. Check your logs to see exactly what headers the Load Balancer is passing:

```bash
# Example Log Entry
INFO com.mulesoft.training.greetings: {
  "headers": {
    "host": "unified-app.mulesoft-training.com",
    "user-agent": "curl/8.1.2"
  },
  "method": "GET",
  "requestPath": "/"
}

```

---

**Build Date:** March 13, 2026

**Environment:** Runtime Fabric

```

**Would you like me to generate the `application.properties` file content to match this?**

```
