# Restful Booker API Automation & Testing

![Postman](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white)
![NodeJS](https://img.shields.io/badge/Node.js-43853D?style=for-the-badge&logo=node.js&logoColor=white)
![Newman](https://img.shields.io/badge/Newman-FF6C37?style=for-the-badge&logo=postman&logoColor=white)

Automated end-to-end API testing framework for the [Restful Booker API](https://restful-booker.herokuapp.com) built with Postman and Newman. This repository demonstrates dynamic test data generation, runtime variable chaining, assertions, and command-line execution with HTML reporting.

---

## 📌 Key Features

* **Dynamic Mock Data Generation:** Uses Postman dynamic variables (`$randomFirstName`, `$randomLastName`, `$randomInt`, `$randomBoolean`, `$randomNoun`) and `Moment.js` pre-request scripts for data-driven testing.
* **Variable Chaining:** Captures runtime identifiers (e.g., `booking_id`, authentication `token`) to execute sequential requests seamlessly.
* **Comprehensive Assertions:** Verifies HTTP status codes, payload field presence/data types, payload match validations, response times (<1000ms), and response size limits.
* **CLI & CI/CD Ready:** Executable via **Newman** for automated headless testing and HTML execution report generation.

---

## 🛠️ Tech Stack

| Tool / Library | Purpose |
| :--- | :--- |
| **Postman** | API collection design and test script execution |
| **Newman** | Command-line runner for Postman collections |
| **JavaScript / Chai** | Pre-request dynamic scripting & assertion scripts |
| **Moment.js** | Dynamic check-in and check-out date calculations |

---

## 🚀 Test Workflow & Endpoints

| Step | Request Name | Method | Endpoint | Description |
| :---: | :--- | :---: | :--- | :--- |
| `01` | **Post_request** | `POST` | `/booking` | Creates a new booking using dynamically generated values and saves `booking_id`. |
| `02` | **Get_Bookings** | `GET` | `/booking` | Fetches all booking IDs to ensure server list response validity. |
| `03` | **Get_bookingsId** | `GET` | `/booking/{{booking_id}}` | Fetches details for the newly created booking ID and validates schema. |
| `04` | **Create_token** | `POST` | `/auth` | Generates authentication token (`admin`/`password123`) for write operations. |
| `05` | **Update_bookings** | `PUT` | `/booking/{{booking_id}}` | Full payload update authorized via token header cookie. |
| `06` | **Get_alreadyBooking** | `GET` | `/booking/{{booking_id}}` | Retrieves booking to confirm full updates persisted correctly. |
| `07` | **Partial_Update_bookings** | `PATCH` | `/booking/{{booking_id}}` | Partial update (firstname/lastname) authorized via token header. |
| `08` | **Delete_booking** | `DELETE` | `/booking/{{booking_id}}` | Deletes the specified booking ID from the system. |
| `09` | **Ping** | `GET` | `/ping` | Health-check endpoint verifying API server status. |

---

## 🔑 Environment Variables

The project uses `Environment_API.postman_environment.json` to store runtime variables:

| Variable | Scope | Description |
| :--- | :--- | :--- |
| `base_url` | Environment | Target API Base URL (`https://restful-booker.herokuapp.com`) |
| `token` | Dynamic | Extracted auth token for PUT/PATCH/DELETE requests |
| `booking_id` | Dynamic | Extracted ID created during `Post_request` |
| `fname`, `lname` | Dynamic | Dynamic guest first and last names |
| `tprice`, `dpaid` | Dynamic | Dynamic total price and payment deposit boolean |
| `checkin`, `checkout` | Dynamic | Calculated dates via Moment.js |
| `additionalneeds` | Dynamic | Dynamic string for additional guest needs |

---

## 📥 Setup & Usage

### Prerequisites
* [Postman Desktop App](https://www.postman.com/downloads/)
* [Node.js](https://nodejs.org/) (v14.x or higher)

### Import to Postman
1. Clone this repository:
   ```bash
   git clone [https://github.com/your-username/your-repo-name.git](https://github.com/your-username/your-repo-name.git)
   cd your-repo-name

🧪 CLI Execution & Reporting
Run with Newman CLI

Ensure Newman is installed globally:
npm install -g newman

Execute the collection with the environment file:
newman run "API testing.postman_collection.json" -e "Environment_API.postman_environment.json"

.
├── API testing.postman_collection.json     # Postman collection with test scripts
├── Environment_API.postman_environment.json # Environment configuration file
├── reports                                # Generated Newman HTML execution reports
└── README.md                               # Project documentation
