<h1 align="center">🥖 Sourdough Management System</h1>

<p align="center">
  <em>A bakery commerce and operations platform connecting customer ordering, point of sale, inventory, and production.</em>
</p>

<p align="center">
  <a href="https://laravel.com"><img src="https://img.shields.io/badge/Laravel-13.x-FF2D20?logo=laravel&logoColor=white" /></a>
  <a href="https://filamentphp.com/"><img src="https://img.shields.io/badge/Filament-v5-8A2BE2?logo=laravel&logoColor=white" /></a>
  <a href="https://www.php.net/"><img src="https://img.shields.io/badge/PHP-%5E8.3-blue?logo=php&logoColor=white" /></a>
</p>

---

<h2>🚀 Overview</h2>

<p>
The <strong>Sourdough Management System</strong> is a bakery commerce and operations platform built with <strong>Laravel 13</strong> and <strong>Filament 5</strong>. It provides the backend APIs and administration panels for a production React Native customer app on iOS and Android, a React Native cashier app for tablets, and multi-branch bakery operations.
</p>

<blockquote>
  📌 This is a public showcase of a private, production-grade project. Source code, credentials, and client-specific business logic are not included here.
</blockquote>

<p><strong>Customer app:</strong> <a href="https://apps.apple.com/eg/app/sourdough-house/id6756028598?l=ar">App Store</a> · <a href="https://play.google.com/store/apps/details?id=com.sourdough.sourdoughapp&amp;hl=ar">Google Play</a></p>

---

<h2>⚙️ Tech Stack</h2>

<table>
  <tr><th>Layer</th><th>Technology</th></tr>
  <tr><td>Language / Runtime</td><td>PHP 8.3+</td></tr>
  <tr><td>Backend Framework</td><td>Laravel 13</td></tr>
  <tr><td>Admin Panel</td><td>Filament 5</td></tr>
  <tr><td>Customer and POS Apps</td><td>React Native (iOS, Android, and tablet)</td></tr>
  <tr><td>Web Asset Pipeline</td><td>Vite 5, Tailwind CSS 3</td></tr>
  <tr><td>Database</td><td>MySQL / MariaDB</td></tr>
  <tr><td>API Authentication</td><td>Laravel Sanctum</td></tr>
  <tr><td>OAuth / Google Sign-In</td><td>Laravel Socialite, Google API Client</td></tr>
  <tr><td>Optional AI Integration</td><td>Laravel AI</td></tr>
  <tr><td>Media Management</td><td>Spatie Laravel Media Library</td></tr>
</table>

---

<h2>🧩 Main Features</h2>

<ul>
  <li><strong>Customer commerce</strong> — Product catalog, configurable options, cart, delivery, pickup, customer accounts, and order tracking.</li>
  <li><strong>Mobile ordering</strong> — Production React Native apps for iOS and Android.</li>
  <li><strong>Tablet point of sale</strong> — Cashier workflows for orders, tills, drawers, tables, reports, drivers, and receipts.</li>
  <li><strong>Bakery operations</strong> — Materials, recipes, cost calculation, production, purchasing, waste tracking, and stock movements.</li>
  <li><strong>Multi-branch control</strong> — Branch-level product and ingredient stock, transfers, thresholds, and operational access.</li>
  <li><strong>Administration</strong> — Filament resources for catalog, branches, inventory, orders, and configurable website pages.</li>
</ul>

---

<h2>🗂 High-Level Architecture</h2>

<pre><code>app/
├── Http/
│   ├── Controllers/       # API + Admin controllers
│   └── Resources/         # Filament Resources
├── Models/                # Eloquent models
├── Services/              # API integrations (WooCommerce, Foodics)
database/
├── migrations/            # DB structure
├── seeders/               # Initial data
docs/                      # API documentation (Markdown)
routes/
├── api.php
├── web.php
└── filament.php
</code></pre>

<p><em>Note: this structure is illustrative — the full source is kept in a private repository.</em></p>

<h2>📚 Showcase Documentation</h2>

<ul>
  <li><a href="./ARCHITECTURE_OVERVIEW.md">Architecture Overview</a> — application components, boundaries, and request flows.</li>
  <li><a href="./DATABASE_STRUCTURE.md">Database Structure</a> — logical data domains and core relationships.</li>
  <li><a href="./PROJECT_SKILLS_AND_FEATURES.md">Project Skills and Features</a> — platform capabilities and feature areas.</li>
</ul>

<h2>🗄 Database Structure</h2>

<p>The relational schema is organized around customers, products, recipes and materials, branch-level stock, orders, production, transfers, and POS finance. The public <a href="./DATABASE_STRUCTURE.md">Database Structure</a> guide summarizes the main table groups and relationships. It is a logical overview, not a full schema dump.</p>

---

<h2>📡 API Access</h2>

<p>
All API endpoints are secured with <strong>Laravel Sanctum</strong>. Endpoint details are documented internally and not published in this showcase repo.
</p>

---

<h2>💡 Future Enhancements</h2>

<ul>
  <li>🔄 Real-time webhook sync for stock updates</li>
  <li>📊 Filament dashboards for analytics</li>
  <li>🏭 Production scheduling and planning module</li>
  <li>📦 Auto purchase order generation based on thresholds</li>
</ul>

---

<h2>👤 Author</h2>

<p>
  <strong>Housam ElMasry</strong><br/>
  Backend & Mobile Engineer — Laravel/Filament, Go, React Native, NestJS<br/>
  🔗 <a href="https://www.linkedin.com/in/housamelmasry/">LinkedIn</a> · <a href="https://github.com/housamelmasry">GitHub</a>
</p>

<p><em>For inquiries about this project, please reach out via LinkedIn or GitHub rather than direct contact details.</em></p>

---

<h2>🪪 License</h2>

<p>This showcase README is shared for portfolio purposes. The underlying codebase is proprietary and not licensed for reuse.</p>

<blockquote>
  "From sourdough to system — bringing artisanal precision to modern bakery management."
</blockquote>
