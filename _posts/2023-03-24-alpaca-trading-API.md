---
layout: post
title: Unlocking the Potential of Alpaca Trading API - A Comprehensive Guide
date: '2023-03-24T09:00:00.000-03:00'
tags: [frontend-development, alpaca API, javascript development]
author_id: christian-casaran
category: development
permalink: /blog/a-comprehensive-guide-to-alpaca-trading-api/
featured_image: /images/alpaca-trading-API/Alpaca_trading.png
---

![Alpaca trading.png](/images/alpaca-trading-API/Alpaca_trading.png)


# What is Alpaca Trading API?

Alpaca API is a cutting-edge platform created by Alpaca Group, a US-based stock brokerage firm. It provides users with a robust infrastructure to develop algorithms for buying and selling stocks, cryptocurrencies, and other financial services. With Alpaca's API, users can send orders directly to Alpaca's servers to automate the trading process, bypassing traditional clients.

One of the key benefits of Alpaca is its supervision by the Securities and Exchange Commission (SEC) and the Financial Industry Regulatory Authority (FINRA), ensuring maximum security and protection of client's funds. Moreover, the Securities Investor Protection Corporation (SIPC) safeguards clients' funds and securities, utilizing the company's strategic backup plan in case of the broker's bankruptcy or inability to meet its obligations. Experience automated trading with peace of mind, only with Alpaca API.

# Pros and Cons of using Alpaca Trading API

If you're considering using the Alpaca Trading API, it's essential to weigh the pros and cons to decide if it's the right choice for you. To assist you in making an informed decision, we've assembled a table highlighting the advantages and disadvantages of using the Alpaca Trading API. This table provides a comprehensive overview of the benefits and drawbacks of Alpaca Trading API, allowing you to make an informed decision that suits your needs.

|                                         Pros |                                         Cons |
| --- | --- |
| Commission-free.  | Customer support is limited to email. |
| Excellent charting tools. | Limited options for deposits and withdrawals. |
| Allows the construction of an automated trading system. | Only US stocks and ETFs (Exchange Traded Funds). |
| Operations are subject to supervision by both the SEC and FINRA.  | Complex process to integrate third-party tools.  |
| Integration with different platforms. |  |

# Alternatives to Alpaca Trading API

If you're considering using Alpaca Trading API, you might also be interested in exploring other options. To help you compare and evaluate them, we've compiled a table that outlines the features and specifications of various trading APIs, including Alpaca. With this comparison, you can easily identify the strengths and limitations of each API, and make an informed decision on which one is right for you.

|  | https://brokerchooser.com/broker-reviews/alpaca-trading-review | https://brokerchooser.com/broker-reviews/alpaca-trading-review/alpaca-trading-alternatives#moomoo | https://brokerchooser.com/broker-reviews/alpaca-trading-review/alpaca-trading-alternatives#webull | https://brokerchooser.com/broker-reviews/alpaca-trading-review/alpaca-trading-alternatives#sofi-invest | https://brokerchooser.com/broker-reviews/alpaca-trading-review/alpaca-trading-alternatives#robinhood |
| --- | --- | --- | --- | --- | --- |
| Overall score | 4.7 | 4.7 | 4.8 | 4.7 | 4.5 |
| Fees score | 4.8 | 4.7 | 4.8 | 5.0 | 4.6 |
| Account opening score | 4.8 | 4.2 | 5.0 | 4.2 | 5.0 |
| Deposit and withdrawal score | 1.8 | 1.9 | 1.9 | 2.2 | 1.8 |
| Web platform score | 3.7 | 0.0 | 5.0 | 3.2 | 4.5 |
| Markets and products score | 2.6 | 2.4 | 2.9 | 2.2 | 2.9 |
| Founded in | 2015 | 2018 | 2017 | 2011 | 2013 |
| Headquarter | US | US | US | US | US |
| Investor protection  | $500,000 | $500,000 | $500,000 | $500,000 | $500,000 |
| Zero commission | yes | yes | yes | yes | yes |
| Regulated by | https://www.finra.org/#/ https://www.sipc.org/ | https://www.finra.org/#/ https://www.sipc.org/ https://www.sec.gov/ | https://www.sec.gov/ https://www.sfc.hk/en/ | https://www.finra.org/#/ https://www.sec.gov/ | https://www.finra.org/#/ https://www.sec.gov/ |
| Main services | Crypto trading, Stock trading | Stock trading | Stock trading, Crypto trading, Recurring Investment | Stocks trading, Stocks trading | Stocks trading, Cash Management |

# Success Stories of Alpaca Trading API

Alpaca Trading API has gained popularity among developers and financial services providers due to its ease of use and flexible interface that enables the creation of automated trading systems. In this section, we showcase some success stories of apps and platforms that have integrated Alpaca Trading API to provide trading and financial services to their users. These examples highlight the diverse ways in which Alpaca Trading API can be utilized to create innovative and successful trading solutions.

| https://www.algotraders.ai/ | This platform performs algorithmic trading, using the Alpaca API, to allow its users to automate their trading strategies. |
| --- | --- |
| https://www.quantconnect.com/ | This is a backtesting and trading strategy development platform that uses the Alpaca API to provide real-time data and order execution for buying and selling. |
| https://es.tradingview.com/ | This trading technical analysis platform uses the Alpaca API to allow users to trade directly from their charts and trading tools. |

# Getting Started with Alpaca API using NodeJS

In this section, we'll provide a step-by-step guide on how to get started with Alpaca API using NodeJS. We'll cover how to set up a paper-only account and a Broker API account, the two alternatives to interact and consume the Alpaca resources. Whether you're a beginner or an experienced developer, our guide will help you get started with Alpaca API quickly and easily.

## Setting up a Paper-Only Account in  Alpaca

Paper trading is a type of account that provides a real-time simulation environment where it's possible to test your code. You can reset and test your algorithm as much as you want using free, real-time market data.

To create a Paper Only Account and integrate it with an app it’s necessary to follow the next steps:

![paper account.gif](/images/alpaca-trading-API/paper_account.gif)

- Register to the Alpaca platform through this URL: [https://alpaca.markets/](https://alpaca.markets/)
- After creating and verifying the account, you should log in and navigate to the [operations dashboard](https://app.alpaca.markets/paper/dashboard/overview).
- Once in the dashboard, locate the API Keys tab and click on the 'Generate', 'New Key’ or 'Regenerate’ buttons. Save these credentials as you won't be able to visualize them again.
- After generating and saving the credentials, you will be able to integrate Alpaca's API with an application. To this end, Alpaca provides an [SDK](https://alpaca.markets/docs/trading/getting_started/) for Python, Javascript C# and Go.
    
    ```bash
    npm install --save @alpacahq/alpaca-trade-api
    ```
    
- After installing the library, it must be imported into the service where it will be used in order to create a new instance, for which the previously saved credentials must be provided.
    
    ```jsx
    import Alpaca from '@alpacahq/alpaca-trade-api';
    
    const alpaca = new Alpaca({
      paper: true,
      secretKey: process.env.SECRET_KEY,
      API: process.env.API_KEY,
    });
    ```
    

At this point, Alpaca API resources can be consumed, and the information can be used according to the application logic. In this case, the resources have been associated with services exposed through a NodeJS API.

- These services can be consumed in different ways, for example using Postman or in some cases directly from a web browser. For this example, the *[REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)* extension of Visual Studio Code is used, for which only a file with the http extension needs to be created within the application. From this file, all calls to the API can be made using the following structure.
    
    ```bash
    @api = http://localhost:3000/api/trading
    
    ### get account info
    GET {{api}}/account
    ```
    

The Javascript SDK provides a large number of functions that allow you to consume a wide variety of resources from the Alpaca API, which can be used to automate trading based on this information and the business logic that is implemented.

- One of the first resources that can be consumed is account information, which can be obtained by making an asynchronous call to the ***getAccount*** function. The response includes all account information.

```jsx
export const getAccount = async () => {
  return await alpaca.getAccount();
};
```

```json
{
	"id": ee302827-4ced-4321-b5fb-71080392d828
	"account_number": PA3717PJAYWN
	"status": ACTIVE
	"crypto_status": ACTIVE
	"currency": USD
	"buying_power": 1768290.404988
	"regt_buying_power": 1768290.404988
	"daytrading_buying_power": 0
	"non_marginable_buying_power": 882145.2
	"cash": 884145.202494
	"accrued_fees": 0
	"pending_transfer_out": None
	"pending_transfer_in": 0
	"portfolio_value": 910178.2209985875
	"pattern_day_trader": False
	"trading_blocked": False
	"transfers_blocked": False
	"account_blocked": False
	"created_at": 2022-04-19 17:46:03.685850+00:00
	"trade_suspended_by_user": False
	"multiplier": 2
	"shorting_enabled": True
	"equity": 910178.2209985875
	"last_equity": 907426.98
	"long_market_value": 26033.0185045875
	"short_market_value": 0
	"initial_margin": 0
	"maintenance_margin": 0
	"last_maintenance_margin": 0
	"sma": 868738.98
	"daytrade_count": 0
}
```

- ***getCryptoBars***: This function allows you to track the performance of a cryptocurrency within a specific period by providing the cryptocurrency name, start and end dates, and a timeframe, it returns a json object with the cryptocurrency price of a specific date.

```jsx
export const getSymbolTrades = async (params: SymbolParams) => {
  const { symbol, days } = params;
  return await alpaca.getCryptoBars(
    symbol,
    { 
      start: getDateFrom(days),
      end: new Date(),
      timeframe: "1Day",
    },
  );
};
```

```json
{
	"symbol": "BTCUSD",
	"timestamp": "2022-07-07T05:00:00Z",
	"exchange": "CBSE",
	"open": 20400.28,
	"high": 20445.5,
	"low": 20224.8,
	"close": 20404.32,
	"volume": 1029.86433895,
	"tradecount": 43372,
	"VWAP": 20350.5220346576
}
```

- ***getPositions***: This function returns the open positions associated with the account. No parameters are required to consume this information.

```jsx
export const getPositionsStatus = async () => {
  return await alpaca.getPositions();
};
```

```json
{
  "asset_id": 64bbff51 - 59d6 - 4b3c - 9351 - 13ad85e3c752
  "symbol": BTCUSD
  "exchange": FTXU
  "asset_class": crypto
  "avg_entry_price": 20983
  "qty": 0.9975
  "side": long
  "market_value": 20928.5475
  "cost_basis": 20930.5425
  "unrealized_pl": -1.995
  "unrealized_plpc": -0.0000953152552066
  "unrealized_intraday_pl": -1.995
  "unrealized_intraday_plpc": -0.0000953152552066
  "current_price": 20981
  "lastday_price": 19344
  "change_today": 0.084625723738627
}
```

- ***getAssets***: This function provides a master list of available cryptocurrencies and tokens. It can take up to 3 different parameters: status, asset_class, and exchange. It retrieves a json object list according to the provided parameters.

```jsx
export const getAssets = async (params: AssetsParams) => {
  return await alpaca.getAssets(params);
};
```

```jsx
{
  "id": "276e2673-764b-4ab6-a611-caf665ca6340",
  "class": "crypto",
  "exchange": "FTXU",
  "symbol": "BTC/USD",
  "name": "BTC/USD pair",
  "status": "active",
  "tradable": true,
  "marginable": false,
  "shortable": false,
  "easy_to_borrow": false,
  "fractionable": true,
  "min_order_size": "0.0001",
  "min_trade_increment": "0.0001",
  "price_increment": "1"
}
```

- ***createOrder***: This function allows you to create a new order for a specific asset, which requires providing a minimum set of parameters, although there are various options available. It returns the created order object.

```jsx
export const createOrder = async (orderParams: any) => {
  return await alpaca.createOrder(orderParams);
};
//example
{
  "symbol": "BTC/USD",
  "qty": 1,
  "side": "buy",
  "type": "market",
  "time_in_force": "gtc"
}
```

```jsx
{
    "id": "5cdabade-aded-47be-9ef1-489695bfa39d",
    "client_order_id": "8fb819c8-98c5-4609-861c-d9bd6bd05b7c",
    "created_at": "2023-01-09T22:30:04.085727Z",
    "updated_at": "2023-01-09T22:30:04.097252Z",
    "submitted_at": "2023-01-09T22:30:04.085201Z",
    "filled_at": "2023-01-09T22:30:04.08896Z",
    "expired_at": null,
    "canceled_at": null,
    "failed_at": null,
    "replaced_at": null,
    "replaced_by": null,
    "replaces": null,
    "asset_id": "276e2673-764b-4ab6-a611-caf665ca6340",
    "symbol": "BTC/USD",
    "asset_class": "crypto",
    "notional": null,
    "qty": "1",
    "filled_qty": "1",
    "filled_avg_price": "17238.291649",
    "order_class": "",
    "order_type": "market",
    "type": "market",
    "side": "buy",
    "time_in_force": "gtc",
    "limit_price": null,
    "stop_price": null,
    "status": "filled",
    "extended_hours": false,
    "legs": null,
    "trail_percent": null,
    "trail_price": null,
    "hwm": null,
    "subtag": null,
    "source": "access_key"
  }
```

- ***getOrders***: This function returns all orders associated with an account and allows you to send certain parameters to filter the information, such as status, until, after, limit, and others.

```jsx
export const getOrders = async (params: any) => {
  if (params.orderId) {
    return await getOrderById(params.orderId);
  }

  return alpaca.getOrders(params);
};
```

```jsx
[
  {
    "id": "5cdabade-aded-47be-9ef1-489695bfa39d",
    "client_order_id": "8fb819c8-98c5-4609-861c-d9bd6bd05b7c",
    "created_at": "2023-01-09T22:30:04.085727Z",
    "updated_at": "2023-01-09T22:30:04.097252Z",
    "submitted_at": "2023-01-09T22:30:04.085201Z",
    "filled_at": "2023-01-09T22:30:04.08896Z",
    "expired_at": null,
    "canceled_at": null,
    "failed_at": null,
    "replaced_at": null,
    "replaced_by": null,
    "replaces": null,
    "asset_id": "276e2673-764b-4ab6-a611-caf665ca6340",
    "symbol": "BTC/USD",
    "asset_class": "crypto",
    "notional": null,
    "qty": "1",
    "filled_qty": "1",
    "filled_avg_price": "17238.291649",
    "order_class": "",
    "order_type": "market",
    "type": "market",
    "side": "buy",
    "time_in_force": "gtc",
    "limit_price": null,
    "stop_price": null,
    "status": "filled",
    "extended_hours": false,
    "legs": null,
    "trail_percent": null,
    "trail_price": null,
    "hwm": null,
    "subtag": null,
    "source": "access_key"
  }
]
```

### Real-Time services

The Alpaca API provides other Real-Time options, which can be consumed in real-time through web sockets. These options allow you to subscribe to different types of resources and receive instant updates, enabling you to make timely decisions regarding market behavior. To use the Real-Time resources  the Alpaca API has to offer you need to follow these steps:

- Create an Alpaca instance just like you did previously. After creating the instance, assign the required client, and once the specific client has been assigned, it is possible to subscribe to the required resources.

```jsx
const alpaca = new Alpaca({
  paper: true,
});

const websocket = alpaca.crypto_stream_v2;
```

- In this example a subscription is made to ************subscribeForTrades************, corresponding to the events generated by updating a specific symbol, such as a cryptocurrency or a stock.

```jsx
websocket.onConnect(() => {
	websocket.subscribeForTrades(["AAPL"]);
});
```

- Just like subscriptions, the respective listeners for each event must be initialized, such as *connect*, *onError*, *onStateChange*, and the listeners for specific resources to which you have subscribed, such as *onStockTrade*, *onStockBar*, and others.

```jsx
websocket.onStateChange((status) => { 
  console.log("Crypto stream status:", status);
});

websocket.onError((err) => {
  console.log("Error:", err);
});

websocket.onCryptoBar((bar) => {
  console.log("Crypto Bar:", bar);
});

websocket.onCryptoDailyBar((bar) => {
  console.log("Crypto Daily Bar:", bar);
});

websocket.onCryptoOrderbook((order) => {
  console.log("Crypto Order Book:", order);
});

websocket.onCryptoQuote((quote) => {
  console.log("Crypto Quote:", quote);
});

websocket.onCryptoTrade((trade) => {
  console.log("Crypto Trade:", trade);
});

websocket.onCryptoUpdatedBar((bar) => {
  console.log("Crypto updated bar:", bar);
});
```

- In the API created with Typescript and NodeJS, the *websocket crypto_stream_v2* client is used, which allows you to receive information on different events associated with the cryptocurrencies you want to analyze in an array. Additionally, the *data_stream_v2* client provides information on different events.

```jsx
// crypto_stream_v2
subscribe(symbols: {
   trades?: Array<string>;
   quotes?: Array<string>;
   bars?: Array<string>;
   updatedBars?: Array<string>;
   dailyBars?: Array<string>;
   orderbooks?: Array<string>;
}): void;
```

```jsx
// data_stream_v2
subscribe(symbols: {
    trades?: Array<string>;
    quotes?: Array<string>;
    bars?: Array<string>;
    updatedBars?: Array<string>;
    dailyBars?: Array<string>;
    statuses?: Array<string>;
    lulds?: Array<string>;
}): void;
```

In addition to these two WebSocket clients, there are also the *news_stream* and *data_ws* clients, which provide other types of real-time information.

The above functions are some of the many options provided by the SDK. Depending on the needs and logic of the application, you can choose to use the one that meets the requirements. These resources can be consulted in the [API documentation](https://alpaca.markets/docs/).

## **Setting up a Broker API Account in the Alpaca API**

The Broker API Account provided by Alpaca allows you to create trading applications with various tools for users. Alpaca provides an isolated environment with all the necessary tools and information to implement and test all the functionalities a broker app typically offers. This isolated testing environment has the same capabilities as the real environment, except for a few functionalities that require real money. 

### Use Cases for Creating Apps with a Broker API Account

Depending on the type of application you want to build, there are three use cases for creating applications: Trading/investing app, Broker dealer (fully-disclosed, non-disclosed, omnibus), and Registered Investment Advisor (RIA). Depending on the case, specific API resources are used.

- **[Trading/Investing](https://alpaca.markets/docs/broker/use-cases/#tradinginvesting-app)**: This type of trading and/or investment application can be developed by a technology company, an established fintech company that offers cash management services, a neobank, or even a payroll company without the required license. In this case, the account approval process is owned by Alpaca, and the application creator would own the user experience and most of the communications. Unless you have a solid CIP/KYC/AML program that has been reviewed by Alpaca, your clients will go through Alpaca's CIP/KYC/AML process.
- **[Broker-Dealer](https://alpaca.markets/docs/broker/use-cases/#broker-dealer)**: This use case has two alternatives, Fully-Disclosed and Omnibus.
    - **[Fully-Disclosed](https://alpaca.markets/docs/broker/use-cases/#fully-disclosed):** In this case, a user established as a broker-dealer within their jurisdiction, creates individual accounts for their clients in Alpaca using their information. Depending on the legal framework of the application creator's jurisdiction, they may own the complete user experience, from account opening, trading, generating reports, and maintaining a robust customer identification program (CIP) and procedures to fully identify customers (KYC), in accordance with anti-money laundering (AML) regulations.
    - **[Omnibus](https://alpaca.markets/docs/broker/use-cases/#omnibus):** In this case, a user established as a stockbroker manages the information and trading flow of their clients with long and short-term trading accounts. In this configuration, clients' basic information such as name, address, etc. is not revealed to Alpaca.
- **[Registered Investment Advisor (RIA)](https://alpaca.markets/docs/broker/use-cases/#registered-investment-advisor-ria):** In this case, an RIA user registered in the SEC with clients within or outside the US, must create accounts for their clients in Alpaca. Said creation and approval will be the property of Alpaca, while the user of the application will own the user experience and most communications. Unless they have a solid CIP/KYC/AML program that has been reviewed by Alpaca, their clients will go through Alpaca's CIP/KYC/AML process.
As an RIA, the user can communicate directly with their clients, and Alpaca will work with the user to market the service using the Broker API in a compatible way.

### Creating **a Broker API Account**

To create a Broker API Account and integrate it with an app it’s necessary to follow these steps:

![broker account.gif](/images/alpaca-trading-API/broker_account.gif)

- Register to the Alpaca Broker platform through this URL: [https://broker-app.alpaca.markets/sign-up](https://broker-app.alpaca.markets/sign-up)
- After creating your account and logging in, you need to generate your API access credentials. To do this, go to the [API/Devs](https://broker-app.alpaca.markets/dev) page and click on the Generate option.
- Once you have the corresponding credentials, you can proceed to integrate with the Broker API. In this case, this platform does not have an SDK for such integration. In the practical example, NodeJS and Typescript were used, and API calls were made with the Axios library. For this, the first step was to create a function that generates a token based on the generated credentials, and another function that receives the endpoint to be queried and the respective parameters.
    
```jsx
const generateAuthToken = () => {
  return Buffer.from(`${BROKER_API_KEY}:${BROKER_SECRET}`, 'utf8').toString('base64');
};

const callAPI = async (endpoint: string, method = 'get', params = {}, data = {}) => {
  const response = await axios({
    method,
    url: `https://broker-api.sandbox.alpaca.markets/v1/${endpoint}`,
    params,
    data,
    headers: {
      'Authorization': `Basic ${generateAuthToken()}`,
      'content-type': 'application/json',
    }
  });

  if (!response.data) {
    return response;
  }

  return response.data;
};
```
    
- The AlpacaBroker API guide recommends initially exporting and exploring the Postman collection, which contains all the resources provided by the API, and serves as a guide to identifying the resources required for the implementation of the services to be executed.

After having the base configuration to communicate with the API, and having chosen and explored the services to be used, the implementation begins. In this case, services were enforced for the creation and consultation of client users, and consultation of assets and commercial events.

- ***createAccount***: This service allows the creation of a new user account associated with the broker account. This service receives a series of parameters, some mandatory and some optional, and it returns the created account info.
    
This resource is accessible at the endpoint: *https://broker-api.sandbox.alpaca.markets/v1/accounts*
    

```jsx
export const createNewAccount = async (params: UserInfo) => {
  return callAPI('accounts', 'post', {}, params);
};
```

```jsx
{
  "contact": {
    "email_address": "alpaca@example.com",
    "phone_number": "555-666-7788",
    "street_address": ["20 N San Mateo Dr"],
    "city": "San Mateo",
    "state": "CA",
    "postal_code": "94401",
    "country": "USA"
  },
  "identity": {
    "given_name": "John",
    "family_name": "Doe",
    "date_of_birth": "1990-01-01",
    "tax_id": "666-55-4321",
    "tax_id_type": "USA_SSN",
    "country_of_citizenship": "USA",
    "country_of_birth": "USA",
    "country_of_tax_residence": "USA",
    "funding_source": ["employment_income"]
  },
  "disclosures": {
    "is_control_person": false,
    "is_affiliated_exchange_or_finra": false,
    "is_politically_exposed": false,
    "immediate_family_exposed": false
  },
  "agreements": [
    {
      "agreement": "margin_agreement",
      "signed_at": "2020-09-11T18:09:33Z",
      "ip_address": "185.13.21.99"
    },
    {
      "agreement": "account_agreement",
      "signed_at": "2020-09-11T18:13:44Z",
      "ip_address": "185.13.21.99"
    },
    {
      "agreement": "customer_agreement",
      "signed_at": "2020-09-11T18:13:44Z",
      "ip_address": "185.13.21.99"
    }
  ],
  "documents": [
    {
      "document_type": "identity_verification",
      "document_sub_type": "passport",
      "content": "/9j/Cg==",
      "mime_type": "image/jpeg"
    }
  ],
  "trusted_contact": {
    "given_name": "Jane",
    "family_name": "Doe",
    "email_address": "jane.doe@example.com"
  }
}
```

- ***getAccounts***: This service allows consulting all the user accounts associated with the broker account. Among the parameters received by this service is the status or accountId, the response is an array with the accounts information. This resource is accessible at the endpoint [https://broker-api.sandbox.alpaca.markets/v1/accounts](https://broker-api.sandbox.alpaca.markets/v1/accounts).

```jsx
export const getAccounts = async (params: any) => {
  let resource = 'accounts'

  if (params.accountId) {
    resource = `${resource}/${params.accountId}`;
  }

  return callAPI(resource);
};
```

```jsx
[
  {
    "id": "fc1a5a44-6a9a-4919-9e4f-9e17edf9cc64",
    "account_number": "961722725",
    "status": "ACTIVE",
    "crypto_status": "INACTIVE",
    "kyc_results": {
      "reject": {},
      "accept": {},
      "indeterminate": {},
      "summary": "pass"
    },
    "currency": "USD",
    "last_equity": "0",
    "created_at": "2023-01-16T22:05:31.346989Z",
    "account_type": "trading",
    "enabled_assets": [
      "us_equity"
    ]
  }
]
```

- ***getAssets***: This service allows querying the current asset information, for this query the parameters *symbol*, *status*, *asset_class*, and *exchange* must be passed. The response is composed of an array with the assets data. This is because if this filter is not done, the API returns too much data. This resource is accessible at the endpoint [https://broker-api.sandbox.alpaca.markets/v1/assets](https://broker-api.sandbox.alpaca.markets/v1/assets).

```jsx
export const getAssets = async (assetParams: AssetsParams) => {
  const { symbol, status,  asset_class, exchange } = assetParams;
  let resource = 'assets';
  const params = {};

  if (symbol) {
    resource = `${resource}/${symbol}`;
  } else {
    Object.assign(params, {
      status: status || 'active',
      asset_class: asset_class || 'crypto',
      exchange: exchange || 'FTXU',
    });
  }

  return callAPI(resource, 'get', params);
};
```

```jsx
[
	{
		"id": "7595a8d2-68a6-46d7-910c-6b1958491f5c",
		"class": "us_equity",
		"exchange": "NYSE",
		"symbol": "A",
		"name": "Agilent Technologies Inc.",
		"status": "active",
		"tradable": true,
		"marginable": true,
		"shortable": true,
		"easy_to_borrow": true,
		"fractionable": true
	}
]
```

- ***getTradeEvents***: This service allows to consult all the trade events that have occurred in a range of time. TeThis resource is accessible at the endpoint. [https://broker-api.sandbox.alpaca.markets/v1/events/trades](https://broker-api.sandbox.alpaca.markets/v1/events/trades)

```jsx
export const getTradeEvents: Handler = async (req, res) => {
  try {
    const trades = await pullTradeEvents(req.query);
    return res.json(trades);
  } catch (error) {
    return res.status(500).json(handleError(error));
  }
};
```

```jsx
{
    "account_id":"c8f1ef5d-edc0-4f23-9ee4-378f19cb92a4",
    "at":"2021-06-14T10:04:05.172241Z",
    "event":"new",
    "event_id":3014423,
    "execution_id":"a829b698-da07-479f-91e6-f204c77573fc",
    "order":{
      "asset_class":"us_equity",
      "asset_id":"b0b6dd9d-8b9b-48a9-ba46-b9d54906e415",
      "canceled_at":null,
      "client_order_id":"d6499947-dacd-4f85-a728-81734dc39c27",
      "commission":"1.1",
      "created_at":"2021-06-14T10:04:05.150255Z",
      "expired_at":null,
      "extended_hours":false,
      "failed_at":null,
      "filled_at":null,
      "filled_avg_price":null,
      "filled_qty":"0",
      "hwm":null,
      "id":"d507255a-b072-4fb7-96f3-9ad5a9c02b2a",
      "legs":null,
      "limit_price":null,
      "notional":"10",
      "order_class":"",
      "order_type":"market",
      "qty":null,
      "replaced_at":null,
      "replaced_by":null,
      "replaces":null,
      "side":"buy",
      "status":"new",
      "stop_price":null,
      "submitted_at":"2021-06-14T10:04:05.0937Z",
      "symbol":"AAPL",
      "time_in_force":"day",
      "trail_percent":null,
      "trail_price":null,
      "type":"market",
      "updated_at":"2021-06-14T10:04:05.165088Z"
    },
    "timestamp": "2021-06-14T10:04:05.172241Z"
  }
```

<aside>
👉 Practical Example: building an API REST with NodeJs, Typescript y Express**

As an example, we built a REST API with NodeJs, Typescript, and Express, in which the services described above were implemented. The code is available on [GitHub](https://github.com/Kriz1618/alpaca-rest-api).

</aside>

## Going to Production with Alpaca Trading API

Launching a technological and financial solution into production involves significant responsibilities and risks, so it is essential to follow good security practices and comply with applicable regulations.

To deploy any application, different steps may be required, depending on the technology or business structure, but in general, the following points could be highlighted.

- **Testing stage:** Starting from an existing implementation, and having a testing account in Alpaca with the respective credentials, it must be ensured that the application is fully tested and works correctly in the development and test environment.
- **Account creation**: After testing and verifying that all the services integrating the Alpaca API are working, you must create a production account in Alpaca and start the verification with new credentials.
- **Security and Hosting Configuration:** All of Alpaca's requirements must be met, and in addition, settings such as the protection of credentials and sensitive data must be made. Then the process of updating the application on the chosen hosting system must be automated.
- **********************Monitoring:********************** It's paramount that, in the first days of operation, the platform has detailed monitoring to identify and correct any inconvenience that may arise in any of the services.

## Conclusion

Alpaca API provides a tremendous amount of options to implement cryptocurrency trading applications. To go deeper into this world, you can check out the official documentation and the Alpaca community [forums](https://forum.alpaca.markets/). 

Alpaca ha tenido un gran crecimiento en los últimos años gracias a diferentes factores, entre los que podemos mencionar los siguientes puntos.

Alpaca has had impressive growth during the last couple of years thanks to various factors, including:

- Accessibility: The platform is available and provides different tools for a broad audience, with few restrictions to test its services.
- Low commissions: Alpaca offers low commissions compared to other trading platforms, making it an affordable alternative
- Integration: The Alpaca API allows integration with third-party applications, with different programming languages through libraries.
- Large developer community: Alpaca has developed an active community of developers that creates and shares tools and applications for the platform, making it more attractive to those interested in automated trading.

The possibilities of Alpaca API are almost endless, and whatever your fintech app is, it can surely help you with your objectives. But with great power comes great responsibility and it's important to know what the best options are for you so as not to get lost in that much information/possibilities. I encourage you to educate yourself in the Alpaca API or to hire a third party who knows the tech's ins and outs so you can have a more professional assessment. 

You can get a comprehensive and honest picture of your project or product and its opportunities by jumping on a free discovery call with our team, which includes developers well-versed in this platform. Contact us here. 

We hope this guide proved to be useful, any questions or comments are more than welcome. Thanks for reading!