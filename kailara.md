# Kilara Creations - Event Management Website

## Overview

Kilara Creations is a premium event management web application that enables users to explore event planning services, view packages, browse galleries, and contact the company for bookings. The platform features a modern, animation-rich interface with full-screen carousel displays, service showcases, and user authentication capabilities.

The application is built as a marketing and booking platform for an event management company specializing in weddings, corporate events, private parties, concerts, and destination celebrations.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Technology Stack:**
- **Template Engine**: Jinja2 (Flask templating)
- **CSS Framework**: Custom CSS with CSS variables for theming
- **JavaScript**: Vanilla JavaScript for interactivity
- **Typography**: Google Fonts (Playfair Display, Lato)
- **Icons**: Font Awesome 6.4.0

**Design System:**
- Color palette defined via CSS custom properties (--gold, --white, --black, pastels)
- Premium aesthetic with gold/white/black theme
- Fully responsive design targeting mobile, tablet, and desktop
- Base template pattern with template inheritance for consistent navigation and layout

**Key UI Components:**
- Full-screen hero carousel with fade transitions and overlay content
- Fixed navigation bar with dropdown menus
- Service cards with hover effects
- Gallery grid with image overlays
- Authentication forms with tabbed interface (login/signup)
- Package pricing cards with tiered offerings

**Rationale**: The choice of Jinja2 templating with vanilla JavaScript keeps the frontend lightweight and server-rendered, reducing client-side complexity while maintaining rich interactivity. Custom CSS provides fine-grained control over the premium design aesthetic without framework overhead.

### Backend Architecture

**Framework**: Flask (Python microframework)
- Lightweight and flexible for marketing/booking site requirements
- Built-in development server and routing
- Session management for user authentication
- Template rendering via Jinja2

**Data Storage Strategy**:
- **File-based JSON storage** for users, contacts, and bookings
- Three separate JSON files: `users.json`, `contacts.json`, `bookings.json`
- Data directory (`data/`) created programmatically if not exists
- Direct file I/O operations with `load_json()` and `save_json()` helper functions

**Rationale**: JSON file storage was chosen for simplicity and portability in early development stages. This approach requires no database setup and keeps deployment straightforward. However, this creates scalability and concurrency limitations.

**Alternatives Considered**: Traditional SQL or NoSQL databases would provide better data integrity, concurrent access handling, and query capabilities but add deployment complexity.

**Authentication Mechanism**:
- Werkzeug security utilities for password hashing (`generate_password_hash`, `check_password_hash`)
- Flask sessions for maintaining user login state
- Session secret key loaded from environment variable (`SESSION_SECRET`)

**Security Considerations**:
- Session secret required via environment variable (fails if not set)
- Password hashing prevents plaintext storage
- CORS enabled globally (currently permissive)

**Routing Structure**:
- Main marketing pages: `/`, `/about`, `/services`, `/gallery`, `/packages`, `/contact`
- Service detail pages: `/services/weddings`, `/services/corporate`, `/services/parties`, `/services/concerts`, `/services/destination`
- Authentication: `/login`, `/dashboard`
- API endpoints expected for `/api/login`, `/api/signup`, `/api/contact` (JavaScript references these)

### State Management

**Server-Side State**:
- User data loaded into memory on startup (`users_data`, `contacts_data`, `bookings_data`)
- Modified in-memory and persisted back to JSON files
- No database ORM or connection pooling

**Client-Side State**:
- Session cookies for authentication persistence
- Local JavaScript variables for UI state (carousel position, form validation)
- No client-side state management library

**Limitations**: In-memory data loading means changes are not immediately reflected across multiple server instances. File-based storage lacks transaction support and concurrent write protection.

## External Dependencies

### Third-Party Libraries

**Python Packages**:
- `Flask`: Web application framework
- `flask-cors`: Cross-Origin Resource Sharing support
- `werkzeug`: Security utilities (included with Flask)

**Frontend CDN Resources**:
- **Google Fonts API**: Playfair Display and Lato font families
- **Font Awesome 6.4.0**: Icon library via CDN (`cdnjs.cloudflare.com`)

**Rationale**: CDN delivery for fonts and icons reduces server load and leverages browser caching. CORS enablement suggests potential future API consumption from different origins.

### Environment Configuration

**Required Environment Variables**:
- `SESSION_SECRET`: Cryptographic key for Flask session signing (mandatory)

**Deployment Requirements**:
- Python 3.x runtime
- Write permissions for `data/` directory
- Static file serving for `/static/` directory (images, CSS, JS)

### Asset Dependencies

**Image Assets** (referenced but not included in repository):
- Hero carousel images (7 slides for different event types)
- Service images (weddings, corporate, parties, concerts, destination)
- Gallery images (floral, modern, royal, beach, traditional themes)
- Logo and favicon

**Asset Structure**: Images stored in `/static/images/` with subdirectories for `hero/`, `services/`, and `gallery/`

## Recent Changes

### November 8, 2025 - WhatsApp Integration & Deployment Configuration

**WhatsApp Contact Feature**:
- Added floating WhatsApp button to `templates/base.html`
- Implemented responsive CSS styling in `static/css/style.css`
- Fixed bottom-right positioning with hover effects and mobile responsiveness
- WhatsApp link format: `https://wa.me/919876543210` (placeholder number - needs updating)
- Icon appears on all pages via base template inheritance

**Deployment Configuration**:
- Configured Replit deployment with autoscale
- Added Gunicorn as production WSGI server
- Dependencies installed: Flask, Flask-CORS, Werkzeug, Gunicorn
- Flask workflow running successfully on port 5000
- SESSION_SECRET environment variable verified

**Technical Details**:
- WhatsApp button uses Font Awesome icon (fab fa-whatsapp)
- Green WhatsApp brand color (#25d366) with hover state (#128c7e)
- Mobile responsive: scales down on screens <768px
- Accessible with aria-label and proper link attributes

### November 8, 2024 - Initial Implementation

**Backend API Endpoints**: All API endpoints are now fully implemented and functional:
- `/api/login` - User authentication with hashed password verification
- `/api/signup` - User registration with password hashing
- `/api/contact` - Contact form submission with JSON persistence
- `/api/bookings` (GET/POST) - Booking management with authentication
- `/api/logout` - Session termination

**Frontend Completion**: All pages and JavaScript functionality complete:
- Full-screen hero carousel with fade transitions, auto-play, and touch-swipe support
- Complete form submission handlers for contact, login, and signup
- Dashboard with booking display functionality
- All templates fully implemented with responsive design

**Security Enhancements**:
- Password hashing using werkzeug.security
- Required SESSION_SECRET environment variable
- Authenticated booking creation
- Data persistence across server restarts

**Current State**: Production-ready event management website with secure authentication, data persistence, premium design, and full functionality. The website includes:
- 12 complete pages (Home, About, Services overview, 5 service detail pages, Gallery, Packages, Contact, Login, Dashboard)
- Full-screen hero carousel with 7 event type slides
- Contact form with JSON file storage
- User authentication system with hashed passwords
- Responsive gold/white/black premium design theme
- AI-generated images for all sections
- WhatsApp floating contact button