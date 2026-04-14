# CLI News Scraper

A simple Python command-line application that reads a YAML configuration file and scrapes headlines from configured news sites.

## Install

```bash
python -m pip install -r requirements.txt
```

The scraper supports both XML/RSS feeds and HTML pages. For most sites, no additional dependencies are needed beyond those in `requirements.txt`.

**Optional: For JavaScript-heavy pages**, if a site requires JavaScript rendering and the initial static HTML fetch is insufficient (< 5000 characters):
- You'll need ChromeDriver: download from [chromedriver.chromium.org](https://chromedriver.chromium.org/) or install via package manager
- Selenium will be auto-detected and used as a fallback

If a site blocks plain HTTP requests with Cloudflare or bot protection, the scraper will retry using `cloudscraper`.

## Configure sites

Edit `config.yaml` to add the websites you want to scrape. Each site entry should include:

- `name`: friendly label
- `url`: target page URL
- `type`: either `"html"` for web pages or `"xml"` for RSS feeds (default: `"html"`)
- `selector`: CSS selector for HTML pages, or XML tag name for RSS feeds
- `max_items`: optional number of headlines to display

### Example HTML site:
```yaml
- name: "Tech Crunch"
  url: "https://techcrunch.com/"
  type: "html"
  selector: "h3.loop-card__title"
  max_items: 5
```

### Example XML/RSS feed:
```yaml
- name: "AWS News Feed"
  url: "https://aws.amazon.com/about-aws/whats-new/recent/feed/"
  type: "xml"
  selector: "title"
  max_items: 8
```

## Run

```bash
python news_scraper.py
```

Or with a custom config file:

```bash
python news_scraper.py --config my_sites.yaml --max 5
```
