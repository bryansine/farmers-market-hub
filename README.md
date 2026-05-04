# Farmers Market Hub

**Farmers Market Hub** is a robust e-commerce and logistics management platform designed to bridge the gap between smallholder Kenyan farmers and bulk buyers. Built with **Django** and integrated with the **Safaricom Daraja API**, it provides a seamless end-to-end workflow from harvest listing to secure payment.

---

##  Key Features

*   **Farmer Dashboard:** Real-time inventory management for crops (Maize, Wheat, Legumes).
*   **M-Pesa Integration:** Fully functional **STK Push** implementation for secure, mobile-first transactions.
*   **Automated Order Workflow:** Synchronized status updates between `Cart`, `Orders`, and `Payment` confirmation.
*   **Localized UI:** Mobile-responsive design optimized for farmers using devices like the Samsung S-series and A-series in field conditions.
*   **Role-Based Access:** Distinct permissions for Farmers (Sellers), Customers (Buyers), and Site Administrators.

---

##  Tech Stack

*   **Backend:** Python 3.12, Django 5.1
*   **Database:** PostgreSQL (Production), SQLite
*   **Payments:** Safaricom Daraja API (M-Pesa)
*   **Frontend:** Bootstrap 5, Django Crispy Forms
*   **Deployment:** Docker, Render, Gunicorn

---

## Payment Logic

The platform implements a "Production-Ready" payment callback architecture:
1.  **Initiation:** Customer triggers STK Push via `daraja/utils.py`.
2.  **Callback Handling:** A dedicated Django endpoint processes the `LNMOnline` JSON response from Safaricom.
3.  **Order Validation:** Orders are only marked as **'Paid'** after a successful `ResultCode 0` validation, ensuring financial integrity and preventing manual order status tampering.

---

## Local Setup

To run this project locally on Ubuntu:

1.  **Clone the repo:**
    ```bash
    git clone [https://github.com/bryansine/farmers-market-hub.git](https://github.com/bryansine/farmers-market-hub.git)
    cd farmers-market-hub
    ```

2.  **Environment Setup:**
    ```bash
    python3 -m venv venv
    source venv/bin/activate
    pip install -r requirements.txt
    ```

3.  **Configure Environment Variables:**
    Create a `.env` file in the root directory:
    ```text
    DEBUG=True
    SECRET_KEY=your_secret_key
    DARAJA_CONSUMER_KEY=your_key
    DARAJA_CONSUMER_SECRET=your_secret
    DARAJA_BUSINESS_SHORTCODE=your_shortcode
    ```

4.  **Migrations & Superuser:**
    ```bash
    python manage.py migrate
    python manage.py createsuperuser
    python manage.py runserver
    ```

##  Future Roadmap
- **WhatsApp Integration:** Direct order notifications via WhatsApp Business API for farmers without consistent app access.
- **Smart Season Integration:** Linking soil health and risk data from the *Smart Season* platform directly to product quality tags.
- **Offline Mode:** Service worker implementation for areas with low connectivity in rural Kenya.

Developed by [Bryan](https://github.com/bryansine)