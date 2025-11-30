# API Reference

This document outlines the REST API endpoints available in the Arogya Saathi backend. All responses return JSON.

## Base URL

Local: `http://localhost:8000`

## Authentication

### 1. Send OTP

Initiates the login process. If the phone number does not exist, a new user account is auto-provisioned.

* **Endpoint:** `/auth/send-otp`
* **Method:** `POST`
* **Body:**

  ```json
  {
    "phone_number": "+919876543210",
    "role": "patient"  // or "doctor"
  }

* **Response (200 OK):**

    ```json
    {
      "status": "success",
      "message": "OTP Sent",
      "debug_otp": "1234"
    }
    ```

### 2\. Verify OTP

Verifies the provided code and returns the user session data.

* **Endpoint:** `/auth/verify-otp`
* **Method:** `POST`
* **Body:**

    ```json
    {
      "phone_number": "+919876543210",
      "otp": "1234",
      "role": "patient"
    }
    ```

* **Response (200 OK):** Returns the user object, including ID and onboarded status.

## Patient Operations

### 1\. Trigger Voice Call

Simulates an incoming call from the AI Doctor to the patient's phone number via Twilio.

* **Endpoint:** `/patient/trigger-call`
* **Method:** `POST`
* **Body:**

    ```json
    {
      "phone_number": "+919876543210",
      "reason": "Routine Checkup"
    }
    ```

### 2\. Update Profile

Updates demographic details after initial registration.

* **Endpoint:** `/patient/update-profile`
* **Method:** `PUT`
* **Body:**

    ```json
    {
      "phone_number": "+919876543210",
      "full_name": "Rudra Sawant",
      "age": 28
    }
    ```

## Doctor Operations

### 1\. Update Greeting

Configures the custom TTS message played to patients upon call connection.

* **Endpoint:** `/doctor/update-greeting`
* **Method:** `PUT`
* **Body:**

    ```json
    {
      "phone_number": "+919999999999",
      "new_greeting": "Namaste! This is Dr. Sharma's AI assistant."
    }
    ```

## Analytics

### 1\. Get Dashboard Stats

Retrieves aggregated data for the Doctor Portal.

* **Endpoint:** `/analytics/dashboard-stats`
* **Method:** `GET`
* **Response:**

    ```json
    {
      "total_patients": 120,
      "critical_cases": 5,
      "avg_adherence": 85
    }
    ```
