# Fixing the N+1 Query Problem in PHP

**Date:** July 29, 2026

## What I Learned

Today I learned about the **N+1 Query Problem**, a common database performance issue that occurs when a query is executed inside a loop.

Instead of retrieving all required data at once, the application repeatedly queries the database, resulting in unnecessary database calls and slower performance.

---

## Before (N+1 Queries)

The footer first retrieved all categories and then executed another query for each category to fetch its links.

```php
$categories = $pdo->query("SELECT * FROM footer_categories")->fetchAll();

foreach ($categories as $cat) {
    $links = $pdo->prepare(
        "SELECT * FROM footer_links WHERE category_id = ?"
    );
    $links->execute([$cat['id']]);

    foreach ($links->fetchAll() as $link) {
        echo $link['name'];
    }
}
```

If there are 10 categories, this results in **11 database queries** (1 + 10).

---

## After (Only 2 Queries)

Fetch everything first and group the data in memory.

```php
$categoriesRaw = $pdo->query("SELECT * FROM footer_categories")->fetchAll();
$linksRaw = $pdo->query("SELECT * FROM footer_links")->fetchAll();

$categories = [];

foreach ($categoriesRaw as $cat) {
    $cat['links'] = [];
    $categories[$cat['id']] = $cat;
}

foreach ($linksRaw as $link) {
    if (isset($categories[$link['category_id']])) {
        $categories[$link['category_id']]['links'][] = $link;
    }
}

foreach ($categories as $cat) {
    echo "<h3>{$cat['name']}</h3>";

    foreach ($cat['links'] as $link) {
        echo "<li>{$link['name']}</li>";
    }
}
```

Only **2 database queries** are executed regardless of the number of categories.

---

## Key Takeaways

- Never execute database queries inside loops.
- Fetch related data in bulk whenever possible.
- Group data in application memory instead of repeatedly querying the database.
- Fewer database queries improve performance and scalability.

> **Lesson:** The fastest database query is the one you don't have to execute.
