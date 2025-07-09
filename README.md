# stripe-checkout-instructions
Stripe checkout instructions using Java SpringBoot

**step-by-step guide to integrate Stripe Checkout using Java Spring Boot** in **test mode**:

---

## ✅ Prerequisites

1. Stripe account: [https://dashboard.stripe.com](https://dashboard.stripe.com)
2. Java 17+ (recommended)
3. Spring Boot (Maven project)
4. Stripe Secret Key (starts with `sk_test_`)

---

## 📦 Step 1: Add Stripe Dependency

Add to your `pom.xml`:

```xml
<dependency>
  <groupId>com.stripe</groupId>
  <artifactId>stripe-java</artifactId>
  <version>24.9.0</version>
</dependency>
```

---

## 🔑 Step 2: Set Stripe API Key

In `application.properties`:

```properties
stripe.secret.key=sk_test_YOUR_SECRET_KEY
stripe.success.url=http://localhost:3000/success
stripe.cancel.url=http://localhost:3000/cancel
```

---

## 🧠 Step 3: Create Checkout Controller

```java
package com.example.demo.controller;

import com.stripe.Stripe;
import com.stripe.exception.StripeException;
import com.stripe.model.checkout.Session;
import com.stripe.param.checkout.SessionCreateParams;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.web.bind.annotation.*;

import java.util.HashMap;
import java.util.Map;

@RestController
@RequestMapping("/api/checkout")
public class CheckoutController {

    @Value("${stripe.secret.key}")
    private String stripeSecretKey;

    @Value("${stripe.success.url}")
    private String successUrl;

    @Value("${stripe.cancel.url}")
    private String cancelUrl;

    @PostMapping("/create-session")
    public Map<String, String> createCheckoutSession() throws StripeException {
        Stripe.apiKey = stripeSecretKey;

        SessionCreateParams params = SessionCreateParams.builder()
            .setMode(SessionCreateParams.Mode.PAYMENT)
            .setSuccessUrl(successUrl)
            .setCancelUrl(cancelUrl)
            .addLineItem(
                SessionCreateParams.LineItem.builder()
                    .setQuantity(1L)
                    .setPriceData(
                        SessionCreateParams.LineItem.PriceData.builder()
                            .setCurrency("usd")
                            .setUnitAmount(2000L) // $20.00
                            .setProductData(
                                SessionCreateParams.LineItem.PriceData.ProductData.builder()
                                    .setName("Test Product")
                                    .build()
                            )
                            .build()
                    )
                    .build()
            )
            .build();

        Session session = Session.create(params);

        Map<String, String> responseData = new HashMap<>();
        responseData.put("url", session.getUrl());

        return responseData;
    }
}
```

---

## 🌐 Step 4: Frontend – Call API and Redirect

In your React/Next.js frontend:

```ts
const handleCheckout = async () => {
  const res = await fetch('http://localhost:8080/api/checkout/create-session', {
    method: 'POST',
  });

  const data = await res.json();
  window.location.href = data.url;
};
```

---

## 🧪 Step 5: Test the Flow

1. Run your Spring Boot backend.
2. Open your frontend and click the checkout button.
3. Use test card:

   * **Card Number:** `4242 4242 4242 4242`
   * **Any future expiry & CVC**
4. You'll be redirected to the `success` page.

---

## ✅ Done!
