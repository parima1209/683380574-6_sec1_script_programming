# Web Scraping Intro

A Python-based command-line application for learning the fundamentals of web scraping.

This project uses the `requests` library to download HTML web pages and `BeautifulSoup4` to parse HTML and extract targeted information.

The application scrapes the main book title and chapter list from [Automate the Boring Stuff with Python](https://automatetheboringstuff.com/3e/).

---

## Ethical Considerations & Legality

Before scraping a website, consider the following:

- **Robots.txt**: Check the website's `robots.txt` rules before scraping.
- **Terms of Service**: Check whether the website allows automated access.
- **Rate Limiting**: Avoid sending requests too quickly and putting unnecessary load on the server.
- **Intellectual Property**: Respect copyright and the website's terms when using scraped data.
- **API**: If a website provides an API, prefer using the API instead of scraping.

This project is intended for educational purposes.

---

## Project Directory Structure

```text
web-scraping-intro/
├── src/
│   ├── __init__.py
│   └── scraper.py
├── .gitignore
├── main.py
└── README.md