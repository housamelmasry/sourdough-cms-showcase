# Architecture Overview

Sourdough is a Laravel application that centralizes bakery commerce and operations. It exposes versioned APIs for customer-facing clients and staff workflows, and uses Filament panels for administration. Eloquent models represent the domain; services coordinate business operations that span orders, inventory, production, and finance.

## High-Level Components

```text
React Native customer app      React Native tablet cashier      Staff / administrators
    iOS / Android                     app                               |
             |                              |                               |
             +------------------------------+-------------------------------+
                                            |
                              Laravel routes and middleware
                              routes/api.php, api_cashier.php,
                              routes/web.php
                                            |
                        Controllers, requests, API resources
                              app/Http/Controllers/
                                            |
                            Application and domain services
                                app/Services/
                                            |
                         Eloquent models and authorization
                        app/Models/ and app/Policies/
                                            |
                              Relational database
                   database/migrations/, models, relationships

                  Filament panels also use the same models,
                  services, and authorization rules for staff UI.
```

The production customer and cashier apps are React Native clients maintained separately from this Laravel backend repository. The customer app targets iOS and Android; the cashier app targets tablets. Customer/general API endpoints are versioned under `/api/v1`, and cashier endpoints are grouped under `/api/v1/cashier`.

## React Native Clients

The mobile apps are separate client applications; this repository owns their backend contracts and business operations rather than their React Native screens or native build configuration.

| Client       | Platform        | Backend integration                                                                                                                              |
| ------------ | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| Customer app | iOS and Android | Customer authentication, catalog, cart, shipping, addresses, loyalty-related features, and ordering through `/api/v1`                            |
| Cashier app  | Tablet          | Staff authentication, branch-scoped orders, till and drawer operations, tables, reports, drivers, and receipt printing through `/api/v1/cashier` |

The APIs keep business rules such as order validation, pricing, stock changes, branch scope, and till authorization on the server. This lets the client apps focus on their platform-specific user experience while using the same operational data and rules.

## Main Application Boundaries

### HTTP Entry Points

- `routes/api.php` registers customer and general API routes, including catalog, customer authentication, shipping, cart, and order functionality.
- `routes/api_cashier.php` registers cashier and waiter routes, using Sanctum authentication, token abilities, role checks, branch scoping, and till middleware where required.
- `routes/web.php` registers browser-facing routes.
- Controllers validate/coordinate HTTP requests and format responses; business operations that affect multiple records belong in the existing service layer where available.

### Domain and Services

`app/Models/` contains the Eloquent domain entities and their relationships. Major concepts include products, options, customers, orders, branches, materials, recipes, stock, production, tills, and transfers.

`app/Services/` contains workflows that coordinate domain operations. Examples include `OrderService`, `OrderStockService`, `ProductionService`, `RecipeProductionService`, `StockService`, `PricingService`, `ShippingService`, `TillService`, and `ReportService`.

Inventory and order changes can affect multiple related records. Preserve the existing transactions, stock-movement records, and authorization checks when modifying these workflows.

### Filament Administration

`app/Filament/` contains admin and branch-facing resources, pages, widgets, imports, and exports. These interfaces operate on the same application domain as the APIs rather than maintaining a separate data model. Policies and configured roles/permissions determine access to protected resources and actions.

### Persistence and Background Work

`database/migrations/` defines the schema; seeders and factories support initialization and testing. `app/Jobs/`, `app/Events/`, `app/Observers/`, and `app/Notifications/` provide the application's asynchronous and event-driven extension points where used.

## Typical Request Flows

### Customer Order

1. A client calls a `/api/v1` route.
2. Route middleware applies public or customer authentication and rate limits as configured.
3. The controller validates input and resolves the customer, branch, order type, and requested products/options.
4. Order and stock services validate availability, calculate prices and delivery charges, and create the order records.
5. The response returns the order representation; related stock changes and movement records are persisted by the relevant workflow.

Delivery, pickup, and dine-in have different address, branch, shipping, or table requirements. See [Project Skills and Features](PROJECT_SKILLS_AND_FEATURES.md) for the ordering feature overview.

### Cashier Order

1. The cashier client authenticates through the cashier API.
2. Middleware verifies the token and permitted staff role; request handling scopes orders to the staff member's branch.
3. Till-dependent actions verify the current till where required.
4. Order, stock, table, payment, and receipt workflows use the same domain records and services as appropriate.

See [Project Skills and Features](PROJECT_SKILLS_AND_FEATURES.md) for the cashier, tables, and till feature overview.

### Production and Inventory Transfer

Production checks required material or recipe availability, consumes inputs, records movements, and updates produced stock. Transfers move items through explicit lifecycle states and update source/destination branch inventory as they are shipped and received. See [Database Structure](DATABASE_STRUCTURE.md) for the related data domains and [Project Skills and Features](PROJECT_SKILLS_AND_FEATURES.md) for the inventory and production overview.

## Repository Layout

| Path                                         | Contents                                                                 |
| -------------------------------------------- | ------------------------------------------------------------------------ |
| `app/Actions/`, `app/Services/`, `app/Jobs/` | Application workflows, business services, and queued work                |
| `app/Http/`                                  | Controllers, middleware, requests, and API response resources            |
| `app/Models/`, `app/Enums/`                  | Domain entities and enumerated domain values                             |
| `app/Filament/`                              | Admin and branch panels, resources, pages, widgets, imports, and exports |
| `app/Policies/`, `app/Providers/`            | Authorization and application/service registration                       |
| `routes/`                                    | Web, customer/general API, cashier API, and console route definitions    |
| `database/`                                  | Migrations, factories, and seeders                                       |
| `resources/`, `public/`                      | Source templates/assets and web-served assets                            |
| `tests/`                                     | Feature, unit, and performance tests                                     |
| `docs/`, `scripts/`                          | Project/domain documentation and development/testing scripts             |

For a feature-oriented navigation guide, see [Project Skills and Features](PROJECT_SKILLS_AND_FEATURES.md). For database relationships, see [Database Structure](DATABASE_STRUCTURE.md).

## Showcase Documentation

- [Showcase README](README.md)
- [Database Structure](DATABASE_STRUCTURE.md)
- [Project Skills and Features](PROJECT_SKILLS_AND_FEATURES.md)
