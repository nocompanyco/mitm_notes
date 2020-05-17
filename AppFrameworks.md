STATUS: 
* Todo: Test electronjs on winodws


Notes on testing front-end Application frameworks that have javascript optionally under the hood. 


# Possible Frameworks
Conclusion: 
We will stick with electron for now. Switching out to Vue based or ReactJS based frameworks would be interesting but require additional work on rewriting UI, which currently we conveniently use browser tables and DOM+CSS for UI changes

## Options

Electronjs. Javascript centered. Used by many apps. Already in use for snifferjs.

[deskgap](https://deskgap.com/#whats-the-difference-between-deskgap-and-electron) uses os bundled browser kit instead of chromium. Is new and they note of some missing features.

[protonjs](https://proton-native.js.org/#/)  like [react native](https://reactnative.dev/) but for desktop. ReactJS UI views. From experience React requires optimization and testing overhead

[vuido](https://vuido.mimec.org/) is Vue.js based dekstop apps. _"Vuido is very lightweight compared to other frameworks, such as Electron or NW.js. The size of a simple Vuido application is about 20 MB, while a typical Electron application takes 90 MB or more. Applications using Vuido also take less memory and have faster startup time"_ -- while faster sounds nice I wonder if Vue.js UI elements can handle thousands of line entries as well as a browser/dom/electronjs version.

[nw.js](https://nwjs.io/) electron alternative. I believe I tried this years ago and found issues on the snifferjs side. But could try again

[sciter](https://sciter.com/) html centered with some tie ins to code?  Could be a very simple but limited alternative

## Non-javascript focused

[U++](https://www.ultimatepp.org/) C++. Would be nice if we for some reason had to switch to C++ but I do not see that happening

[fman](https://build-system.fman.io/) python with installer. Qt based. Intended as lightweight alternative to electron.