# CHANGELOG
## 3.0.3
- rearraged the order in which the template parameters show up. "returnEventData" is now part of the collapsible "customEventData"

## 3.0.2
- FEATURE: added `page_load_id` which allows to connect every event on a page
- TESTS: added tests for `page_load_id` consistency and reload behavior
- REFACTOR: extracted `simulatePageLoad()` function for improved test reusability

## 3.0.1
- TESTS: added tests to `btnt.js` 
- REFACTOR: renamed `frontendLibrary.js` to `btnt.js`

## 3.0.0
- FEATURE: added `maxBaxSize` parameter to the btntConfig. Setting this parameter to an Integer will cause btnt events to be batched and not sent via individual requests. This can be useful when there are dozens of events happening at the same time
- 
## 2.1.1
- FIX: dropped check for existance of `page_referrer` since for direct traffic it can acutally be empty

## 2.1.0

- ADD: Setting for enabling returning event data as json
- ADD: validation for required params
- REFACTOR: added some undefined checks to make it more resilient
- REFACTOR: removed unnessacry decode URL

## 2.0.6

- FEAT: event names that trigger a new_session can now also be passed as a pipe-separated ( | ) list

## 2.0.5

- refactor: simplified response logic

## 2.0.4

- FIX: bots requesting the btnt.js library received a 404 response which in turn triggered the error monitoring of our default server GTM setup in Google Cloud. From now on bots will receive an empty 204 response. This avoids uncessary egress cost and doesnt trigger error monitoring

## 2.0.3

- FIX: `computeEffectiveTldPlusOne` fails if not provided with a valid URL. This fix introduces a fallback solution that checks for the validity of the input argument before running `computeEffectiveTldPlusOne`

## 2.0.2

- FIX: in order to avoid duplicate data, all parameters that already are in the a custom_params/custom_metrics object will not be repeated in the remaining event data
- FIX: array in the BTNT config will always be stringified
- Feat: `decodeUriComponent` on all values of the event data object
- Feat: frontend library now will flatten objects that are passed as object values. For example passing `{generic_settings: {page_path: "test", page_host: "website.com"}}` will set the parameters `page_path` and `page_host`. This makes it easier to have settings-variable type that you can pass to all BTNT tags

## 2.0.1

- FEAT: list of default parameters is now configurable

## 2.0.0

- FEAT: added allowlist for custom parameters in order to be able to avoid storing data that we do not want to store
- FEAT: automatically will sort parameters into numerical and string parameters in order to write them into a respective column in BigQuery (no more need to add the `ep.` or `em.` prefixes in the frontend requests)

## 1.3.4

- FIX: server-timing header only added in debug mode

## 1.3.3

- FIX: First action is to check if the request comes from a bot and if it isn't, this client stops execution immediately

## 1.3.2

- FEAT: you can now select to wait for tags to finish. This will increase the response time, but it will open to possibility to return custom cookies to the user

## 1.3.1

- FEAT: all paramters can now be submitted as camel_case through the frontend library

## 1.3.0

- FIX: no more failure when page_referrer is not a valid URL

## 1.2.6

- FIX: decode `page_location` and `page_referrer` before working with them

## 1.2.5

- FEAT: recognize traffic with the `awc` click ID as traffic coming from AWIN

## 1.2.4

- FIX: organic and social referrals now marked as such mediums

### 1.2.3

- NEW: added support for referral exclusion

## 1.2.2

- NEW: fix for rogue referrals. When the `event_name` is `page_view`, we store the current `page_location` in `window.btntConfig.pageReferrer`. Then, all events after the first page_view, will use that variable for the `page_referrer`. Thus, we can avoid several page_views triggering a new session in a single-page context where the `document.referrer` will remain unchanged

## 1.2.1

- NEW: campaign timeout
- NEW: if the source is a referral-website, the value will be set to the origin of the referring website (i. e. www.linkedin.com) instead of the etdl+1 (i. e. linkedin.com)
- REFACTOR: the debug cookie is now called `BTNT_debug` in order to match the naming convention for the other cookies used by this client

## 1.2

- FIX: Attribution is now working as expected.
- NEW: added Attribution Tests
- REFACTOR: Renamed Parameter Names in FE Lib for better Readability
