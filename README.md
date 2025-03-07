# surjopay-integration-documentation

[^1]: This is the first footnote.

**Step 01: Install shurjoPay payment system**

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

### Step 03: Export form index.ts file inside the config folder.

### Step 04: Import shurjopay

```javascript
import shurjopay from "shurjopay";
```

### Step 05: Create an type declearation surjopay.d.ts file into interface folder

### Step 06: Setting up shurjopay credentials from the environment variables into order.uitls.ts

```javascript
shurjopay.config(
  config.sp.sp_endpoint!,
  config.sp.sp_password!,
  config.sp.sp_prefix!,
  config.sp.sp_return_url!,
  config.sp.sp_return_url!
);
```

### Step 07: Initialize payment payload after the order into order.service.ts file

```javascript
const shurjopayPayload = {
  amount: totalPrice,
  order_id: order._id,
  currency: "BDT",
  customer_name: user.name, //add name
  customer_address: user.address, //add address
  customer_email: user.email, //add email
  customer_phone: user.phone, //add phone
  customer_city: user.city, //add city
  client_ip,
};
//You can also add "" or "N/A" empty string for the value
```

### Step 09: Create makePayment function into orders.uitls.ts

```javascript
const makePaymentAsync = async (
  paymentPayload: any
): Promise<PaymentResponse> => {
  return new Promise((resolve, reject) => {
    shurjopay.makePayment(
      paymentPayload,
      (response: PaymentResponse) => resolve(response),
      (error: any) => reject(error)
    );
  });
};
```

### Step 11: Call the make payment function from service page

```javascript
const payment = await orderUitls.makePaymentAsync(shurjopayPayload);
```

### Step 12:Add verify payment method into order.uitls.ts file

```javascript
const verifyPaymentAsync = (
  order_id: string
): Promise<VerificationResponse[]> => {
  return new Promise((resolve, reject) => {
    shurjopay.verifyPayment(
      order_id,
      (response) => resolve(response),
      (error) => reject(error)
    );
  });
};
```

### Step 13:Call verify payment method from order.service.ts

```javascript
const verifiedPayment = await orderUtils.verifyPaymentAsync(order_id);
```
