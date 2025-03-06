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

### Step 03: Export form index.ts file inside the config folder.

### Step 04: Import shurjopay

```javascript
import shurjopay from "shurjopay";
```

### Step 04: Create an type declearation surjopay.d.ts file into interface folder

```javascript
declare module 'shurjopay' {
  class Shurjopay {


  }
  export default Shurjopay;
}
```

### Step 05: Add config function type into type deleartion file

```javascript
declare module 'shurjopay' {
  class Shurjopay {

constructor(): Shurjopay;

    config(
      root_url: string,
      merchant_username: string,
      merchant_password: string,
      merchant_key_prefix: string,
      return_url: string
    ): void;

  }
  export default Shurjopay;
}
```

### Step 06: Setting up shurjopay credentials from the environment variables

```javascript
shurjopay.config(
  config.sp.sp_endpoint,
  config.sp.sp_password,
  config.sp.sp_prefix,
  config.sp.sp_return_url,
  config.sp.sp_return_url
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
//You can also add "" empty string for the value
```

### Step 08:Add type for makepayment function

```javascript
declare module 'shurjopay' {
  class Shurjopay {

constructor(): Shurjopay;

    config(
      root_url: string,
      merchant_username: string,
      merchant_password: string,
      merchant_key_prefix: string,
      return_url: string
    ): void;
    makePayment(
      checkout_params: PaymentRequest,
      checkout_callback?: Callback<PaymentResponse>,
      error_handler?: ErrorHandler,
    ): void;
  }
  export default Shurjopay;
}
```

### Step 09: Create makePayment function into orders.uitls.ts and add the types into type delearation file

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

### Step 10: Add interface for payment response

```javascript
declare module 'shurjopay' {
  export interface PaymentResponse {
    checkout_url: string; // URL for payment execution
    amount: number; // Amount to be paid by the customer
    currency: string; // Currency in which the payment will be made
    sp_order_id: string; // shurjoPay payment ID
    customer_order_id: string; // Merchant-generated order ID
    customer_name: string; // Name of the customer making the payment
    customer_address: string; // Address of the customer making the payment
    customer_city: string; // City of the customer making the payment
    customer_phone: string; // Phone number of the customer making the payment
    customer_email: string; // Email of the customer making the payment
    client_ip: string; // IP address of the customer making the payment
    intent: string; // Purpose of the payment (e.g., Sale, Service, etc.)
    transactionStatus: string; // State of the payment (e.g., Pending, Completed)
  }
  class Shurjopay {
    constructor(): Shurjopay;
    config(
      root_url: string,
      merchant_username: string,
      merchant_password: string,
      merchant_key_prefix: string,
      return_url: string,
    ): void;
    makePayment(
      checkout_params: PaymentRequest,
      checkout_callback?: Callback<PaymentResponse>,
      error_handler?: ErrorHandler,
    ): void;
  }
  export default Shurjopay;
}

```

### Step 11: Call the make payment function from service page

```javascript
const payment = await orderUitls.makePaymentAsync(shurjopayPayload);
```
