# 🏫 School Management ERP

A full-featured, offline-first desktop ERP for school administration — built with **Spring Boot 3** + **JavaFX 21** + **H2 embedded database**.

---

## 📦 Tech Stack

| Layer       | Technology                          |
|-------------|-------------------------------------|
| Backend     | Spring Boot 3.2.3, Spring Data JPA  |
| Frontend    | JavaFX 21 (FXML + CSS)              |
| Database    | H2 (file-based, embedded)           |
| Build Tool  | Maven 3.8+                          |
| Java        | Java 21 (LTS)                       |
| Other       | Lombok, Apache POI, iText           |

---

## 🖥️ Features

### 📊 Dashboard
- Live stats: students, teachers, fee collection, books, notices
- Bar chart of student distribution by class
- Recent notices feed
- Quick action buttons

### 👨‍🎓 Student Management
- Full CRUD with tabbed form (Personal / Academic / Parent / Medical)
- Filter by class, section, status
- Live search
- Double-click student profile with attendance, results, fees
- Export to Excel

### 👩‍🏫 Teacher Management
- Full CRUD with designation, department, salary, qualification
- Filter by department and status

### ✅ Attendance
- Daily class-wise attendance marking with 5 statuses per student
  (Present / Absent / Late / Half-Day / Leave)
- Mark-all-present / Mark-all-absent
- Attendance statistics with percentage display
- Monthly report export

### 💰 Fee Management
- **Collect Fee** tab: student search, fee category selection, discount/fine/balance auto-calculation, payment mode, receipt generation
- **Payment History** tab: filterable by date range and status
- **Fee Structure** tab: CRUD for fee categories

### 📝 Examinations
- Exam CRUD with class, date range, status management
- Status: UPCOMING → ONGOING → COMPLETED → RESULT_DECLARED

### 🏆 Results
- Enter marks per student per subject per exam
- Auto-calculated grades (A+/A/B/C/D/F) and pass/fail
- Generate report cards (PDF export)

### 📅 Timetable
- Class & section-wise timetable view
- Add/remove periods

### 📚 Library
- Book catalog with CRUD and availability tracking
- Issue books to students with due date
- One-click return with automatic fine calculation (₹2/day)
- Overdue tracking

### 📢 Notice Board
- Publish/archive notices with audience targeting
- Categories: Academic, Exam, Holiday, Sports, Circular, Urgent
- Audiences: All, Students, Teachers, Parents, Staff

### 🏫 Classes & Sections
- Manage all classes, sections, and subjects in one view

### 👷 Non-Teaching Staff
- Staff directory with role, salary, joining date

### 📈 Reports & Analytics
- Student List, Attendance Report, Fee Collection, Result Analysis, Library Report
- Export to PDF and Excel

---

## 🚀 Setup & Run

### Prerequisites

- **Java 21** — [Download](https://adoptium.net/)
- **Maven 3.8+** — [Download](https://maven.apache.org/)

### Quick Start (Windows)

```bat
git clone <repo-url>
cd school-management
run.bat
```

### Quick Start (Linux / Mac)

```bash
git clone <repo-url>
cd school-management
chmod +x run.sh
./run.sh
```

### Manual Steps

```bash
# Build
mvn clean package -DskipTests

# Run via Maven JavaFX plugin (recommended)
mvn javafx:run

# Or run the JAR directly
java --add-modules javafx.controls,javafx.fxml \
     --add-opens javafx.graphics/com.sun.javafx.application=ALL-UNNAMED \
     -jar target/school-management-erp-1.0.0.jar
```

---

## 🗄️ Database

- **Engine**: H2 (embedded file-based)
- **Location**: `./schoolerp-data.mv.db` (auto-created on first run)
- **H2 Console** (dev): [http://localhost:8099/h2-console](http://localhost:8099/h2-console)
  - JDBC URL: `jdbc:h2:file:./schoolerp-data`
  - Username: `sa` | Password: `school123`
- Schema is auto-created by Hibernate (`ddl-auto=update`)
- Sample data loaded on first run by `DataInitializer`

---

## 📁 Project Structure

```
school-management/
├── src/main/java/com/school/
│   ├── SchoolApp.java              # Entry point (JavaFX Application + @SpringBootApplication)
│   ├── config/
│   │   └── DataInitializer.java   # Sample data seeder
│   ├── model/                     # JPA Entities (Student, Teacher, ClassRoom, ...)
│   ├── repository/
│   │   └── PublicRepos.java       # All Spring Data JPA repositories
│   ├── service/
│   │   └── SchoolService.java     # Business logic layer
│   └── ui/
│       ├── MainController.java    # Sidebar navigation, page loading
│       ├── DashboardController.java
│       ├── StudentController.java
│       ├── StudentFormDialog.java
│       ├── StudentProfileDialog.java
│       ├── TeacherController.java
│       ├── AttendanceController.java
│       ├── FeeController.java
│       ├── OtherControllers.java  # Library, Exams, Results, Notices, Timetable, Classes, Staff, Reports
│       └── UIHelper.java          # Dialog/alert utilities
├── src/main/resources/
│   ├── application.properties
│   ├── css/
│   │   └── style.css              # Master stylesheet
│   └── fxml/
│       ├── main.fxml              # Root layout
│       ├── dashboard.fxml
│       ├── students.fxml
│       ├── teachers.fxml
│       ├── attendance.fxml
│       ├── fees.fxml
│       ├── library.fxml
│       ├── exams.fxml
│       ├── results.fxml
│       ├── notices.fxml
│       ├── timetable.fxml
│       ├── classes.fxml
│       ├── staff.fxml
│       └── reports.fxml
├── pom.xml
├── run.sh
├── run.bat
└── README.md
```

---

## 🎨 Default Login / Seeded Data

On first run, the app loads:
- **14 Classes**: Nursery, KG, 1–12 with sections A & B
- **10 Teachers** across departments
- **15 Students** in Class 6-A
- **8 Subjects** (Math, Science, English, Hindi, SST, CS, PE, Art)
- **6 Fee Structures** (Tuition, Admission, Sports, Library, Lab, Exam)
- **10 Books** in library
- **4 Notices**
- **6 Non-Teaching Staff**

---

## 🏗️ Key Design Patterns

| Pattern | Usage |
|---------|-------|
| Spring DI in JavaFX | `loader.setControllerFactory(springContext::getBean)` |
| Page caching | `MainController.pageCache` (HashMap, invalidatable) |
| Builder pattern | All entities use `@Builder` (Lombok) |
| Auto-IDs | `ADM{yr}{####}`, `EMP####`, `RCP{yr}{#####}`, `STF####` |

---

## 📝 License

MIT License — Free to use for educational and non-commercial purposes.
