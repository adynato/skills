---
name: mobile
description: Mobile app development conventions for Adynato projects using React Native and Expo. Covers navigation patterns, native APIs, performance optimization, and platform-specific considerations. Use when building or modifying mobile applications.
---

# Mobile Development Skill

Use this skill for all Adynato mobile projects built with React Native and Expo.

## Stack

- **Framework**: Expo (managed workflow preferred)
- **Navigation**: Expo Router (file-based routing)
- **Styling**: NativeWind (Tailwind for React Native)
- **State**: Zustand or React Context
- **Data Fetching**: TanStack Query

## Project Structure

```
app/
├── (tabs)/
│   ├── _layout.tsx
│   ├── index.tsx
│   └── profile.tsx
├── (auth)/
│   ├── _layout.tsx
│   ├── login.tsx
│   └── register.tsx
├── _layout.tsx
└── +not-found.tsx
components/
├── ui/
│   ├── Button.tsx
│   └── Input.tsx
└── [feature]/
hooks/
lib/
constants/
assets/
├── images/
└── fonts/
```

## Navigation

### Expo Router Patterns

```tsx
// app/_layout.tsx - Root layout
import { Stack } from 'expo-router'

export default function RootLayout() {
  return (
    <Stack>
      <Stack.Screen name="(tabs)" options={{ headerShown: false }} />
      <Stack.Screen name="(auth)" options={{ headerShown: false }} />
    </Stack>
  )
}
```

```tsx
// app/(tabs)/_layout.tsx - Tab navigation
import { Tabs } from 'expo-router'
import { Home, User } from 'lucide-react-native'

export default function TabLayout() {
  return (
    <Tabs>
      <Tabs.Screen
        name="index"
        options={{
          title: 'Home',
          tabBarIcon: ({ color }) => <Home color={color} />,
        }}
      />
      <Tabs.Screen
        name="profile"
        options={{
          title: 'Profile',
          tabBarIcon: ({ color }) => <User color={color} />,
        }}
      />
    </Tabs>
  )
}
```

### Navigation Actions

```tsx
import { router } from 'expo-router'

// Navigate
router.push('/profile')
router.replace('/home')
router.back()

// With params
router.push({
  pathname: '/user/[id]',
  params: { id: '123' }
})
```

## Components

### Platform-Specific Styles

```tsx
import { Platform, StyleSheet } from 'react-native'

const styles = StyleSheet.create({
  container: {
    paddingTop: Platform.OS === 'ios' ? 50 : 30,
    ...Platform.select({
      ios: { shadowColor: '#000' },
      android: { elevation: 4 },
    }),
  },
})
```

### Safe Area Handling

```tsx
import { SafeAreaView } from 'react-native-safe-area-context'

export function Screen({ children }) {
  return (
    <SafeAreaView className="flex-1 bg-white dark:bg-gray-900">
      {children}
    </SafeAreaView>
  )
}
```

### Pressable Over TouchableOpacity

```tsx
import { Pressable, Text } from 'react-native'

<Pressable
  onPress={handlePress}
  className="active:opacity-70 bg-blue-500 px-4 py-2 rounded-lg"
>
  <Text className="text-white font-semibold">Press Me</Text>
</Pressable>
```

## Images in Mobile

### Using Expo Image

Prefer `expo-image` over React Native's Image:

```tsx
import { Image } from 'expo-image'

<Image
  source={{ uri: 'https://example.com/image.webp' }}
  style={{ width: 200, height: 200 }}
  contentFit="cover"
  placeholder={blurhash}
  transition={200}
/>
```

### Local Images

```tsx
import { Image } from 'expo-image'

<Image
  source={require('@/assets/images/logo.png')}
  style={{ width: 100, height: 100 }}
/>
```

## Native APIs

### Permissions Pattern

```tsx
import * as Location from 'expo-location'

async function requestLocation() {
  const { status } = await Location.requestForegroundPermissionsAsync()

  if (status !== 'granted') {
    // Handle denial gracefully
    return null
  }

  return await Location.getCurrentPositionAsync({})
}
```

### Secure Storage

```tsx
import * as SecureStore from 'expo-secure-store'

// Store sensitive data
await SecureStore.setItemAsync('token', authToken)

// Retrieve
const token = await SecureStore.getItemAsync('token')

// Delete
await SecureStore.deleteItemAsync('token')
```

## Performance

### List Optimization

```tsx
import { FlashList } from '@shopify/flash-list'

<FlashList
  data={items}
  renderItem={({ item }) => <ItemCard item={item} />}
  estimatedItemSize={100}
  keyExtractor={(item) => item.id}
/>
```

### Memoization

```tsx
import { memo, useCallback, useMemo } from 'react'

const ExpensiveComponent = memo(function ExpensiveComponent({ data }) {
  const processed = useMemo(() => processData(data), [data])
  const handlePress = useCallback(() => { ... }, [])

  return <View>...</View>
})
```

## Testing

### Component Testing

```tsx
import { render, fireEvent } from '@testing-library/react-native'
import { Button } from '@/components/ui/Button'

test('Button calls onPress', () => {
  const onPress = jest.fn()
  const { getByText } = render(<Button onPress={onPress}>Click</Button>)

  fireEvent.press(getByText('Click'))
  expect(onPress).toHaveBeenCalled()
})
```

## Build & Deploy

### EAS Build

```bash
# Development build
eas build --profile development --platform ios

# Production
eas build --profile production --platform all
```

### Environment Variables

```tsx
// Use expo-constants for env vars
import Constants from 'expo-constants'

const apiUrl = Constants.expoConfig?.extra?.apiUrl
```

## Checklist

Before releasing:

- [ ] Tested on both iOS and Android
- [ ] Safe area handling on all screens
- [ ] Keyboard avoiding views where needed
- [ ] Loading and error states for all async operations
- [ ] Offline handling considered
- [ ] Deep linking configured
- [ ] App icons and splash screen set
- [ ] Performance profiled (no jank)
