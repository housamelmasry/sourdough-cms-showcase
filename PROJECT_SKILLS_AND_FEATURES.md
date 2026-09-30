# Project Skills and Features

This guide describes the capabilities implemented by the Sourdough platform and points contributors to the code and deeper documentation for each area. The platform includes production React Native client apps: a customer app for iOS and Android, and a cashier app for tablets. Their source code is maintained separately from this Laravel backend repository; this repository provides the APIs and administration system they use.

## Client Applications

### Customer App

The production React Native customer app is available for iOS and Android:

- [Download on the App Store](https://apps.apple.com/eg/app/sourdough-house/id6756028598?l=ar)
- [Get it on Google Play](https://play.google.com/store/apps/details?id=com.sourdough.sourdoughapp&hl=ar)

The app connects to the customer API for account, catalog, cart, shipping, address, and order workflows. The React Native app source is maintained outside this backend repository.

### Cashier App

The production React Native cashier app is designed for tablets. It connects to the branch-scoped cashier API for order entry, till and drawer operations, tables, reports, driver assignment, and receipt printing. Its source is maintained separately from this repository.

## Feature Areas

### Product Catalog and Ordering

- Organize products with categories, visibility, featured status, media, and branch availability.
- Publish offers and provide branch, city, and delivery-zone data used by ordering clients.
- Configure product options and customizations, including additional or override pricing and associated material or recipe consumption.
- Expose customer-facing catalog, offer, branch, shipping, cart, wishlist, and order workflows through the versioned API.
- Support delivery, pickup, and dine-in order types, with order status updates and stock validation.

See [Architecture Overview](ARCHITECTURE_OVERVIEW.md) for the request and application flow, and [Database Structure](DATABASE_STRUCTURE.md) for the product and order data relationships.

### Inventory, Recipes, and Production

- Track materials, recipes, and finished products with branch-level quantities and stock thresholds.
- Convert between storage and ingredient units and calculate product and recipe costs from their inputs.
- Record stock movements for purchasing, production, sales, adjustments, and transfers.
- Manage production orders and recipe production, including availability checks and material consumption.
- Transfer inventory between branches through request, approval, shipment, receipt, and cancellation stages.
- Purchase materials from suppliers, route deliveries to branches, and update stock when purchases are received.

See [Database Structure](DATABASE_STRUCTURE.md) for inventory, recipe, production, purchasing, and transfer data, and [Architecture Overview](ARCHITECTURE_OVERVIEW.md) for the related application boundaries.

### Cashier, Tables, and Till Operations

- Provide a branch-scoped cashier API for order entry, order lookup, status updates, and receipt printing.
- Manage till opening and closing, cash drawer operations, reports, table assignments, and walk-in customers.
- Apply role and branch checks to staff operations; cashier order creation and status changes can require an open till.
- Support waiter workflows and driver-assigned orders, delivery status/location updates, and driver statistics through role-aware API routes.

See [Architecture Overview](ARCHITECTURE_OVERVIEW.md) for the cashier request flow and [Database Structure](DATABASE_STRUCTURE.md) for POS and order data relationships.

### Website Content Management

- Edit and publish the Privacy Policy, Terms of Service, welcome page, and other slug-based pages through Filament.
- Serve published page content through browser-facing routes.

See [Architecture Overview](ARCHITECTURE_OVERVIEW.md) for the web and administration boundaries.

### Customer Accounts and Loyalty

- Authenticate customer API requests and manage customer addresses and order history.
- Provide loyalty points and wishlist-related customer workflows.
- Support customer registration, login, password recovery, and Google sign-in routes.

See [Architecture Overview](ARCHITECTURE_OVERVIEW.md) for API boundaries and [Database Structure](DATABASE_STRUCTURE.md) for customer and loyalty data domains.

### Administration and Access Control

- Manage catalog, inventory, branches, transfers, orders, and operational records through Filament resources.
- Organize administration and branch-facing resources separately under `app/Filament/`.
- Use policies, roles, permissions, and Filament Shield to control access to protected operations.

## Code Map

| Area                    | Primary location                                                          | Responsibility                                                                     |
| ----------------------- | ------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| Domain models           | `app/Models/`                                                             | Eloquent entities, relationships, casts, and model-level behavior                  |
| Business services       | `app/Services/`                                                           | Order, stock, production, pricing, shipping, till, drawer, and reporting workflows |
| HTTP APIs               | `app/Http/Controllers/Api/`                                               | Customer, cashier, driver, and other API request handling                          |
| API route registration  | `routes/api.php`, `routes/api_cashier.php`                                | Versioned customer and cashier route groups and middleware                         |
| Web routes              | `routes/web.php`                                                          | Browser-facing routes                                                              |
| Admin UI                | `app/Filament/Resources/`, `app/Filament/Pages/`, `app/Filament/Widgets/` | Filament resources, pages, and dashboards                                          |
| Authorization           | `app/Policies/`, `app/Providers/`                                         | Policy checks and application authorization setup                                  |
| Schema and initial data | `database/migrations/`, `database/seeders/`, `database/factories/`        | Database schema, seed data, and test data factories                                |
| Tests                   | `tests/Feature/`, `tests/Unit/`, `tests/Performance/`                     | Automated feature, unit, and performance coverage                                  |
| Frontend assets         | `resources/`, `public/`, `vite.config.js`                                 | Blade views, CSS/JS source, and built public assets                                |
| Project documentation   | `docs/`                                                                   | API contracts, domain workflows, database references, and operations guides        |

## Contributor Skills

When changing the project, contributors should be able to:

- Trace a request from its route and middleware through a controller to a service and model.
- Preserve branch scope, role permissions, and authentication boundaries when changing APIs.
- Keep stock mutations and related movement records consistent, preferably within the existing transactional service flow.
- Follow existing unit-conversion and pricing rules for recipes, materials, products, and options.
- Update API documentation or domain-flow documents when changing externally visible behavior.
- Add or update focused PHPUnit tests for changed business rules and run the relevant checks.

For the broader component relationships, see [Architecture Overview](ARCHITECTURE_OVERVIEW.md). For database entities, see [Database Structure](DATABASE_STRUCTURE.md).

## Showcase Documentation

- [Showcase README](README.md)
- [Architecture Overview](ARCHITECTURE_OVERVIEW.md)
- [Database Structure](DATABASE_STRUCTURE.md)
