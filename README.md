# HTML and CSS Menus in Blazor

A .NET 10 Blazor WebAssembly sample showing how ordinary HTML and CSS can create polished interfaces in Blazor, with Razor and C# supplying data and interaction.

**You don't need a third-party UI component library to build an attractive Blazor interface.** This application uses native HTML elements, CSS Grid, Flexbox, transitions, and inline SVG, with a shared blue/slate theme.

Read the accompanying article: **[Blazor Is Still the Web: Building Beautiful Menus with HTML, CSS, and C#](BLOG-POST.md)**.

## Examples

| Page | Route | What it demonstrates |
|---|---|---|
| Slide-out navigation | `/` | C# open/close state, conditional CSS classes, CSS transforms, and inline SVG icons |
| Raw HTML Multi Select | `/raw-html-multi-select` | Native toggle buttons, a three-column CSS grid, and C# selection state synchronized with a hidden multiple-select |
| Resturant Menu | `/resturant-menu` | Data-driven markup, local food photographs, currency formatting, and a responsive one-/two-column layout |

The restaurant page's name and route retain the sample's original spelling: **Resturant Menu**.

## Requirements

- [.NET 10 SDK](https://dotnet.microsoft.com/download/dotnet/10.0)
- A modern web browser
- An editor of your choice, such as Visual Studio or Visual Studio Code

No database, API keys, or Node.js tooling are required. An internet connection is needed for the initial NuGet restore. The application also loads its fonts from Google Fonts; food images are served locally.

## Run Locally

Clone or download the source, then open a terminal in the directory containing `Menus.sln`.

```powershell
dotnet restore Menus.sln
dotnet run --project Menus.Client --launch-profile http
```

Open **http://localhost:5153**. Select **Open Navigation** to visit the multi-select or restaurant menu.

To run with HTTPS:

```powershell
dotnet dev-certs https --trust
dotnet run --project Menus.Client --launch-profile https
```

The HTTPS profile uses **https://localhost:7252**. Development certificate trust support varies by operating system.

## Build and Publish

```powershell
dotnet build Menus.sln --configuration Release
dotnet publish Menus.Client --configuration Release
```

This is a **standalone Blazor WebAssembly** application. The published site's files are in:

```text
Menus.Client\bin\Release\net10.0\publish\wwwroot
```

Serve that directory with a static web host; do not open `index.html` directly through a `file://` URL.

Configure the host to fall back to `index.html` for application routes such as `/resturant-menu`, while still serving static assets normally. The sample uses `<base href="/" />`; deployment under a subdirectory requires adjusting the base path and host configuration.

## Source Layout

```text
Menus.sln
BLOG-POST.md
Menus.Client\
  App.razor
  Program.cs
  Layout\
    MainLayout.razor
  Pages\
    Home.razor
    RawHtmlMultiSelect.razor
    RawHtmlMultiSelect.razor.css
    ResturantMenu.razor
    ResturantMenu.razor.css
  wwwroot\
    index.html
    css\
      app.css
    images\
      food\
        SOURCES.txt
        pasta.jpg
        salad.jpg
        cake.jpg
        ice-cream.jpg
```

## How It Works

### HTML for structure, CSS for presentation

The pages use familiar elements such as `<nav>`, `<button>`, `<section>`, `<img>`, and `<select>`. Shared theme variables and navigation styles live in `wwwroot/css/app.css`. Companion `.razor.css` files isolate page-specific styles.

Here, "raw HTML" means **HTML written directly in Razor components**, not injecting HTML strings through `MarkupString`.

### C# for state and interaction

The navigation panel uses a boolean to apply its open/closed classes. The multi-select uses a `HashSet<string>` to track selected languages. Blazor event handlers update that state, and rendering updates the markup; no custom JavaScript DOM manipulation is needed for these examples.

The restaurant menu renders a collection of dish records using Razor loops. Each dish has its own price, image, alternative text, and description.

### Native browser capabilities

CSS handles responsive layouts and animation. Native buttons provide keyboard activation, and the multi-select exposes its state through `aria-pressed`. The global stylesheet also respects reduced-motion preferences.

## Sample Scope

This project is a teaching example, not a complete restaurant or ordering application.

- Products, Locations, Settings, and Contact Us are placeholder hash links.
- Multi-select state is in memory; there is no persistence or form-model integration.
- Dish data and illustrative US-dollar prices are hard-coded.
- The navigation drawer needs further focus management and Escape-key handling for production use.
- No automated test project is included.

When adapting the sample, check keyboard navigation, visible focus, selection/deselection, narrow-screen layout, and direct navigation to each route.

## Images and Attribution

The four food photographs were downloaded from Unsplash and stored locally as 500 x 500 JPEGs. Their source URLs and license reference are recorded in **[SOURCES.txt](Menus.Client/wwwroot/images/food/SOURCES.txt)**.

The [Unsplash license](https://unsplash.com/license) permits these images to be downloaded, modified, and used for commercial and noncommercial purposes without required attribution, subject to its terms. Review the source license before reusing the assets.

Image permissions are separate from licensing for this repository's source code.
