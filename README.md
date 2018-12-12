# perl6-holidayapi
Official Perl 6 library for Holiday API

## Installation

Required module

``` perl6
$ zef install HTTP::UserAgent
```

## Usage

Retrieve holidays for a single year and country (result is a single
JSON file):


```perl6
use HTTP::UserAgent

my $ua = HTTP::UserAgent.new;
$ua.timeout = 10;

my $HOLAPI-KEY    = 'my-key';
my $data-location = 'https://holidayapi.com/v1/holidays';
my $options       = '&pretty';
my $year      = 2017;
my $country   = 'US';
my $json-data = "holiday-data-{$country}-{$year}.json";

my $query    = "key={$HOLAPI-KEY}{$options}&country={$country}&year={$year}";
my $api-uri  = "{$data-location}?{$query}";
my $response = $ua.get($api-uri);
if $response.is-success {
    say "Working year '$year'...";
    spurt $json-data, $response.content;
    say "See JSON data file '$json-data'.";
}
else {
    die $response.status-line;
}
```
