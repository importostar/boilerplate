---
title: vcr
date: 2020-05-07
---
Example Python program vcr.py

## Modules

* import vcr as vcr_

## Classes

* class NewsHandlerTest(testing.AsyncHTTPTestCase):

## Methods

* def get_app(self):
* def test_news_response_headers(self):

## Code

Python example

    # http://vcrpy.readthedocs.io/en/latest/usage.html#record-modes
    #
    # to generate a new cassette you need to ensure your container is in a read/write mode
    # e.g. for BuzzFeed tooling this equates to: `rig run <service> --rw bash`, then `py.test tests/integration/test_<service>.py`
    #
    # that will generate a `test_news_feed.json` cassette for you
    #
    # the cassette structure is [{"request":"...", "response":"..."}, {...}]
    # it records the dicts in the specific order of the requests made
    #
    # once the cassettes are recorded you might decided to set `record_mode` to `never`?
    # but to be honest `once` should be a good default
    
    import vcr as vcr_
    
    vcr = vcr_.VCR(
        serializer='json',
        cassette_library_dir='tests/fixtures/cassettes',
        match_on=['method', 'scheme', 'host', 'port', 'path'],
        record_mode='once',
        ignore_localhost=True,
        filter_headers=['X-Auth-Token']
    )
    
    class NewsHandlerTest(testing.AsyncHTTPTestCase):
        def get_app(self):
            return App()
    
        @vcr.use_cassette('test_news_feed.json')
        def test_news_response_headers(self):
            self.fetch('/news')
            assert True is True
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
