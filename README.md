# surjopay-integration-documentation

### Step 01: Install shurjoPay payment system

```javascript
npm install shurjopay
```

### Step 02: Create a .env file inside your project's root directory. Here is a sample .env configuration.

```javascript
SP_ENDPOINT=https://sandbox.shurjopayment.com
SP_USERNAME=sp_sandbox
SP_PASSWORD=pyyk97hu&6u6
SP_PREFIX=SP
SP_RETURN_URL=https://sandbox.shurjopayment.com/response
```

### Step 03: Import shurjopay

```javascript
import shurjopay from "shurjopay";
```

### Step 03: Setting up shurjopay credentials from the environment variables
