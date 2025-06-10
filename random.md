Below is a lightweight React/React-Native-Web pattern that
	•	shows a blocking overlay only when
	•	the screen is in landscape and
	•	the device is hand-held (phone / tablet – not a desktop monitor);
	•	never appears on desktop (even if you shrink the window).

Feel free to drop it straight into your Expo + React-Native-Web project.

⸻

1  Hook: useLandscapeGuard()

import { useState, useEffect } from 'react';

function isMobileLike(): boolean {
  // Quick heuristic: user agent OR small viewport in portrait
  return /iPhone|iPad|iPod|Android/i.test(navigator.userAgent) ||
         Math.min(window.innerWidth, window.innerHeight) < 768;
}

export function useLandscapeGuard() {
  const [showOverlay, setShowOverlay] = useState(
    isMobileLike() && window.innerWidth > window.innerHeight
  );

  useEffect(() => {
    if (!isMobileLike()) return;                 // ignore desktop altogether

    const handle = () => {
      setShowOverlay(window.innerWidth > window.innerHeight);
    };

    window.addEventListener('resize', handle);   // fires on rotation too
    window.addEventListener('orientationchange', handle);

    return () => {
      window.removeEventListener('resize', handle);
      window.removeEventListener('orientationchange', handle);
    };
  }, []);

  return showOverlay;
}

	•	isMobileLike() first checks the UA string (good enough for iOS/Android).
If privacy-hardened browsers strip the UA, it falls back to “portrait shortest side < 768 px” – which still distinguishes phones/tablets from desktop screens.

⸻

2  Overlay component

import { View, Text, StyleSheet } from 'react-native';

export function LandscapeOverlay() {
  return (
    <View pointerEvents="auto" style={styles.cover}>
      <Text style={styles.msg}>Please rotate back to portrait</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  cover: {
    position: 'fixed',
    top: 0, left: 0, right: 0, bottom: 0,
    backgroundColor: 'rgba(0,0,0,0.8)',
    justifyContent: 'center',
    alignItems: 'center',
    zIndex: 9999
  },
  msg: {
    color: '#fff',
    fontSize: 18,
    textAlign: 'center',
    paddingHorizontal: 24
  }
});


⸻

3  Drop it into your root screen

import { useLandscapeGuard } from './hooks/useLandscapeGuard';
import { LandscapeOverlay } from './components/LandscapeOverlay';

export default function AppRoot() {
  const mustBlock = useLandscapeGuard();

  return (
    <>
      {/* your normal app UI */}
      {mustBlock && <LandscapeOverlay />}
    </>
  );
}


⸻

Why this satisfies the requirement

Behaviour	How it’s enforced
Desktop → no popup ever	isMobileLike() exits early → listener never attaches.
Mobile portrait	window.innerWidth < window.innerHeight → hook returns false.
Mobile landscape	Resize / orientationchange flips the condition → overlay shown.
Back to portrait	Condition flips again → overlay unmounts immediately.

No need for external libraries, CSS breakpoints, or browser-specific hacks—just pure JS + React Native styles, fully compatible with Expo’s web build and your existing codebase.