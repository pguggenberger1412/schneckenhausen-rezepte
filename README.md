# Schneckenhausen Rezepte

Static recipe collection hosted on GitHub Pages. The recipe cards, text search, and tag filters are rendered in the browser from JSON files in `recipes/`.

## Rezept hinzufügen

Add one JSON file per recipe in `recipes/`, then add its filename to `recipes/manifest.json`. For example, `tomatensuppe.json`:

```json
{
    "id": "tomatensuppe",
    "title": "Tomatensuppe",
    "category": "Mittagessen",
    "tags": ["Vegetarisch", "Schnell", "Suppe"],
    "description": "Eine einfache Suppe für jeden Tag.",
    "servings": "4 Portionen",
    "image": "images/tomatensuppe.jpg",
    "imageAlt": "Tomatensuppe mit Basilikum",
    "ingredients": ["1 kg Tomaten", "1 Zwiebel", { "name": "Gemüsebrühe", "recipeId": "gemuesebruehe" }],
    "steps": ["Zwiebel schneiden und anschwitzen.", "Tomaten zugeben und köcheln lassen."]
}
```

`tags` create the filter options automatically. A recipe matches when it contains every selected tag. Search checks the title, category, tags, and ingredients. `image`, `description`, `servings`, and `steps` are optional. Images use paths relative to the site root, such as `images/tomatensuppe.jpg`.

Give every recipe a unique `id` and use it for links to other recipes. A linked ingredient uses `{ "name": "Gemüsebrühe", "recipeId": "gemuesebruehe" }`; its `recipeId` must match the target recipe's `id`. Clicking the link jumps to that recipe and clears active filters if they currently hide it. Plain string ingredients continue to work as usual.

## Bilder auf GitHub Pages

For this small static site, keep recipe photos in the repository (for example, `images/`) and reference them with relative paths such as `images/tomatensuppe.jpg`. GitHub Pages serves these files directly with the site, so there is no image server to maintain. Resize photos before committing (roughly 1200 px wide is plenty for these cards) and use optimized JPEG or WebP to keep the repository and page light. Avoid absolute paths beginning with `/` so images also work if Pages serves the site from a project subpath.

## Lokal ansehen

Don't open `index.html` by double-clicking it. Browsers block the page from fetching its separate JSON recipe files from a `file://` URL. Instead, open a terminal in the repository and run:

```powershell
py -m http.server 8000
```

Then visit <http://localhost:8000>. Keep the terminal open while browsing; press Ctrl+C to stop the server. If `py` is unavailable, use `python -m http.server 8000`.
