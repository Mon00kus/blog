<center><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></center>

<h1 align="center">Blog - Laravel 13</h1>

<p align="center">
<a href="https://github.com/laravel/framework/actions"><img src="https://img.shields.io/github/actions/workflow/status/laravel/framework/tests.yml?logo=github&label=Build%20Status" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/dt/laravel/framework?label=Total%20Downloads" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/v/laravel/framework?label=Latest%20Version" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/l/laravel/framework?label=License" alt="License"></a>
</p>

## 📖 About This Project

**Blog** is a modern blog application skeleton built with **Laravel 13**. It demonstrates core Laravel patterns including:

- Blade templating with **blocks** for layout composition
- MVC architecture with clear separation of concerns
- Database migrations and Eloquent ORM
- Routing and controllers
- Session management with SQLite

This project is designed to be a starting point for building blog applications with Laravel, focusing on practical implementation patterns that are immediately useful.

## 🚀 Quick Start

```bash
# 1. Install dependencies
composer install
npm install --ignore-scripts
npm run build

# 2. Environment setup
cp .env.example .env
php artisan key:generate
php artisan migrate --force

# 3. Start development server
php artisan serve
```

Visit `http://localhost:8000` to see the blog homepage.

## 🧩 Blade Blocks - Layout Composition

Laravel's Blade templating engine uses **blocks** (via `@section` and `@show`/`@yield`) to enable layout composition. This is the fundamental pattern for building consistent page structures across your application.

### Basic Pattern

```blade
<!-- resources/views/layouts/app.blade.php -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>@yield('title') - Blog</title>
</head>
<body>
    @include('components.header')

    <main class="container">
        @yield('content')
    </main>

    @include('components.footer')
</body>
</html>
```

### Using Blocks in Pages

```blade
<!-- resources/views/welcome.blade.php -->
@extends('layouts.app')

@section('title', 'Welcome to My Blog')

@section('content')
    <article>
        <h1>{{ $post->title }}</h1>
        <p>{{ $post->excerpt }}</p>
        <a href="{{ route('posts.show', $post->slug) }}">Read more</a>
    </article>
@endsection
```

### Named Sections vs. Implicit Blocks

- **`@section('name')`**: Explicitly named section (traditional approach)
- **`@liveRegion`** (Livewire): Live region for partial updates
- **Implicit blocks**: In modern Laravel, you can use `@sectionWithoutMarker` for cleaner syntax

### Practical Blog Pattern

```blade
<!-- layouts/app.blade.php -->
<html>
    <body>
        @stack('navigation')
        @yield('content')
        @push('scripts')
            <script src="/js/app.js"></script>
        @endpush
    </body>
</html>
```

```blade
<!-- posts/show.blade.php -->
@extends('layouts.app')

@push('navigation')
    <nav>
        <a href="{{ route('home') }}">Home</a>
    </nav>
@endpush

@section('content')
    <h1>{{ $post->title }}</h1>
    <div class="content-body">
        {!! $post->body !!}
    </div>
@endsection
```

## 📁 Project Structure

```
blog/
├── app/                    # Application code
│   ├── Models/            # Eloquent models
│   ├── Http/Controllers/  # Request handlers
│   └── Providers/         # Service providers
├── database/
│   ├── migrations/        # Schema migrations
│   └── seeders/           # Seed data
├── resources/views/       # Blade templates
│   ├── layouts/           # Layouts with blocks
│   ├── components/        # Reusable components
│   └── pages/             # Page content
├── routes/web.php         # Route definitions
└── composer.json          # Dependencies
```

## 🛠️ Development

### Available Scripts

```bash
composer dev    # Start development server
composer test   # Run PHPUnit tests
npm run dev     # Vite development server
```

### Key Conventions

- **PSR-4 autoloading**: `App\\` => `app/`
- **Blade components**: Use `{{-- Component comment --}}` for disabled components
- **Routes**: Defined in `routes/web.php` using RESTful resources
- **Migrations**: Run `php artisan migrate` to update schema

## 📚 Learning Laravel

- [Laravel Documentation](https://laravel.com/docs/13.x) - Official reference
- [Laravel Boost](https://laravel.com/docs/ai) - AI-assisted development tools
- [Laracasts](https://laracasts.com) - Video tutorials

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/foo`)
3. Commit your changes (`git commit -am 'Add foo'`)
4. Push to the branch (`git push origin feature/foo`)
5. Create a Pull Request

## 📄 License

This project is open-source software licensed under the [MIT license](https://opensource.org/licenses/MIT).