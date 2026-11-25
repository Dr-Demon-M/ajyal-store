# Ajyal Store — Multi-Vendor E-Commerce Platform

A full-featured e-commerce platform built with **Laravel 12** and **PHP 8.2+**. Customers shop from multiple vendor stores through a single catalog and cart, while vendors and admins manage everything from a role-based dashboard.

## Features

### Storefront
- Product catalog with categories, tags, and per-store organization
- Cart, coupons, and multi-currency conversion
- Checkout with **Stripe** (redirect checkout + webhook for payment status updates)
- Order history with order cancellation
- Multilingual interface (`mcamara/laravel-localization`)
- Social login (Laravel Socialite), email verification, and **two-factor authentication** (Laravel Fortify)

### Admin dashboard (`/admin/dashboard`)
- Separate `admin` guard with its own authentication
- **Roles & abilities**: per-admin permissions enforced with Laravel gates (e.g. `can:admins.index`)
- Manage stores, products, categories, coupons, orders, users, and admins
- Soft deletes with trash / restore / force-delete for stores, products, and categories
- Product import
- Notifications with real-time events (**Pusher** / Laravel Echo)

### REST API
- Token-authenticated product API (`/api/product1`) with **Laravel Sanctum**
- Token issue/revoke endpoints (`/api/auth/token`)

## Tech Stack

| Layer | Tools |
| --- | --- |
| Backend | Laravel 12, PHP 8.2+, MySQL |
| Auth | Fortify (2FA), Sanctum (API tokens), Socialite (social login), custom `admin` guard |
| Payments | Stripe (`stripe/stripe-php`) |
| Real-time | Pusher, Laravel Echo |
| Frontend | Blade, Vite, Tailwind CSS, Alpine.js, jQuery |
| i18n | mcamara/laravel-localization, symfony/intl |

## Installation

**Requirements:** PHP 8.2+, Composer, Node.js 18+, MySQL

```bash
# 1. Clone the repository
git clone https://github.com/Dr-Demon-M/ajyal-store.git
cd ajyal-store

# 2. Install PHP dependencies
composer install

# 3. Environment setup
cp .env.example .env
php artisan key:generate

# 4. Create a MySQL database (default name: store)
#    then set DB_DATABASE / DB_USERNAME / DB_PASSWORD in .env

# 5. Run migrations and seeders
php artisan migrate --seed

# 6. Install and build frontend assets
npm install
npm run build        # or: npm run dev

# 7. Serve the app
php artisan serve
```

> Steps 2–6 can also run in one shot with `composer run setup` (uses `migrate --force` without seeding).

### Optional services

The app works locally without these, but the related features need keys in `.env`:

| Feature | .env keys |
| --- | --- |
| Stripe checkout | `STRIPE_KEY`, `STRIPE_SECRET`, webhook secret |
| Real-time notifications | `PUSHER_APP_ID`, `PUSHER_APP_KEY`, `PUSHER_APP_SECRET`, `PUSHER_APP_CLUSTER`, `BROADCAST_CONNECTION=pusher` |
| Social login | provider client ID/secret (Laravel Socialite) |
| Mail (verification, 2FA) | `MAIL_*` |

The admin dashboard lives at `/admin/dashboard` and requires an admin account (see `UserSeeder` / dashboard admin management).

## Testing

```bash
php artisan test
```
