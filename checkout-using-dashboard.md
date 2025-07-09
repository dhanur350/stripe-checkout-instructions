
---

## ✅  Stripe Checkout in Test Mode from Dashboard
### This will help you understand how payments flow, how descriptions appear, and how everything is logged.

---

### 🔹 Step 1: Switch to Test Mode

1. Go to: [https://dashboard.stripe.com/test](https://dashboard.stripe.com/test)
2. Make sure **“Viewing test data”** is **enabled** (toggle in the left sidebar).

---

### 🔹 Step 2: Create a Product (with description)

1. Click **Products** in the left menu.
2. Click **“+ Add product”**
3. Fill the form:

   * **Name:** e.g., “Starter Pack”
   * **Description:** “Test product for learning Stripe Checkout”
   * **Price:** Choose **Standard pricing**, e.g., `$50.00`
4. Click **Save product**

Now you've created a test product with a name and description.

---

### 🔹 Step 3: Create a Test Checkout Link

1. Go to **Payments → Checkout**
2. Click **“Create a new Checkout link”**
3. Choose the product you just created
4. Set quantity or leave as default
5. Click **Create link**
6. Click **Copy link** and **open in a new browser tab**

You'll see the full **Stripe Checkout page** with:

* Product name
* Description
* Total amount

---

### 🔹 Step 4: Test a Payment Using Stripe Test Card

On the Checkout page:

1. Use this **test card**:

   * Card Number: `4242 4242 4242 4242`
   * Expiry: Any future date
   * CVC: Any 3-digit number
   * Name/ZIP: Anything
2. Click **Pay**
3. You’ll be redirected to the **success page**

---

### 🔹 Step 5: View the Payment in Dashboard

Go back to: [https://dashboard.stripe.com/test/payments](https://dashboard.stripe.com/test/payments)

* Click the latest payment
* You’ll see:

  * Product Name
  * **Description** (if added in Product or API)
  * Amount paid
  * Customer test data
  * Status (e.g., "Succeeded")

---

## 🧠 Bonus: Learn Descriptions from the API

If you want to simulate description from code (not just from product), click:

1. **Developers → API logs**
2. Click any recent **POST /v1/checkout/sessions**
3. You’ll see the **payload** with `description` (if it was sent via API)

This is how Stripe shows you exactly what was sent from backend → to Stripe → to Checkout page.

---

