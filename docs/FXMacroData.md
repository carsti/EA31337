# FXMacroData public requests

`FXMacroData.mqh` builds API URLs and fetches public JSON responses through MetaTrader's `WebRequest` function. The public USD baseline needs no API key or account.

```cpp
#include "include/common/FXMacroData.mqh"

void OnStart() {
  FXMacroData client;
  string response;
  int status = client.Get(client.Announcements("usd", "inflation"), response);
  if (status == 200) {
    // Parse response before using it in a strategy.
  }
}
```

Add `https://api.fxmacrodata.com` to the terminal's allowed WebRequest URLs. Run requests from an Expert Advisor or script; MetaTrader does not allow `WebRequest` in indicators or the Strategy Tester.

Public examples include `DataCatalogue("usd")`, `Announcements("usd", "inflation")`, and `Calendar("usd")`. Public announcements are delayed by 15 minutes and cover the most recent 90 days. See the [current API reference](https://fxmacrodata.com/documentation/reference?utm_source=github&utm_medium=referral&utm_campaign=EA31337&utm_content=docs) for availability, limits, and response fields.

## Credential handling

Authenticated requests are not supported by this transport. MetaTrader follows redirects internally, and `WebRequest` does not expose a redirect policy that this helper can enforce. Checking only the starting URL cannot establish where a credential-bearing request will end.

The constructor's optional key parameter remains for source compatibility. If it is nonempty, every `Get` call returns `-1`, clears `response`, and sends no request, regardless of the requested URL. The helper retains only a flag indicating that a key was supplied. `Headers()` always returns an empty string.

Use an empty key for public requests. Do not put keys in URLs, headers, logs, or source files. Existing URL builders do not grant access to protected datasets; FX rates and other protected coverage require an authenticated transport outside this helper.

[MetaQuotes documents automatic redirects](https://www.mql5.com/en/book/advanced/network/network_http) and the [WebRequest execution restrictions](https://www.mql5.com/en/docs/network/webrequest).
