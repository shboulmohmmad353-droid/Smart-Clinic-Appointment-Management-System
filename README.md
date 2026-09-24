# SmartClinic — Smart Clinic Appointment Management System

A web-based clinic platform built with **ASP.NET Core MVC**, where patients find doctors and book appointments, doctors manage their schedules, and an administrator runs the whole system.

---

## 📋 Description

The Smart Clinic Appointment Management System connects three groups of people around one clinic:

- **Patients** — self-register, search for doctors by name or medical specialty, open a doctor's profile, and book an appointment in one of the published time slots.
- **Doctors** — log in to a private dashboard, review incoming appointment requests, accept or reject them, manage their availability schedule, and mark appointments as completed.
- **Administrator** — manages doctors, patients, specialties, appointments, public website content (Home page, About, Services, Testimonials, Contact info), contact messages, and reports.

### Appointment workflow
`Pending → Accepted → Completed` — with `Rejected` and `Cancelled` as terminal states.

---

## 🛠️ Technologies

| Layer | Technology |
|---|---|
| Platform | Visual Studio 2022+, .NET / ASP.NET Core MVC, C# |
| Data | SQL Server, Entity Framework Core, LINQ & Migrations |
| Front end | Bootstrap 5, HTML & CSS, JavaScript & Chart.js |
| Services | REST API controllers, Swagger, Dependency Injection |
| Security | Cookie authentication, Password hashing, Anti-forgery tokens |

---

## ✅ Prerequisites

- Visual Studio 2022 or newer
- .NET 8 SDK (or newer)
- SQL Server (LocalDB is enough for development)
- EF Core tools (usually bundled with Visual Studio)

---

## ⚙️ Installation Steps

1. **Get the source code**
   ```bash
   git clone &lt;your-repository-url&gt;
   ```
   or extract the submitted archive.

2. **Open the solution**
   - Open `SmartClinic.sln` in Visual Studio.

3. **Configure the connection string**
   - Open `appsettings.json` and set your SQL Server connection string:
   ```json
   "ConnectionStrings": {
     "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=SmartClinicDb;Trusted_Connection=true;TrustServerCertificate=true"
   }
   ```

4. **Create the database** — open **Package Manager Console** (Tools → NuGet Package Manager) and run:
   ```powershell
   Update-Database
   ```
   This creates the database, all tables, and seeds the initial data.
   &gt; If you need to recreate it from scratch:
   &gt; ```powershell
   &gt; Drop-Database
   &gt; Update-Database
   &gt; ```

5. **Run the application**
   - Press **F5** or `Ctrl+F5` in Visual Studio.

---

## 🔐 Default Login Accounts

The database is seeded with one account per role:

| Role | Email | Password |
|---|---|---|
| **Admin** | admin@clinic.com | Admin@123 |
| **Doctor** | doctor@clinic.com | Doctor@123 |
| **Patient** | patient@clinic.com | Patient@123 |

&gt; Patients can also be created at any time through the public **Register** page.

---

## 🗂️ Project Structure

```
SmartClinic/
├── Controllers/        # MVC controllers (receive requests, call services, return views)
├── Controllers/Api/    # REST API controllers (return JSON)
├── Models/             # EF Core entities
├── ViewModels/         # Form/list view models
├── Services/           # Business logic (booking, status changes, reports)
├── Data/               # DbContext, entity configurations, seed data
├── Views/              # Razor views grouped by controller
├── wwwroot/            # Static files (CSS, JS, images)
└── appsettings.json    # Configuration and connection string
```

---

## 📡 API Endpoints (Swagger)

After running the app, open `/swagger` to test the JSON endpoints:

| Endpoint | Access | Returns |
|---|---|---|
| `GET /api/doctors` | Public | All active doctors (with optional `name` / `specialty` filters) |
| `GET /api/doctors/{id}` | Public | One doctor's details (HTTP 404 if not found) |
| `GET /api/specialties` | Public | All specialties with doctor count |
| `GET /api/appointments` | Admin only | Appointments with filters by status and date |
| `GET /api/statistics` | Admin only | Dashboard chart data (optional) |

&gt; API responses return DTOs/ViewModels only — never entities or password hashes.

---

## 🧪 Main Functionality to Try

1. **Admin** — view dashboard cards & charts, manage doctors, specialties, patients, website content, and cancel appointments.
2. **Doctor** — add availability slots, accept / reject / complete appointments, edit own profile.
3. **Patient** — register, search and filter doctors, book an available slot, follow the status in "My Appointments", cancel when allowed.

---

## 📌 Notes

- All business rules (BR-01 … BR-15) are enforced **server-side**, not only in the UI.
- Every list, count, and chart reads from the database — no hard-coded data.
- Run the project at least once on a clean machine before the presentation.

---

**Project deadline:** 10-10-2026
