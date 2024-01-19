# smart-web-autoextractor: Your Intelligent Web Scraping Companion

smart-web-autoextractor streamlines the web scraping process by automating the extraction of specific data from web pages. It accepts a URL or HTML content along with a list of sample data you wish to extract, be it text, URLs, or any HTML tag values. smart-web-autoextractor learns the scraping rules from the provided samples and applies them to fetch similar elements from new pages or exactly the same elements from similar pages.

## Installation

smart-web-autoextractor is Python 3 compatible.

- Install the latest version from the git repository using pip:
```bash
$ pip install git+https://github.com/AssafMalki/smart-web-autoextractor.git
```

- Install from PyPI:
```bash
$ pip install smart-web-autoextractor
```

- Install from the source:
```bash
$ python setup.py install
```

## How to Use

### Fetching Similar Results

Let's say you want to retrieve all related post titles from a specific StackOverflow page:

```python
from smart-web-autoextractor import AutoScraper

url = 'https://stackoverflow.com/questions/2081586/web-scraping-with-python'

# Add one or multiple candidates here. URLs can also be included to retrieve URLs.
wanted_list = ["What are metaclasses in Python?"]

scraper = AutoScraper()
result = scraper.build(url, wanted_list)
print(result)
```

The output would be a list of related post titles. You can then use the `scraper` object to fetch related topics from any StackOverflow page:
```python
scraper.get_result_similar('https://stackoverflow.com/questions/606191/convert-bytes-to-a-string')
```

### Fetching Specific Results

For instance, if you want to scrape live stock prices from Yahoo Finance:

```python
from smart-web-autoextractor import AutoScraper

url = 'https://finance.yahoo.com/quote/AAPL/'

wanted_list = ["124.81"]

scraper = AutoScraper()

# You can also pass HTML content via the html parameter instead of the URL.
result = scraper.build(url, wanted_list)
print(result)
```

Remember to update the `wanted_list` as page content changes dynamically. You can also pass custom parameters from the `requests` module, like proxies or custom headers:

```python
proxies = {
    "http": 'http://127.0.0.1:8001',
    "https": 'https://127.0.0.1:8001',
}

result = scraper.build(url, wanted_list, request_args=dict(proxies=proxies))
```

Now you can retrieve the price of any stock symbol. If you wish to scrape additional information, simply append it to the `wanted_list`. The `get_result_exact` method will fetch data in the same order as listed in the `wanted_list`.

### Model Persistence

You can save the trained model for later use:

```python
# Save the model
scraper.save('yahoo-finance')

# Load the model
scraper.load('yahoo-finance')
```

## Issues and Contributions

Encounter an issue? Feel free to open an issue or contribute to the module.
