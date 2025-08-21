# PahanaSuite

PahanaSuite is a web-based management system for the Pahana Edu Bookshop. It is built with JSPs and plain Jakarta Servlet 6 APIs and packaged as a WAR for deployment to any servlet container.

## Architecture

- **Presentation layer** &mdash; JSP pages backed by lightweight servlets.  Common page chrome is factored into `header.jsp` and `nav.jsp` includes.
- **Persistence layer** &mdash; simple DAO classes wrapping MySQL queries.  Connection parameters live in [`DBConnectionFactory`](src/main/java/com/pahanaedu/pahanasuite/dao/DBConnectionFactory.java) and should be adjusted for your environment.
- **JSON utilities** &mdash; Jackson is used to serialize/deserialize data where needed.

## Features

PahanaSuite bundles several day‑to‑day bookshop workflows:

- **Users** &mdash; manage staff accounts and enforce role‑based permissions.
- **Customers** &mdash; capture customer details and history.
- **Items** &mdash; maintain the inventory catalog.
- **Sales / Billing** &mdash; create invoices, process payments and view past bills.
- **Reports** &mdash; produce summaries of sales and stock levels.
- **Settings** &mdash; update shop metadata and configuration values.
- **Help** &mdash; built‑in guide to using each module.

The dashboard automatically loads the correct section based on the logged‑in user's role and exposes reusable navigation and header components.

## Requirements

- Java 21 or later
- Maven 3.9+ (Maven Wrapper included)
- MySQL 8 (or compatible)

## Building

Clone the repository and run the Maven wrapper to compile and package the application:

```bash
./mvnw clean package
```

The generated `PahanaSuite.war` will be placed in the `target` directory.

## Database Setup

1. Install MySQL and create a database named `pahanaedu`.
2. Update credentials in [`DBConnectionFactory`](src/main/java/com/pahanaedu/pahanasuite/dao/DBConnectionFactory.java) to match your environment.
3. Create required tables (schema scripts are not yet provided).

## Running

Copy the built WAR to the `webapps` directory of a Jakarta EE 10 compatible container (e.g. Tomcat 10 or Jetty 11) and start the server.  The application will be available at:

```
http://localhost:8080/PahanaSuite
```

## Project Layout

```
PahanaSuite/
├── pom.xml
├── mvnw, mvnw.cmd
├── .mvn/
├── .github/workflows/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/pahanaedu/pahanasuite/
│   │   │       ├── dao/
│   │   │       │   └── impl/
│   │   │       ├── factories/
│   │   │       ├── models/
│   │   │       ├── security/
│   │   │       ├── services/
│   │   │       └── web/
│   │   └── webapp/
│   │       ├── css/
│   │       ├── js/
│   │       ├── dashboard.jsp
│   │       ├── index.jsp
│   │       ├── login.jsp
│   │       └── WEB-INF/
│   │           ├── web.xml
│   │           └── views/
│   └── test/
│       └── java/
```

## Testing
