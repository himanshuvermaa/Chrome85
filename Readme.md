Content Visibility

Browsers rendering process
Turning your HTML into something the user can see, requires the browser to go through a number of steps before it can even paint the first pixel. And it does it for the whole page, even for content that isn’t visible in the viewport.

Applying content-visibility: auto to an element, tells the browser that it can skip the rendering work for that element until it scrolls into the viewport, providing a faster initial render.

.my-class {
  content-visibility: auto;
}

To get the most impact out of content-visibility, apply it to parent sections with more complex layout algorithms, like flexbox, and grid, or that have children with contained layouts of their own.



By chunking content and adding content-visibility: auto;, this page went from a rendering time of 232ms to only 30ms.

Check out the content visibility to see how you can use it to improve your rendering performance.

@property and CSS variables
CSS variables, technically called custom properties, are awesome. With the Houdini CSS Properties and Values API, you can define a type and default fallback value for your custom properties. I previously covered them in New in Chrome 78, when we added support for defining them in JavaScript.

Starting in Chrome 85, you can also define and set CSS properties directly in your CSS. What I love about CSS Properties - is that it gives the property semantic meaning, fallback values, and even enables CSS testing.

@property --colorPrimary {
  syntax: '<color>';
  initial-value: magenta;
  inherits: false;
}

Una has a great post @property: giving superpowers to CSS variables that shows you how you can use them.

Get installed related apps
The getInstalledRelatedApps() API makes it possible for you to check if your app is installed, then, customize the user experience.

For example, show different content to the user on a landing page if your app is already installed. Centralize overlapping functionality in one app to prevent confusion. Or, if your native app is already installed, don’t promote the installation of your PWA.

When it first shipped in Chrome 80, it only worked for Android apps. Now, on Android, it can also check if your PWA is installed. And on Windows, it can check if your Windows UWP app is installed.

const relatedApps = await navigator.getInstalledRelatedApps();
relatedApps.forEach((app) => {
  console.log(app.id, app.platform, app.url);
});

Check out my article Is your app installed? getInstalledRelatedApps() will tell you! on web.dev to see how it works, and how to sign your apps to prove they’re yours.

App Icon Shortcuts

App icon shortcut on Windows
In Chrome 84, we added support for App Icon Shortcuts. I accidentally said they were available everywhere, but they were only available on Android. Now, in Chrome 85, they’re available on Android and Windows, and in both Chrome and Edge.

"shortcuts": [
  {
    "name": "Open Play Later",
    "short_name": "Play Later",
    "description": "View the list you saved for later",
    "url": "/play-later",
    "icons": [
      { "src": "//play-later.png", "sizes": "192x192" }
    ]
  },
]

Check out the App Icon Shortcuts article on web.dev for complete details, and I’m sorry for the confusion I caused.

Origin Trial: Streaming requests with fetch()
Starting in Chrome 85, fetch upload streaming is available as an origin trial. It lets you start a fetch before the request body is ready. Previously, you could only start a request once you had the whole body ready to go. But now, you can start sending content, even while you're still generating it.

const { readable, writable } = new TransformStream();

const responsePromise = fetch(url, {
  method: 'POST',
  body: readable,
});

For example, use it to warm up the server, or stream audio or video as it’s captured from the microphone or camera.

Jake has an in-depth look in Streaming requests with the fetch API on web.dev, and also covered it in the latest HTTP203 - Streaming requests with fetch video.

And more
Of course, there’s plenty more.

Promise.any returns a promise that is fulfilled by the first given promise to be fulfilled or rejected.

try {
  const first = await Promise.any(arrayOfPromises);
  console.log(first);
} catch (error) {
  console.log(error.errors);
}

Replacing all instances in a string is easier with .replaceAll(), no more regular expressions!

const myName = 'My name is Bond, James Bond.'
    .replaceAll('Bond', 'Powers')
    .replace('James', 'Austin');
console.log(myName);
// My name is Powers, Austin Powers.

Chrome 85 adds decode support for AVIF, an image format encoded with AV1 and standardized by the Alliance for Open Media. AVIF offers significant compression gains vs. JPEG and WebP, with a recent Netflix study showing 50% savings vs. standard JPEG and > 60% savings on 4:4:4 content.

And AppCache removal has begun.
