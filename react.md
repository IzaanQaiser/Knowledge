Copy and paste the following exact comment into your workOrderSteps.tsx file — ideally near the button where you want Copilot to add the checker logic:

// Create a button that logs whether the interaction was a mouse click or a touch press.
// Use a ref and add a pointerdown event listener inside useEffect.
// When pointerType is 'mouse', log "Mouse Click detected".
// When pointerType is 'touch', log "Touch Press detected".
// Clean up the event listener on unmount.
// Use TypeScript with proper typing.

That should prompt Copilot to generate the component correctly.

But if you want the full ready-to-use code to paste directly and skip guessing, here it is:

import React, { useRef, useEffect } from "react";

const InputTypeButton = () => {
  const buttonRef = useRef<HTMLButtonElement>(null);

  useEffect(() => {
    const handlePointerDown = (e: PointerEvent) => {
      if (e.pointerType === "mouse") {
        alert("Mouse Click detected");
      } else if (e.pointerType === "touch") {
        alert("Touch Press detected");
      } else if (e.pointerType === "pen") {
        alert("Pen Input detected");
      }
    };

    const btn = buttonRef.current;
    if (btn) {
      btn.addEventListener("pointerdown", handlePointerDown);
    }

    return () => {
      if (btn) {
        btn.removeEventListener("pointerdown", handlePointerDown);
      }
    };
  }, []);

  return (
    <button
      ref={buttonRef}
      className="px-4 py-2 bg-blue-600 text-white rounded"
    >
      Test Input Type
    </button>
  );
};

export default InputTypeButton;

Then just import and use it anywhere in workOrderSteps.tsx like:

<InputTypeButton />

Let me know if you want it inline instead of separate!