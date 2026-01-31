# TopHoliday Travel and Tours Application

A comprehensive travel management system built with Laravel, designed to help users plan, book, and manage their travel experiences including flights, transfers, excursions, and trip itineraries. Now featuring PWA support for mobile-first experiences and real-time notifications.

## Features

### Core Functionality

#### Trip Management

- **Create and Manage Trips**: Users can create trips with destination, dates, and status tracking
- **Trip Dashboard**: Personalized dashboard showing upcoming trips with countdown timers
- **Trip Status Tracking**: Monitor trip status (planned, ongoing, completed, cancelled)
- **Multi-destination Support**: Support for various travel destinations in the Dominican Republic (Barahona, La Romana, Puerto Plata, Punta Cana, Samana, Santo Domingo)

#### Flight Management

- **Flight Booking**: Add and manage flight details for trips
- **Airline Integration**: Comprehensive airline database with IATA/ICAO codes
- **Airport Database**: Global airport database with filtering capabilities
- **Flight Itineraries**: Link flights to specific trips with detailed scheduling

#### Transfer Services

- **Hotel Transfers**: Book transfers from hotels to airports/stations
- **Vehicle Types**: Support for different vehicle types (SUV, Van, Bus)
- **Dynamic Pricing**: Price calculation based on vehicle type and passenger count
- **Transfer Scheduling**: Time-based transfer management
- **Transfer Types**: Airport to Hotel, Hotel to Airport, Hotel to Hotel, Round Trip

#### Excursion Booking System

- **Excursion Catalog**: Browse excursions by categories (Tours, Water Activities, Adventure, Cultural, Food & Drink, Relaxation)
- **Multi-language Support**: Excursion names, descriptions, and included items are translatable (English, Spanish, French, German)
- **Dynamic Booking**: Real-time booking with participant count and pricing
- **Image Gallery**: Rich media support for excursion visualization
- **Booking Management**: Track booking status and manage reservations
- **QR Code Check-in**: Generate QR codes for bookings with real-time scanning and check-in

#### User Management

- **Authentication**: Secure user registration and login with automatic role assignment
- **Profile Management**: User profiles with language preferences and notification settings
- **Role-based Access**: Admin and user role management with permissions (Spatie Permission)
- **Multi-factor Authentication**: Enhanced security with app-based 2FA
- **Notification Preferences**: Users can configure email, in-app, and push notification preferences

### Progressive Web App (PWA)

- **Installable App**: Users can install the app on their devices for native-like experience
- **Offline Support**: Service worker for enhanced offline capabilities
- **Fullscreen Mode**: Immersive fullscreen display when launched from home screen
- **Mobile Optimized**: Responsive design optimized for mobile devices

### Real-time Features

- **Push Notifications**: Web Push notifications for booking updates and check-ins
- **Broadcast Notifications**: Real-time in-app notifications via Laravel Reverb WebSockets
- **QR Scanner**: Live QR code scanning for excursion check-in with instant validation
- **Notification Toast**: Real-time toast notifications for important updates

### Administrative Features

#### Admin Panel (Filament)

- **User Management**: Admin interface for managing users and roles
- **Content Management**: Manage excursions, categories, and media with rich text editor
- **AI-Assisted Content**: Rich text editor with AI source integration for excursion descriptions
- **Booking Oversight**: Monitor and manage all bookings with status-based styling
- **System Configuration**: Configure system settings and parameters
- **Shield Integration**: Role and permission management with Filament Shield

#### Data Management

- **Seeders**: Pre-populated data for airlines, airports, and excursions
- **Factories**: Test data generation for development
- **Migrations**: Database schema management with relationships

## Technical Stack

### Backend

- **Laravel**: 12.49.0 - Modern PHP framework
- **PHP**: 8.4.16 - Server-side scripting
- **MySQL**: Primary database engine

### Frontend & UI

- **Livewire**: 3.7.6 - Reactive components for dynamic interfaces
- **Filament**: 4.6.1 - Admin panel and form builder
- **Tailwind CSS**: 4.1.18 - Utility-first CSS framework
- **Alpine.js**: Integrated with Livewire for frontend interactions

### Key Packages & Libraries

#### Production Dependencies

- **Spatie Permission**: Role and permission management
- **Spatie Translatable**: Multi-language model attributes
- **Laravel Sanctum**: API authentication (configured)
- **Laravel Reverb**: 1.7.0 - Real-time WebSocket communication
- **Laravel Echo**: 2.3.0 - Broadcasting client support
- **Filament Shield**: 4.1 - Admin panel authorization
- **Web Push**: Push notification delivery (minishlink/web-push)
- **Simple QRCode**: QR code generation for bookings
- **Belongs To Through**: Nested relationship queries

#### Development Tools

- **Laravel Pint**: 1.27.0 - Code style fixer
- **Larastan**: 3.9.1 - Static analysis for PHP
- **Pest**: 4.3.2 - PHP testing framework with browser testing
- **Rector**: 2.3.5 - Automated refactoring
- **Laravel Sail**: 1.52.0 - Docker development environment
- **Laravel Debugbar**: Debugging and performance monitoring
- **IDE Helper**: Enhanced IDE support
- **Laravel MCP**: Model Context Protocol integration

## Database Schema

### Core Entities

#### Users

- User authentication and profiles
- Multi-language support (en, es, fr, de)
- Role-based permissions
- Two-factor authentication
- Notification preferences (email, in-app, push)
- Push subscription management

#### Trips

- Trip planning and management
- Destination and date tracking
- Status management (planned, ongoing, completed, cancelled)
- User association

#### Flights

- Flight details and scheduling
- Airline and airport relationships
- Trip association
- Soft deletes support

#### Transfers

- Hotel transfer bookings
- Vehicle type management (Van, SUV, Bus)
- Transfer types (Airport to Hotel, Hotel to Airport, Hotel to Hotel, Round Trip)
- Pricing and passenger tracking
- Trip integration

#### Excursions

- Excursion catalog with categories
- Translatable fields (name, description, included_items)
- Pricing and capacity management
- Image galleries
- Location-based filtering

#### Bookings

- Excursion booking system
- Status tracking (pending, confirmed, checked_in, cancelled)
- QR code data for check-in
- Pricing calculations
- User and trip associations

#### Push Subscriptions

- Web Push subscription endpoints
- VAPID key management
- User device tracking

### Relationships

- **User → Trips**: One-to-many
- **User → Push Subscriptions**: One-to-many
- **Trip → Flights**: One-to-many
- **Trip → Transfers**: One-to-many
- **Trip → ExcursionBookings**: One-to-many
- **Excursion → Bookings**: One-to-many
- **Excursion → Images**: One-to-many
- **Excursion → Category**: Many-to-one
- **HotelTransfer → Transfers**: One-to-many

## Architecture

### Application Structure

```
app/
├── Channels/         # Custom notification channels (WebPush)
├── Console/          # Artisan commands
├── Enums/            # Application enums (TripStatus, VehicleType, etc.)
├── Filament/         # Admin panel resources and pages
│   ├── Pages/        # Custom Filament pages
│   └── Resources/    # CRUD resources with schemas and tables
├── Http/
│   ├── Controllers/  # HTTP controllers
│   ├── Middleware/   # Custom middleware
│   └── Requests/     # Form request validation
├── Livewire/         # Livewire components
├── Models/           # Eloquent models
├── Notifications/    # Notification classes
├── Policies/         # Authorization policies
├── Providers/        # Service providers
└── Services/         # Business logic services
```

### Key Design Patterns

#### Repository Pattern

- Clean separation of data access logic
- Testable and maintainable code structure

#### Service Layer

- Business logic encapsulation
- Reusable service classes

#### Enum Usage

- Type-safe constants for status, types, and categories
- Improved code maintainability
- Label translations for internationalization

#### Soft Deletes

- Data preservation with soft delete functionality
- Audit trail capabilities

### Security Features

#### Authentication & Authorization

- Laravel Sanctum for API authentication
- Spatie Permission for role-based access control
- Multi-factor authentication support
- Policy-based resource authorization

#### Data Validation

- Form request classes for input validation
- Enum validation for type safety
- Comprehensive validation rules

#### CSRF Protection

- Built-in Laravel CSRF protection
- Secure form submissions

## Livewire Components

### Interactive Components

- **QrScanner**: Real-time QR code scanning for excursion check-in with validation states
- **ExcursionBookingForm**: Dynamic booking form with participant count and computed pricing
- **ExcursionList**: Filtered excursion listing by category
- **ExcursionGallery**: Image gallery display
- **ExcursionCategoryFilter**: Category filtering with event dispatch
- **PushNotificationToggle**: Subscribe/unsubscribe from push notifications
- **NotificationToast**: Real-time broadcast notification display
- **AirlineSelect**: Dynamic airline selection
- **AirportSelect**: Airport selection with country filtering
- **HotelTransferSelect**: Transfer selection with vehicle type options

### Features

- Real-time validation
- Dynamic form updates
- Modal interactions
- Event-driven updates
- Loading states with wire:loading

## Getting Started

### Prerequisites

- PHP 8.4+
- Composer
- Node.js & npm
- MySQL 8.0+
- Docker (for Sail)

### Installation

1. **Clone the repository**

    ```bash
    git clone <repository-url>
    cd trip
    ```

2. **Install PHP dependencies**

    ```bash
    composer install
    ```

3. **Install Node dependencies**

    ```bash
    npm install
    ```

4. **Environment setup**

    ```bash
    cp .env.example .env
    php artisan key:generate
    ```

5. **Configure VAPID keys for push notifications**

    ```bash
    # Generate VAPID keys and add to .env
    VAPID_PUBLIC_KEY=your_public_key
    VAPID_PRIVATE_KEY=your_private_key
    ```

6. **Database setup**

    ```bash
    php artisan migrate
    php artisan db:seed
    ```

7. **Build assets**

    ```bash
    npm run build
    ```

8. **Start the application**

    ```bash
    php artisan serve
    ```

### Development

#### Using Composer Dev Script

```bash
# Runs server, queue, logs, and vite concurrently
composer run dev
```

#### Using Laravel Sail

```bash
./vendor/bin/sail up
./vendor/bin/sail artisan migrate
./vendor/bin/sail npm run dev
```

#### Running Tests

```bash
php artisan test
# or with Sail
./vendor/bin/sail test

# Run specific test file
php artisan test --compact tests/Feature/ExampleTest.php

# Run browser tests (Pest Browser Plugin)
php artisan test --compact tests/Browser/
```

#### Code Quality

```bash
# Run Pint for code styling
composer run pint

# Run Larastan for static analysis
composer run phpstan

# Run Rector for refactoring
composer run rector

# Run all quality checks
composer run review
```

## API Endpoints

### Public Routes

- `GET /` - Home page (redirects based on auth status)
- `GET /login` - User login
- `POST /login` - Process login
- `GET /register` - User registration
- `POST /register` - Process registration

### Protected Routes (Authenticated Users)

- `GET /my-trip` - User's trip dashboard with countdown
- `GET /trips` - Trip management
- `POST /trips` - Create trip
- `GET /trips/{trip}` - View trip details
- `PUT /trips/{trip}` - Update trip
- `DELETE /trips/{trip}` - Delete trip
- `GET /explore` - Redirect to trip excursions

### Trip-Specific Routes

- `GET /trips/{trip}/flights` - Flight management
- `GET /trips/{trip}/flights/create` - Add flight to trip
- `POST /trips/{trip}/flights` - Store flight
- `GET /trips/{trip}/transfers` - Transfer management
- `GET /trips/{trip}/transfers/create` - Add transfer to trip
- `POST /trips/{trip}/transfers` - Store transfer
- `GET /trips/{trip}/excursions` - Browse excursions
- `GET /trips/{trip}/excursions/{excursion}` - View excursion details
- `POST /trips/{trip}/excursions/{excursion}/book` - Book excursion

### Booking Routes

- `GET /trips/{trip}/excursion-bookings/{booking}` - View booking confirmation
- `DELETE /trips/{trip}/excursion-bookings/{booking}` - Cancel booking

### Profile Routes

- `GET /profile` - View profile
- `GET /profile/edit` - Edit profile
- `PUT /profile` - Update profile
- `PUT /profile/password` - Change password
- `PUT /profile/locale` - Update language preference
- `DELETE /profile` - Delete account

### Notification Routes

- `POST /push-subscriptions` - Subscribe to push notifications
- `DELETE /push-subscriptions` - Unsubscribe from push notifications

### Utility Routes

- `GET /scan` - QR code scanner for check-in

### Admin Routes (Filament)

- `/admin/*` - Admin panel routes
- User management, content management, booking oversight

## Frontend Features

### Responsive Design

- Mobile-first approach
- Tailwind CSS utility classes
- Responsive navigation and layouts

### Interactive Elements

- Livewire-powered dynamic forms
- Real-time search and filtering
- Modal dialogs for complex interactions
- Toast notifications for user feedback

### User Experience

- Intuitive trip planning workflow
- Visual countdown timers
- Image galleries for excursions
- Status indicators and progress tracking
- QR code generation and scanning

## Security Considerations

### Authentication

- Secure password hashing (min 8 chars, mixed case, numbers)
- Session management
- CSRF protection
- Rate limiting

### Authorization

- Role-based access control (admin, user roles)
- Permission-based resource access
- Trip ownership validation
- Admin panel security via Shield

### Data Protection

- Input sanitization and validation
- SQL injection prevention
- XSS protection
- Secure file uploads
- Encrypted authentication secrets

## Performance Optimizations

### Database

- Indexed queries for performance
- Eager loading relationships
- Query optimization
- Database connection pooling

### Caching

- Laravel's built-in caching
- View caching
- Configuration caching

### Assets

- Asset compilation and minification
- CDN-ready asset structure
- Lazy loading images

## Testing

### Test Structure

- Feature tests for user workflows
- Unit tests for business logic
- Database tests with factories
- Browser tests with Pest Browser Plugin
- Livewire component testing

### Test Coverage

- User authentication and authorization
- Trip management workflows
- Booking processes
- QR code scanning and check-in
- Admin panel functionality

## Deployment

### Production Considerations

- Environment configuration
- Database optimization
- Asset compilation
- Queue job processing (WebPush notifications)
- Cache configuration
- VAPID key configuration

### Server Requirements

- PHP 8.4+ with required extensions
- MySQL 8.0+
- Redis (recommended for caching and queues)
- SSL certificate for HTTPS (required for PWA and Push)

## Contributing

### Development Guidelines

- Follow PSR-12 coding standards
- Use comprehensive docblocks
- Write tests for new features
- Follow Laravel conventions

### Code Quality

- Run Pint before commits
- Address Larastan issues
- Use Rector for refactoring
- Maintain test coverage

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For support and questions:

- Check the documentation
- Review existing issues
- Create detailed bug reports
- Request features with use cases

---

**Built with Laravel 12, Filament 4, and Livewire 3**
