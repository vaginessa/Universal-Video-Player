# Responsive Accessible HTML5 Video Player

## by Ind.ie, based on work by the PayPal Accessibility Team
See the [Authors](#authors) section below for details.

## What is it?
A lightweight responsive HTML5 video player which includes support for captions and screen reader accessibility.

## Features
- Provides a responsive HTML5 video player with custom controls.
- Supports captions; simply denote a VTT caption file using the standard HTML5 video syntax.
- Uses native HTML5 form controls for volume (range input) and progress indication (progress element).
- Accessible to keyboard-only users and screen reader users.
- Option provided to set captions on or off by default (upon loading).
- Option provided to set number of seconds by which to rewind and forward.
- The width adjusts to the width of the video element.
- No dependencies. Written in "vanilla" JavaScript.
- When JavaScript is unavailable, the browser's native controls are used.

## Implementation

### CSS and Image
Insert the CSS in the Head of your HTML document. You'll also need to upload the sprite image (or use your own) and adjust the path in the CSS file.

```html
<link rel="stylesheet" href="/css/px-video.css" />
```

### HTML
Insert the HTML5 video markup in the Body of your HTML document. Replace the video, poster, and caption URLs. Modify the sizes of video and fallback image as needed.
```html
<div class="px-video-container" id="myvid">
	<div class="px-video-img-captions-container">
		<div class="px-video-captions hide"></div>
		<div class="px-video-wrapper">
			<video poster="../media/foo.jpg" class="px-video" controls>
				<!-- video files -->
				<source src="../media/foo.mp4" type="video/mp4" />
				<source src="../media/foo.webm" type="video/webm" />
				<source src="../media/foo.ogv" type="video/ogg" />

				<!-- text track file -->
				<track kind="captions" label="English captions" src="../media/captions-foo-en.vtt" srclang="en" default />

				<!-- fallback for browsers that don't support the video element -->
				<div>
					<a href="../media/foo.mp4">
						<img src="../media/foo.jpg" width="640" height="360" alt="download video" />
					</a>
				</div>
			</video>
		</div>
	</div><!-- end container for captions and video -->
	<div class="px-video-controls"></div>
</div><!-- end video container -->
```

### JavaScript
Insert the JavaScript file right before the closing Body element of your HTML document. Add a Script element to initialize the video. Options are passed in JSON format. The options are:

- videoId: the value of the ID of the widget container (string) [required]
- captionsOnDefault: denotes whether to show or hide caption upon loading (boolean) [optional, default is true]
- seekInterval: the number of seconds to rewind and fast forward (whole number) [optional, default is 10]
- videoTitle: short title of video; used for aria-label attribute on Play button to clarify to screen reader user what will be played (text) [optional, default is "Play"]
- debug: turn console logs on or off (boolean) [optional, default is false]

```html
<script src="js/px-video.js"></script>
<script>
// Initialize
new InitPxVideo({
	"videoId": "myvid",
	"captionsOnDefault": true,
	"seekInterval": 20,
	"videoTitle": "clips of stand-up comedy",
	"debug": true
});
</script>
```

## Testing
Due to Cross-Origin Resource Sharing (CORS), you'll need to run a web server in order to test the video player locally.

## Original Authors
- Dennis Lembree, primary developer || [https://github.com/weboverhauls](https://github.com/weboverhauls) || [@dennisl](https://twitter.com/dennisl)
- Victor Tsaran, consultation and testing || [https://github.com/vick08](https://github.com/vick08) || [@vick08](https://twitter.com/vick08)
- Jason Gabriele, consultation
- Tim Resudek, design

## Ind.ie Authors
- Laura Kalbag, design and development

## Browser Support
- Chrome: full support.
- Safari: full support.
- Firefox: full support.
- Internet Explorer 10, 11: full support.
- Internet Explorer 9: native video player used (aesthetic choice since HTML5 range input and progress element are not supported).
- Internet Explorer 8: renders fallback content of video element (in the demo, this is an image linked to the video file).
- Smartphones and tablets: controls and captions are not customized as both are natively supported in latest versions.

## Limitations and Known Issues
- Currently, only one caption file per video is supported.
- Only VTT caption files are supported (not SRT nor TTML). VTT cue settings are not supported but inline styles function (see first few lines of example).
- The controls have a minimum width of 360px.

## Copyright and License
Original work copyright 2014, eBay Software Foundation under [the BSD license](LICENSE.md)
Additional work copyright © 2013-2015 Ind.ie. © Article 12 under [the BSD license](LICENSE.md)