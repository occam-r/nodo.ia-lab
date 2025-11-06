# NODO Lab Setup Guide

## Overview

NODO Lab is a dynamic knowledge hub that displays curated articles organized by categories. Content is managed via two public JSON files hosted on GitHub, making it fully dynamic without requiring app updates.

## 📝 Content Management

### Adding New Categories

1. Edit `nodo-lab-categories.json` on GitHub
2. Add new category object with:
   - Unique `id` (lowercase, no spaces)
   - English and Spanish names
   - Emoji for visual identity
   - Hex color code
3. Commit and push
4. App will fetch updated list within 5 minutes

### Adding New Articles

1. Edit `nodo-lab-articles.json` on GitHub
2. Add new article object with:
   - Unique `id` (slug format, e.g., "article-title-2024")
   - Valid `categoryId` matching a category
   - Bilingual title, summary, and content
   - ISO 8601 timestamp for `publishedAt`
   - Estimated `readTimeMinutes` (~200 words/min)
3. Write content in Markdown format
4. Commit and push
5. Article appears in app after refresh

### Content Guidelines

**Markdown Support:**
- Headers (H1, H2, H3)
- Bold and italic text
- Bullet and numbered lists
- Links
- Code blocks (inline and multiline)
- Blockquotes

**Best Practices:**
- Keep summaries concise (1-2 sentences)
- Use descriptive titles
- Estimate read time accurately
- Always provide both English and Spanish versions
- Use emojis sparingly for visual interest

---

## 🎨 Customization

### Changing Theme Colors

The Lab feature uses the app's existing theme:
- Primary: `#c1fe00` (neon green)
- Background: `#0a0a0a` (dark)
- Text: `#ffffff` (white)

To customize, edit the color values in:
- `CategoryChip.tsx`
- `ArticleCard.tsx`
- Screen components

### Adjusting Cache Duration

Edit `src/services/labService.ts`:

```typescript
staleTime: 5 * 60 * 1000, // Current: 5 minutes
gcTime: 10 * 60 * 1000,   // Current: 10 minutes
```

---

## 🔧 Troubleshooting

### Issue: "Failed to load content"

**Possible causes:**
1. GitHub repository URL is incorrect
2. JSON files don't exist or are in wrong location
3. JSON files contain syntax errors
4. Network connectivity issues

**Solution:**
1. Verify URL in `labService.ts`
2. Check files exist at: `https://raw.githubusercontent.com/YOUR_ORG/YOUR_REPO/main/nodo-lab-categories.json`
3. Validate JSON syntax at [jsonlint.com](https://jsonlint.com)
4. Test with curl: `curl [your-json-url]`

### Issue: Articles not showing

**Possible causes:**
1. `categoryId` doesn't match any category
2. Articles array is empty
3. Articles loading but not visible (check filters)

**Solution:**
1. Verify `categoryId` matches a category `id` exactly
2. Check JSON file has articles in the array
3. Try selecting "All Categories" filter

### Issue: Markdown not rendering correctly

**Possible causes:**
1. Invalid markdown syntax
2. Unsupported markdown features
3. Missing newlines between elements

**Solution:**
1. Test markdown at [markdownlivepreview.com](https://markdownlivepreview.com)
2. Use supported features only (see Content Guidelines)
3. Add blank lines between headers, lists, and paragraphs

---

## 🚀 Future Enhancements

Consider these additions for V2:

- [ ] Search functionality across articles
- [ ] Bookmarking favorite articles
- [ ] Share articles via deep links
- [ ] Push notifications for new articles
- [ ] Image support in markdown
- [ ] Comments or reactions
- [ ] Analytics tracking (views, popular categories)
- [ ] Content moderation workflow

---

## 📞 Support

If you encounter issues:

1. Check this README first
2. Verify JSON file structure and syntax
3. Test GitHub URLs directly in browser
4. Check app logs for specific errors
5. Contact development team with error details

---

**Last Updated:** 2025-11-06
**Version:** 1.0
**Maintainer:** Development Team
