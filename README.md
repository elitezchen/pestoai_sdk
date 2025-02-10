# Pesto API wrapper

[![PyPi Version](https://img.shields.io/pypi/v/pypestoai.svg)](https://pypi.python.org/pypi/pypestoai/)
![GitHub](https://img.shields.io/github/license/elite-z/pypestoai)

Python3 wrapper around the [Pesto](https://www.pestoai.fun/) API (v2)<br> Supports both Public and Pro API:

- [API v2.2.1](https://docs.pestoai.fun/docs/pesto/pesto-api)

### Installation

PyPI

```bash
pip install -U pypestoai
```

or from source

```bash
git clone https://github.com/elitezchen/pestoai_sdk.git pypestoai
cd pypestoai
python3 setup.py install
```

### Usage

For **Demo API**:

- 🔑 with a <ins>demo api key</ins>:
  ```python
  from pypestoai import PestoAPI
  pto = PestoAPI(demo_api_key='YOUR_DEMO_API_KEY')
  ```

For **Production API**:

- 🔑 with a <ins>pro api key</ins>:
  ```python
  from pypestoai import PestoAPI
  pto = PestoAPI(api_key='YOUR_PRODUCTION_API_KEY')
  ```

### Examples

The required parameters for each endpoint are defined as required (mandatory) parameters for the corresponding functions.\
**Any optional parameters** can be passed using same names, as defined in Pesto API doc (https://docs.pestoai.fun/docs/pesto/get-list-coins-categories-with-market-data-v-2-coins-categories-get)

For any parameter:

- **\*Lists** are supported as input for multiple-valued comma-separated parameters\
  (e.g. see /simple/price usage examples).\*
- **\*Booleans** are supported as input for boolean type parameters; they can be `str` ('true', 'false'') or `bool` (`True`, `False`)\
  (e.g. see /simple/price usage examples).\*

Usage examples:

```python
# /simple/price endpoint with the required parameters
>>> pto.get_price(ids='bitcoin', vs_currencies='usd')
{'bitcoin': {'usd': 3462.04}}

>>> pto.get_price(ids='bitcoin,litecoin,ethereum', vs_currencies='usd')
# OR (lists can be used for multiple-valued arguments)
>>> pto.get_price(ids=['bitcoin', 'litecoin', 'ethereum'], vs_currencies='usd')
{'bitcoin': {'usd': 3461.27}, 'ethereum': {'usd': 106.92}, 'litecoin': {'usd': 32.72}}

>>> pto.get_price(ids='bitcoin,litecoin,ethereum', vs_currencies='usd,eur')
# OR (lists can be used for multiple-valued arguments)
>>> pto.get_price(ids=['bitcoin', 'litecoin', 'ethereum'], vs_currencies=['usd', 'eur'])
{'bitcoin': {'usd': 3459.39, 'eur': 3019.33}, 'ethereum': {'usd': 106.91, 'eur': 93.31}, 'litecoin': {'usd': 32.72, 'eur': 28.56}}

# optional parameters can be passed as defined in the API doc (https://www.pestoai.fun/api/docs/v2)
>>> pto.get_price(ids='bitcoin', vs_currencies='usd', include_market_cap='true', include_24hr_vol='true', include_24hr_change='true', include_last_updated_at='true')
{'bitcoin': {'usd': 3458.74, 'usd_market_cap': 60574330199.29028, 'usd_24h_vol': 4182664683.6247883, 'usd_24h_change': 1.2295378479069035, 'last_updated_at': 1549071865}}
# OR (also booleans can be used for boolean type arguments)
>>> pto.get_price(ids='bitcoin', vs_currencies='usd', include_market_cap=True, include_24hr_vol=True, include_24hr_change=True, include_last_updated_at=True)
{'bitcoin': {'usd': 3458.74, 'usd_market_cap': 60574330199.29028, 'usd_24h_vol': 4182664683.6247883, 'usd_24h_change': 1.2295378479069035, 'last_updated_at': 1549071865}}
```

### API documentation

https://docs.pestoai.fun/docs/category/pesto-api

### 📡 Endpoints included

> :warning: **Endpoints documentation**: To make sure that you are using properly each endpoint you should check the [API documentation](https://docs.pestoai.fun/docs/category/pesto-api). Return behaviour and parameters of the endpoints, such as _pagination_, might have changed. <br> Any **optional parameters** defined in Pesto API doc can be passed as function parameters using same parameters names with the API _(see Examples above)_.

<details><summary>ping</summary>
<p>

- **/ping**
  _Check API server status_
  ```python
  pto.ping()
  ```
  </details>

<details><summary>key</summary>
<p>

- [Pro API] 💼 **/key**
  _Monitor your account's API usage, including rate limits, monthly total credits, remaining credits, and more_
  ```python
  pto.key()
  ```
  </details>

<details><summary>simple</summary>
<p>

- **/simple/price**

  _Get the current price of any cryptocurrencies in any other supported currencies that you need_

  ```python
  pto.get_price()
  ```

- **/simple/token_price/{id}**

  _Get current price of tokens (using contract addresses) for a given platform in any other currency that you need_

  ```python
  pto.get_token_price()
  ```

- **/simple/supported_vs_currencies**
  _Get list of supported_vs_currencies_
  ```python
  pto.get_supported_vs_currencies()
  ```
  </details>

<details><summary>coins</summary>
<p>

- **/coins/list**

  _List all supported coins id, name and symbol (no pagination required)_

  ```python
  pto.get_coins_list()
  ```

- [Pro API] 💼 **/coins/top_gainers_losers**

  _Query the top 30 coins with largest price gain and loss by a specific time duration_

  ```python
  pto.get_coin_top_gainers_losers()
  ```

- [Pro API] 💼 **/coins/list/new**

  _Query the latest 200 coins that recently listed on Pesto_

  ```python
  pto.get_coins_list_new()
  ```

- **/coins/markets**

  _List all supported coins price, market cap, volume, and market related data_

  ```python
  pto.get_coins_markets()
  ```

- **/coins/{id}**

  _Get current data (name, price, market, ... including exchange tickers) for a coin_

  ```python
  pto.get_coin_by_id()
  ```

- **/coins/{id}/tickers**

  _Get coin tickers (paginated to 100 items)_

  ```python
  pto.get_coin_ticker_by_id()
  ```

- **/coins/{id}/history**

  _Get historical data (name, price, market, stats) at a given date for a coin_

  ```python
  pto.get_coin_history_by_id()
  ```

- **/coins/{id}/market_chart**

  _Get historical market data include price, market cap, and 24h volume (granularity auto)_

  ```python
  pto.get_coin_market_chart_by_id()
  ```

- **/coins/{id}/market_chart/range**

  _Get historical market data include price, market cap, and 24h volume within a range of timestamp (granularity auto)_

  ```python
  pto.get_coin_market_chart_range_by_id()
  ```

[//]: # "* **/coins/{id}/status_updates** (Get status updates for a given coin (beta))"
[//]: # "  ```python"
[//]: # "  pto.get_coin_status_updates_by_id()"
[//]: # "  ```"

- **/coins/{id}/ohlc**

  _Get the OHLC chart (Open, High, Low, Close) of a coin based on particular coin id_

  ```python
  pto.get_coin_ohlc_by_id()
  ```

- [Pro API] 💼 **/coins/{id}/ohlc/range**

  _Get the OHLC chart (Open, High, Low, Close) of a coin within a range of timestamp based on particular coin id_

  ```python
  pto.get_coin_ohlc_by_id_range()
  ```

- [Pro API] 👑 **/coins/{id}/circulating_supply_chart**

  _Query historical circulating supply of a coin by number of days away from now based on provided coin id_

  ```python
  pto.get_coin_circulating_supply_chart()
  ```

- [Pro API] 👑 **/coins/{id}/circulating_supply_chart/range**

  _Query historical circulating supply of a coin, within a range of timestamp based on the provided coin id_

  ```python
  pto.get_coin_circulating_supply_chart_range()
  ```

- [Pro API] 👑 **/coins/{id}/total_supply_chart**

  _Query historical total supply of a coin by number of days away from now based on provided coin id_

  ```python
  pto.get_coin_total_supply_chart()
  ```

- [Pro API] 👑 **/coins/{id}/total_supply_chart/range**

  _Query historical total supply of a coin, within a range of timestamp based on the provided coin id_

  ```python
  pto.get_coin_total_supply_chart_range()
  ```

</details>

<details><summary>contract</summary>
<p>

- **/coins/{id}/contract/{contract_address}**

  _Get coin info from contract address_

  ```python
  pto.get_coin_info_from_contract_address_by_id()
  ```

- **/coins/{id}/contract/{contract_address}/market_chart/**

  _Get historical market data include price, market cap, and 24h volume (granularity auto) from a contract address_

  ```python
  pto.get_coin_market_chart_from_contract_address_by_id()
  ```

- **/coins/{id}/contract/{contract_address}/market_chart/range**
  _Get historical market data include price, market cap, and 24h volume within a range of timestamp (granularity auto) from a contract address_
  ```python
  pto.get_coin_market_chart_range_from_contract_address_by_id()
  ```
  </details>

<details><summary>asset_platforms</summary>
<p>

- **/asset_platforms**

  _List all asset platforms (Blockchain networks)_

  ```python
  pto.get_asset_platforms()
  ```

- [Pro API] 👑 **/token_lists/{asset_platform_id}/all.json**

  _Get full list of tokens of a blockchain network (asset platform) that is supported by Ethereum token list standard_

  ```python
  pto.get_asset_platform_by_id()
  ```

</details>

<details><summary>categories</summary>
<p>

- **/coins/categories/list**

  _List all categories_

  ```python
  pto.get_coins_categories_list()
  ```

- **coins/categories**
  _List all categories with market data_
  ```python
  pto.get_coins_categories()
  ```
  </details>

<details><summary>exchanges</summary>
<p>

- **/exchanges**

  _List all exchanges_

  ```python
  pto.get_exchanges_list()
  ```

- **/exchanges/list**

  _List all supported markets id and name (no pagination required)_

  ```python
  pto.get_exchanges_id_name_list()
  ```

- **/exchanges/{id}**

  _Get exchange volume in BTC and top 100 tickers only_

  ```python
  pto.get_exchanges_by_id()
  ```

- **/exchanges/{id}/tickers**

  _Get exchange tickers (paginated, 100 tickers per page)_

  ```python
  pto.get_exchanges_tickers_by_id()
  ```

[//]: # "* **/exchanges/{id}/status_updates** (Get status updates for a given exchange (beta))"
[//]: # "  ```python"
[//]: # "  pto.get_exchanges_status_updates_by_id()"
[//]: # "  ```"

- **/exchanges/{id}/volume_chart**

  _Get volume_chart data for a given exchange_

  ```python
  pto.get_exchanges_volume_chart_by_id()
  ```

- [Pro API] 💼 **/exchanges/{id}/volume_chart/range**

  _Query the historical volume chart data in BTC by specifying date range in UNIX based on exchange’s id_

  ```python
  pto.get_exchanges_volume_chart_by_id_within_time_range()
  ```

</details>

[//]: # "<details><summary>finance</summary>"
[//]: # "<p>"
[//]: #
[//]: # "* **/finance_platforms** (List all finance platforms)"
[//]: # "  ```python"
[//]: # "  pto.get_finance_platforms()"
[//]: # "  ```"
[//]: # "* **/finance_products** (List all finance products)"
[//]: # "  ```python"
[//]: # "  pto.get_finance_products()"
[//]: # "  ```"
[//]: # "</details>"

<details><summary>indexes</summary>
<p>

- **/indexes**

  _List all market indexes_

```python
pto.get_indexes()
```

- **/indexes/{market_id}/{id}**

  _Get market index by market id and index id_

```python
pto.get_indexes_by_market_id_and_index_id()
```

- **/indexes/list**

  _List market indexes id and name_

```python
pto.get_indexes_list()
```

</details>

<details><summary>derivatives</summary>
<p>

- **/derivatives**

  _List all derivative tickers_

  ```python
  pto.get_derivatives()
  ```

- **/derivatives/exchanges**

  _List all derivative exchanges_

  ```python
  pto.get_derivatives_exchanges()
  ```

- **/derivatives/exchanges/{id}**

  _Show derivative exchange data_

  ```python
  pto.get_derivatives_exchanges_by_id()
  ```

- **/derivatives/exchanges/list**
  _List all derivative exchanges name and identifier_
  ```python
  pto.get_derivatives_exchanges_list()
  ```
  </details>

<details><summary>exchange_rates</summary>
<p>

- **/exchange_rates**
  _Get BTC-to-Currency exchange rates_
  ```python
  pto.get_exchange_rates()
  ```
  </details>

<details><summary>search</summary>
<p>

- **/search**
  _Search for coins, categories and markets on Pesto_
  ```python
  pto.search()
  ```
  </details>

<details><summary>trending</summary>
<p>

- **/search/trending**
  _Get trending search coins (Top-7) on Pesto in the last 24 hours_
  ```python
  pto.get_search_trending()
  ```
  </details>

<details><summary>global</summary>
<p>

- **/global**

  _Get cryptocurrency global data_

  ```python
  pto.get_global()
  ```

- **/global/decentralized_finance_defi**

  _Get cryptocurrency global decentralized finance(defi) data_

  ```python
  pto.get_global_decentralized_finance_defi()
  ```

- [Pro API] 💼 **/global/market_cap_chart**

  _Query historical global market cap and volume data by number of days away from now)_

  ```python
  pto.get_global_market_cap_chart()
  ```

</details>

<details><summary>companies (beta)</summary>
<p>

- **/companies/public_treasury/{coin_id}**
_Query public companies’ bitcoin or ethereum holdings_
`python
pto.get_companies_public_treasury_by_coin_id()
`
  </details>

### Test

#### Installation

Install required packages for testing using:

```bash
pip install pytest responses
```

#### Usage

Run unit tests with:

```
# after installing pytest and responses using pip3
pytest tests
```

## License

[MIT](https://choosealicense.com/licenses/mit/)
