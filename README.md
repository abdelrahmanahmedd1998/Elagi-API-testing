# Elagi API Testing

This project showcases **API testing** performed on the [Elagi website](https://elagi.semicorner.com/home) using **Postman**. The goal is to validate API responses, automate test flows with dynamic authentication, and simulate real-world scenarios through chained requests.

---

## 🔧 Tools Used

- **Postman**  
- **JavaScript** (for scripting inside Postman)  
- **Postman Collection Runner**

---

## ✅ Project Features

- Created a dedicated Postman **collection** named `Elagi API Testing` containing all relevant API requests.

- Each request includes **test scripts** to verify:
  - ✅ Correct **status codes**
  - ✅ Valid **response structure** and key data
  - ✅ Acceptable **performance** (e.g., response time < 1000ms)
  - ✅ Business logic (e.g., login success, payment method validation)

- **Dynamic Environment Variables** were used to:
  - 🔐 Handle authentication (e.g., store access token dynamically)
  - 🔄 Reuse user data and chain requests (e.g., user ID, email)
  - 🧪 Link login to other requests (no hardcoded data)

- Automated login flow:
  - Extracts the **auth token** dynamically from login response using:
    ```js
    pm.environment.set("token", jsonData.token);
    ```
  - Injects this token into headers for authorized requests using:
    ```
    Bearer {{token}}
    ```

- Ran the full test suite with **Collection Runner** to simulate end-to-end testing and verify all flows.

---

## 📁 Exported Files

- ✅ `API Elagi.postman_collection.json` – Full collection with requests and test scripts.
- ❗ `Elagi_environment.postman_environment.json` – Optional environment file for context.

> ⚠️ Note: The environment file contains placeholder values. Real-time authentication still relies on dynamic token generation during runtime.

---

## 🚀 How to Use

1. Open **Postman**.
2. Import both:
   - `Elagi_API_Testing.postman_collection.json`
   - `Elagi_environment.postman_environment.json` (optional)
3. Run the Login request first to generate the token before making any authenticated (purchase or update) requests.
4. Use **Collection Runner** to run the full test suite.
5. Review test results, console logs, and dynamic behavior in the Postman UI.

---

## 📌 Notes

- 💡 **Dynamic authentication** is implemented using Postman test scripts.
- 💼 This is a **manual + dynamic API testing project** (automation is planned for the next phase).
- 🌍 No static tokens were used; the token is generated at runtime via login.
- 🧪 Future scope includes adding automated testing with CI tools like Jenkins or Newman.

---

## ⚠️ Observed Issues / API Bugs

While testing the ELAGI API, I noticed a few issues worth documenting:

1. **Broken Arabic Product Descriptions:**
   - When sending a `GET` request to fetch product details, some products return broken or unreadable Arabic text in the `description_ar` field.

2. **Out-of-Stock Products Can Be Added via API:**
   - The UI correctly prevents adding out-of-stock products to the cart.
   - However, when using Postman to send a `POST` request to add such a product, the request succeeds and adds the product.
   - This inconsistency could lead to broken logic or user frustration.

3. **Quantity Limit Bypass via API:**
   -The UI correctly prevents adding more than 3 from the same product to the cart.
   -However, when using Postman to send a `POST` request to add such a product, the request succeeds and adds the product by changing the quentatiy from the body .
   -This could lead to problem in the purchase process

These bugs highlight potential mismatches between frontend validation and backend enforcement.

## Author
  -Abdelrahman Ahmed Mohamed
  -Postman API Tester
  -GitHub: [https://github.com/abdelrahmanahmedd1998]

