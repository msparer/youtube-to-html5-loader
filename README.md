
# Load YoutTube videos as HTML5 emebed element

[![](https://data.jsdelivr.com/v1/package/npm/@thelevicole/youtube-to-html5-loader/badge)](https://www.jsdelivr.com/package/npm/@thelevicole/youtube-to-html5-loader)
[![Latest Stable Version](https://img.shields.io/npm/v/@thelevicole/youtube-to-html5-loader)](https://www.npmjs.com/package/@thelevicole/youtube-to-html5-loader)
[![Total Downloads](https://img.shields.io/npm/dt/@thelevicole/youtube-to-html5-loader)](https://www.npmjs.com/package/@thelevicole/youtube-to-html5-loader)

## Get started

### Load library
First you need to include the library in your project, this can be achieved via NPM or jsDeliver.

#### NPM
```
npm i @thelevicole/youtube-to-html5-loader
```
```javascript
import YouTubeToHtml5 from '@thelevicole/youtube-to-html5-loader'
```

#### jsDeliver
```html
<script src="https://cdn.jsdelivr.net/npm/@thelevicole/youtube-to-html5-loader@5/dist/YouTubeToHtml5.min.js"></script>
```

### Initiating
First setup your HTML something like:
```html
<video data-yt2html5="YOUTUBE_URL_OR_ID_GOES_HERE"></video>
```
And then simply initiate the library with:
```javascript
new YouTubeToHtml5();
```

### Options
There are a number of options that can be passed to the constructor these are:
| Option | Description | Type | Default |
|--|--|--|--|
| `endpoint` | This is the API url thats used for retrieving data. More information to come. | `string` | `https://yt2html5.com/?id=` |
| `selector` | The DOM selector used for finding video elements. | `string` | `video[data-yt2html5]` |
| `attribute` | This is the attribute where your YouTube id/url is stored on the element. | `string` | `data-yt2html5` |
| `formats` | Filter the API results by specific formats. For example `[ '1080p', '720p' ]` will only allow 1080p and 720p formats. An asterix will allow all streaming formats. | `string|array` | `*` |
| `autoload` | Whether or not to load all videos on library init. | `boolean` | `true` |
| `withAudio` | Whether or not to only load streams with audio. | `boolean` | `true` |
| `withVideo` | Whether or not to only load streams with video. | `boolean` | `true` |

### Hooks
The library has a hook mechanism for filters and actions. If you've worked with WordPress before you'll be familiar with this concept.

> Note: all filters and actions will have the library instance (context) passed as the first argument in the callback.

#### Filters
Modify and return values.
##### Request URL
You might want to modify the request URL on each element load. You can do this with the `request.url` filter. For example:
```javascript
const controller = new YouTubeToHtml5({
	autoload: false
});

controller.addFilter('request.url', function(context, url) {
	return `${url}&cache_bust=${(new Date()).getTime()}`;
});

controller.load();
```

#### Actions
Run code everytime the action is called.
##### Before each load
```javascript
const controller = new YouTubeToHtml5({
	autoload: false
});

controller.addAction('load.before', function(context, element, data) {
	element.classList.add('is-loading');
});

controller.load();
```
##### After each load
```javascript
const controller = new YouTubeToHtml5({
	autoload: false
});

controller.addAction('load.after', function(context, element, data) {
	element.classList.remove('is-loading');
});

controller.load();
```
##### After a successful load
```javascript
const controller = new YouTubeToHtml5({
	autoload: false
});

controller.addAction('load.success', function(context, element, data) {
	element.classList.addClass('is-playable');
});

controller.load();
```
##### After a failed load
```javascript
const controller = new YouTubeToHtml5({
	autoload: false
});

controller.addAction('load.failed', function(context, element, data) {
	element.classList.add('is-unplayable');
});

controller.load();
```


## Accepted URL patterns
Below is a list of varying YouTube url patterns, which include http/s and www/non-www.

```
youtube.com/watch?v=ScMzIvxBSi4
youtube.com/watch?vi=ScMzIvxBSi4
youtube.com/v/ScMzIvxBSi4
youtube.com/vi/ScMzIvxBSi4
youtube.com/?v=ScMzIvxBSi4
youtube.com/?vi=ScMzIvxBSi4
youtu.be/ScMzIvxBSi4
youtube.com/embed/ScMzIvxBSi4
youtube.com/v/ScMzIvxBSi4
youtube.com/watch?v=ScMzIvxBSi4&wtv=wtv
youtube.com/watch?dev=inprogress&v=ScMzIvxBSi4&feature=related
m.youtube.com/watch?v=ScMzIvxBSi4
youtube-nocookie.com/embed/ScMzIvxBSi4
```
