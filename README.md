# WebGIS Incident Management System

## 1. Project Overview

This project is a **Web-based Geographic Information System (WebGIS)** developed as part of the course requirements. The system allows users to create, manage, and analyze spatial incident reports through a role-based architecture. The application demonstrates the use of spatial databases, RESTful APIs, authentication, authorization, and performance analysis techniques.

The main goal of the project is to design a functional WebGIS application that supports spatial data operations, team management, and performance evaluation without relying on external map servers or third-party APIs.

---

## 2. System Architecture

The system follows a **client–server architecture**:

* **Frontend:** HTML, CSS, JavaScript
* **Backend:** Node.js (Express.js)
* **Database:** PostgreSQL with PostGIS extension
* **API Documentation:** Swagger (OpenAPI)

All components run locally and communicate through RESTful HTTP requests.

---

## 3. User Roles and Authorization

The system supports role-based access control with three user types:

* **User:** Can create spatial incident reports and view reports.
* **Worker:** Can update the status of assigned reports.
* **Manager:** Can assign teams to reports, manage teams, and delete reports.

Authentication is handled using **JWT (JSON Web Tokens)**, ensuring secure access to protected endpoints.

---

## 4. Database Design

The spatial database is implemented using **PostgreSQL + PostGIS**.

### Tables:

* **users:** Stores user credentials and roles
* **reports:** Stores spatial incident reports (POINT geometry)
* **teams:** Stores team information and availability status

Spatial data is stored using EPSG:4326 coordinate reference system.

---

## 5. CRUD Operations

The application fully supports CRUD operations:

* **Create:** Users can create new spatial reports
* **Read:** All users can retrieve reports
* **Update:** Managers assign teams, workers update report status
* **Delete:** Managers can delete reports

All CRUD operations are implemented via RESTful API endpoints.

---

## 6. REST API Development

A RESTful API was developed to manage both spatial and non-spatial data.

### Main Endpoints:

* `POST /register` – User registration
* `POST /login` – User authentication
* `GET /reports` – Retrieve spatial reports
* `POST /reports` – Create a spatial report
* `PUT /reports/{id}/assign` – Assign team (Manager)
* `PUT /reports/{id}/status` – Update status (Worker)
* `DELETE /reports/{id}` – Delete report (Manager)
* `GET /teams` – Retrieve teams (Manager)

---

## 7. API Documentation (Swagger)

The API is documented using **Swagger UI**, which provides an interactive interface for testing and exploring the endpoints.

Swagger documentation clearly shows request/response structures, authentication requirements, and role-based access restrictions.

Swagger UI is available at:

```
http://localhost:3000/api-docs
```

---

## 8. Spatial Data Usage

Spatial data is handled using **PostGIS geometry types**. Incident locations are stored as POINT geometries.

Spatial queries include:

* Distance-based filtering using `ST_DWithin`
* Bounding box filtering

---

## 9. Spatial Index Experiment

A **GiST spatial index** was created on the geometry column of the `reports` table.

### Query Without Index:

* Sequential Scan
* Higher execution time

### Query With Index:

* Bitmap Index Scan
* Significantly reduced execution time

The experiment demonstrates the performance improvement achieved by spatial indexing.

---

## 10. Performance Testing

Performance testing was conducted using **Artillery**.

Load tests simulated multiple concurrent users accessing the API endpoints. Metrics such as response time, request rate, and error rates were analyzed.

The results confirm that the system can handle concurrent requests efficiently under load.

---

## 11. Testing Tools

* **Postman:** Manual API testing
* **Swagger UI:** Interactive API testing and documentation
* **Artillery:** Load and performance testing

---

## 12. Installation and Execution

### Requirements:

* Node.js
* PostgreSQL
* PostGIS

### Steps:

```bash
npm install
node server.js
```

---

## 13. Conclusion

This project successfully demonstrates the development of a WebGIS application with spatial data management, role-based authorization, RESTful API design, spatial indexing, and performance testing. The system meets all mandatory and selected optional requirements defined in the course guidelines.

---

## 14. Author

**Engin Gökhan Sefer**
