# Laravel E-Commerce RESTful API

This project is a Laravel 5.8 RESTful API that powers a simple e-commerce backend. It exposes product and review resources with JSON responses shaped by Laravel Resource classes and uses Laravel Passport for authentication on protected routes.

## Features
- **Products API**: Public listing with pagination and single-product retrieval. Authenticated users can create, update, or delete products with validation on name, description, price, stock, and discount fields.
- **Reviews API**: Nested review endpoints under each product. Supports creating, updating, listing, and deleting reviews with validated customer name, star rating (0–5), and review body.
- **Resource transformers**: `ProductResource`, `ProductCollection`, and `ReviewResource` standardize JSON output with computed fields like discounted price, rating averages, and review links.
- **Validation**: Form Request classes (`ProductRequest`, `ReviewRequest`) centralize rules to keep controllers lean.
- **Authentication & authorization**: Laravel Passport guards product mutations; custom exceptions block unauthorized edits when ownership checks fail.
- **Error handling**: Custom exception trait supplies consistent JSON responses for missing models and invalid routes.

## API Workflows
- **Products**: `GET /api/products` (paginated list), `GET /api/products/{id}`, `POST /api/products`, `PUT/PATCH /api/products/{id}`, `DELETE /api/products/{id}`.
- **Reviews**: `GET /api/products/{product}/reviews`, `POST /api/products/{product}/reviews`, `PUT/PATCH /api/products/{product}/reviews/{id}`, `DELETE /api/products/{product}/reviews/{id}`.

## Architecture Overview
- **Routing**: `routes/api.php` defines product resources and nested review resources.
- **Controllers**: `ProductController` handles product CRUD with auth middleware and ownership checks; `ReviewController` manages reviews scoped to a product.
- **Models**: `Product` (has many `Review`) and `Review` (belongs to `Product`).
- **Requests**: Form Requests enforce validation before controllers run.
- **Resources**: API Resources shape outgoing payloads with computed totals and rating data.
- **Exceptions**: Custom exception handling ensures consistent JSON errors for missing models and 404 routes.

## Getting Started
1. Install dependencies: `composer install` and `npm install` (if you need to build front-end assets).
2. Copy `.env.example` to `.env` and configure your database and `APP_KEY` (`php artisan key:generate`).
3. Run migrations: `php artisan migrate`.
4. Install Passport keys: `php artisan passport:install`.
5. Serve the API: `php artisan serve` (default `http://localhost:8000`).

## Notes and Next Steps
- Associate the authenticated user to new products to fully enforce ownership checks.
- Add authentication/authorization to review routes if you want to restrict who can post or edit reviews.
- Consider adding filtering/sorting for products, pagination on reviews, and standardized error responses for validation/auth errors.

## License
This project is open-sourced under the [MIT license](https://opensource.org/licenses/MIT).
