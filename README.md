# @advertol/service-google-dfp

[![Build Status][ci-img]][ci] [![BrowserStack Status][browserstack-img]][browserstack]

[Google DFP/Ad Manager](https://admanager.google.com/) service.

## Install

```sh
npm install @advertol/service-google-dfp --save
```

## Usage

```html
<!doctype html>
<html>
	<head>
		<script async="async" src="https://www.googletagservices.com/tag/js/gpt.js"></script>
		<script>
			window.googletag = window.googletag || {};
			window.googletag.cmd = window.googletag.cmd || [];
		</script>
	</head>
	<body>
		<div id="zone-becky"></div>
	</body>
</html>
```

```js
import advertol from '@advertol/core';
import GoogleDfpService from '@advertol/service-google-dfp';

const instance = advertol({
	// …
	service: [
		new GoogleDfpService({
			zones: [{
				id: 'becky',
				adUnitPath: '/42/becky',
				slot: () => window.googletag.defineSlot('/42/becky', ['fluid'], 'zone-becky').addService(window.googletag.pubads())
			}]
		})
	]
});

instance.resolve();
```

## API

### googleDfpService({ zones, onSetup, refreshZones })

#### zones

Type: `Object[]`

List of zones with their slot callback.

| Property | Type | Description |
| --- | --- | --- |
| `slot` | `Function` | Function which returns [`googletag.defineSlot`][googletag-define-slot] or [`googletag.defineOutOfPageSlot`][googletag-define-outofpage-slot] instance. |
| `adUnitPath` | `string` | Full path of the ad unit with the network code and unit code. |
| `id` | `string` | Zone ID. |

#### onSetup

Type: `Function`

Define additional initialization logic.

#### refreshZones(slots)

Type: `Function`

Refresh slots.

By default, it calls [`refresh`][googletag-refresh] method.

##### slots

Type: `googletag.Slot[]`

List of slots to refresh.

### instance.addZone({ slot, adUnitPath, id })

Add new zone with slot callback.

| Property | Type | Description |
| --- | --- | --- |
| `slot` | `Function` | Function which returns [`googletag.defineSlot`][googletag-define-slot] or [`googletag.defineOutOfPageSlot`][googletag-define-outofpage-slot] instance. |
| `adUnitPath` | `string` | Full path of the ad unit with the network code and unit code. |
| `id` | `string` | Zone ID. |

## Browser support

Tested in IE9+ and all modern browsers.

## Test

For automated tests, run `npm run test:automated` (append `:watch` for watcher support).

## License

MIT © [Ivan Nikolić](http://ivannikolic.com)

[ci]: https://travis-ci.com/niksy/advertol-service-google-dfp
[ci-img]: https://travis-ci.com/niksy/advertol-service-google-dfp.svg?branch=master
[browserstack]: https://www.browserstack.com/
[browserstack-img]: https://www.browserstack.com/automate/badge.svg?badge_key=WnJmTGFCek5KWFRxMjhrOE1wdE9CYUNkK3B3Y1U4cVl3SndsQjVEbmV4MD0tLWNzajBEdG1neHZROS94K0NpMW1qbWc9PQ==--70b8da2c741fdc30f6011a0ade9d36429c8b8f52
[googletag-define-slot]: https://developers.google.com/doubleclick-gpt/reference#googletag.defineSlot
[googletag-define-outofpage-slot]: https://developers.google.com/doubleclick-gpt/reference#googletag.defineOutOfPageSlot
[googletag-refresh]: https://developers.google.com/doubleclick-gpt/reference#googletag.PubAdsService_refresh
