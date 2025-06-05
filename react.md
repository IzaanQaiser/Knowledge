✅ Yes, exactly. Here’s the full flow:

⸻

🔧 Step-by-Step:
	1.	Create a new file, e.g.:

src/components/InputDetector.jsx


	2.	Paste the component (example using pointerdown):

import React, { useEffect, useRef } from "react";

const InputDetector = () => {
  const ref = useRef(null);

  useEffect(() => {
    const handlePointerDown = (e) => {
      alert(`Pointer Type: ${e.pointerType}`); // 'mouse', 'touch', or 'pen'
    };

    const el = ref.current;
    el.addEventListener("pointerdown", handlePointerDown);

    return () => {
      el.removeEventListener("pointerdown", handlePointerDown);
    };
  }, []);

  return (
    <div
      ref={ref}
      style={{
        padding: "2rem",
        border: "2px solid white",
        background: "#333",
        color: "white",
        borderRadius: "8px",
        textAlign: "center",
        userSelect: "none",
        cursor: "pointer",
      }}
    >
      Tap or Click me to test input type
    </div>
  );
};

export default InputDetector;


⸻

	3.	Import it into any screen, e.g. in a page or screen:

import InputDetector from '../components/InputDetector';

export default function HomeScreen() {
  return (
    <div>
      <h1>Welcome</h1>
      <InputDetector />
    </div>
  );
}


⸻

Let me know if you want it to be a hook instead (useInputType) or if you want it to trigger different logic based on input (e.g. multi-select mode on long press).