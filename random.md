

> Add a `getDeviceType` function that detects:
>
> * `"iOS"` for iOS devices using `Platform.OS` or userAgent
> * `"Android"` for Android devices
> * `"Desktop (Touch)"` for web on Windows/macOS/Linux with `navigator.maxTouchPoints > 0`
> * `"Desktop (Mouse & Keyboard)"` for web on Windows/macOS/Linux with no touch
>
> Then render a `Button` inside the component that shows an alert saying the device type when pressed.

---

### ✅ The full code Copilot should generate or help you complete:

```tsx
import { Platform, Button, Alert, View } from 'react-native';

const getDeviceType = (): string => {
  if (Platform.OS === 'ios') return 'iOS';
  if (Platform.OS === 'android') return 'Android';

  if (Platform.OS === 'web') {
    const ua = navigator.userAgent.toLowerCase();
    const isTouch = navigator.maxTouchPoints > 0;

    if (ua.includes('iphone') || ua.includes('ipad')) return 'iOS';
    if (ua.includes('android')) return 'Android';
    if (ua.includes('windows') || ua.includes('mac') || ua.includes('linux')) {
      return isTouch ? 'Desktop (Touch)' : 'Desktop (Mouse & Keyboard)';
    }
  }

  return 'Unknown';
};

// Inside your WorkOrderSteps component’s return:
<View>
  {/* ...your existing JSX content... */}
  <Button
    title="Detect Device"
    onPress={() => Alert.alert('Device Type', getDeviceType())}
  />
</View>
```
