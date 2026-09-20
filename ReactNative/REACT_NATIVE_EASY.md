# 📱 React Native - Easy Questions From Notes

> **Topics from Notes Covered:** `ScrollView` vs `SafeAreaView`, `FlatList` vs `Map`.

---

### Q1: `ScrollView` vs `SafeAreaView`
**Question (From Notes):** What is the difference between `ScrollView` and `SafeAreaView` in React Native?

**Answer:**
- **`ScrollView`**: A scrolling container that renders all its children at once. Used when content exceeds screen height.
- **`SafeAreaView`**: A layout container that automatically adds padding to keep content inside the safe boundaries of modern device screens (avoiding notches, camera holes, status bars, and home indicator bars).

```jsx
import React from 'react';
import { SafeAreaView, ScrollView, Text, StyleSheet } from 'react-native';

export function ScreenLayout() {
  return (
    <SafeAreaView style={styles.safe}>
      <ScrollView contentContainerStyle={styles.scroll}>
        <Text>Safe and scrollable content</Text>
      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  safe: { flex: 1, backgroundColor: '#fff' },
  scroll: { padding: 16 }
});
```

---

### Q2: `FlatList` vs `Array.map()`
**Question (From Notes):** Why should you use `FlatList` instead of `Array.map()` for rendering lists in React Native?

**Answer:**
- **`Array.map()` inside `ScrollView`**: Renders **every single item immediately** into native views. For large arrays (100+ items), this causes extreme memory usage and crashes the app.
- **`FlatList`**: Uses **Virtualization / Lazy Loading**. It only renders the items currently visible on the screen (+ a small buffer window) and recycles off-screen views.

```jsx
import React from 'react';
import { FlatList, View, Text } from 'react-native';

const data = Array.from({ length: 1000 }, (_, i) => ({ id: `${i}`, title: `Item ${i}` }));

export function EfficientList() {
  return (
    <FlatList
      data={data}
      keyExtractor={item => item.id}
      renderItem={({ item }) => (
        <View style={{ padding: 16, borderBottomWidth: 1, borderColor: '#ccc' }}>
          <Text>{item.title}</Text>
        </View>
      )}
    />
  );
}
```
