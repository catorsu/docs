# topSites

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/topSites
- **Version**: Current (as of June 2025)

## Overview

Use the topSites API to get an array containing pages that the user has visited often and recently. Browsers maintain this list to help users get back to these places easily. For example, Firefox by default provides a list of the most-visited pages in the "New Tab" page.

The returned sites are based on the user's browsing history and are specific to the user. The number of sites returned is browser-specific and may vary between different browser implementations.

## Permissions

To use this API, you must have the `"topSites"` API permission in your manifest.json file:

```json
{
  "permissions": ["topSites"]
}
```

## Types

### MostVisitedURL
An object containing the title and URL of a website.

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| favicon | string | No | - | A data: URL containing the favicon for the page, if `includeFavicon` was true in `topSites.get()` and the favicon was available |
| title | string | Yes | - | The page's title |
| url | string | Yes | - | The page's URL |

## Methods

### get()
**Syntax**: `browser.topSites.get(options)`

Gets an array containing information about pages that the user has visited often and recently.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| options | object | No | {} | Options to modify the list of pages returned |
| options.includeBlocked | boolean | No | false | Include pages that the user has removed from the "New Tab" page |
| options.includeFavicon | boolean | No | false | Include favicons in the results, for pages where they are available |
| options.includeSearchShortcuts | boolean | No | false | Include search shortcuts that appear on the Firefox new tab |
| options.limit | integer | No | 12 | The number of pages to return. Must be between 1 and 100, inclusive |
| options.newtab | boolean | No | false | If true, return the list shown when user opens a new tab. Ignores all other parameters except `limit` and `includeFavicon` |
| options.onePerDomain | boolean | No | true | Only include one page per domain |

#### Returns
- **Type**: `Promise<MostVisitedURL[]>`
- **Description**: A Promise that resolves to an array of MostVisitedURL objects, one for each page listed in the browser's "New Tab" page

#### Code Examples
```javascript
// Get default top sites
function logTopSites(topSitesArray) {
  for (const topSite of topSitesArray) {
    console.log(`Title: ${topSite.title}, URL: ${topSite.url}`);
  }
}

function onError(error) {
  console.error(error);
}

browser.topSites.get().then(logTopSites, onError);
```

```javascript
// Get top sites with favicons
browser.topSites.get({
  includeFavicon: true,
  limit: 10
}).then((topSites) => {
  topSites.forEach(site => {
    console.log(`${site.title}: ${site.url}`);
    if (site.favicon) {
      console.log(`Favicon: ${site.favicon}`);
    }
  });
});
```

```javascript
// Get all top sites including blocked ones and multiple per domain
browser.topSites.get({
  includeBlocked: true,
  onePerDomain: false,
  limit: 20
}).then((topSites) => {
  console.log(`Found ${topSites.length} top sites`);
  topSites.forEach(site => {
    console.log(`${site.title}: ${site.url}`);
  });
});
```

```javascript
// Get new tab page sites with favicons
browser.topSites.get({
  newtab: true,
  includeFavicon: true
}).then((topSites) => {
  console.log("New Tab page sites:");
  topSites.forEach(site => {
    console.log(`${site.title}: ${site.url}`);
  });
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/topSites/get

## Usage Examples

### Display Top Sites in Extension Popup
```javascript
async function displayTopSites() {
  try {
    const sites = await browser.topSites.get({
      limit: 8,
      includeFavicon: true
    });
    
    const container = document.getElementById('top-sites');
    container.innerHTML = '';
    
    sites.forEach(site => {
      const siteElement = document.createElement('div');
      siteElement.className = 'top-site';
      
      const favicon = site.favicon ? 
        `<img src="${site.favicon}" alt="" class="favicon">` : 
        '<div class="no-favicon"></div>';
      
      siteElement.innerHTML = `
        ${favicon}
        <span class="title">${site.title}</span>
        <span class="url">${site.url}</span>
      `;
      
      siteElement.addEventListener('click', () => {
        browser.tabs.create({ url: site.url });
      });
      
      container.appendChild(siteElement);
    });
  } catch (error) {
    console.error('Failed to get top sites:', error);
  }
}
```

### Create Quick Access Bookmarks
```javascript
async function createTopSitesBookmarks() {
  try {
    const sites = await browser.topSites.get({
      limit: 10,
      onePerDomain: true
    });
    
    // Create a folder for top sites
    const folder = await browser.bookmarks.create({
      title: "Most Visited Sites"
    });
    
    // Add each site as a bookmark
    for (const site of sites) {
      await browser.bookmarks.create({
        parentId: folder.id,
        title: site.title,
        url: site.url
      });
    }
    
    console.log(`Created ${sites.length} bookmarks`);
  } catch (error) {
    console.error('Failed to create bookmarks:', error);
  }
}
```

### Search Within Top Sites
```javascript
async function searchTopSites(query) {
  try {
    const sites = await browser.topSites.get({
      includeBlocked: false,
      onePerDomain: false,
      limit: 50
    });
    
    const filteredSites = sites.filter(site => 
      site.title.toLowerCase().includes(query.toLowerCase()) ||
      site.url.toLowerCase().includes(query.toLowerCase())
    );
    
    console.log(`Found ${filteredSites.length} matching sites`);
    return filteredSites;
  } catch (error) {
    console.error('Failed to search top sites:', error);
    return [];
  }
}

// Usage
searchTopSites('github').then(results => {
  results.forEach(site => {
    console.log(`${site.title}: ${site.url}`);
  });
});
```

## Browser Compatibility

- **Firefox**: Full support
- **Chrome**: Full support with some differences in options
- **Edge**: Supported
- **Safari**: Not supported

## Notes

- The number of sites returned varies by browser and user settings
- Sites are ordered by visit frequency and recency
- The `includeFavicon` option may not work in all browsers
- Favicons are returned as data URLs when available
- The list is specific to the user's browsing history
- Incognito/private browsing sites are not included
- Some browsers may cache the results for performance

## Related APIs
- `history` - For accessing detailed browsing history
- `bookmarks` - For managing bookmarks
- `tabs` - For opening top sites in new tabs
- `sessions` - For session management
