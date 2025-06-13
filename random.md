“Add a button to WorkOrderSteps.tsx that, when pressed or clicked, does the following:
	1.	Uses onPointerDown to detect whether the interaction was with mouse, touch, or pen.
	2.	Uses Platform.OS from react-native to detect the current platform (ios, android, or web).
	3.	For web, detect whether it’s running on a mobile device or desktop using navigator.userAgent.
	4.	Combines that info and shows a window.alert() in the browser that says something like:
Platform: iOS | Input: Touch or Platform: Desktop | Input: Mouse.

Also: Wrap the platform detection in a helper function like getDevicePlatformType().”
