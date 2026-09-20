# 📱 React Native - Medium Questions From Notes

> **Topics from Notes Covered:** `ScrollView` vs `FlatList`, Horizontal Scrolling Implementation.

---

### Q1: `ScrollView` vs `FlatList`
**Question (From Notes):** Compare `ScrollView` vs `FlatList` in React Native.

**Answer:**
| Feature | `ScrollView` | `FlatList` |
| :--- | :--- | :--- |
| **Rendering Strategy** | Eager (renders all child elements at once) | Lazy Virtualization (renders only visible items) |
| **Memory Footprint** | Grows linearly $O(N)$ with number of items | Constant $O(1)$ memory footprint |
| **Use Case** | Short, fixed content (forms, settings page, < 30 items) | Infinite feeds, product catalogs, chats (100+ items) |

---

### Q2: Horizontal Scrolling Implementation in React Native
**Question (From Notes):** How do you implement horizontal scrolling in React Native?

**Answer:**
Using `FlatList` with `horizontal={true}` and `showsHorizontalScrollIndicator={false}`:

```jsx
import React from 'react';
import { FlatList, View, Text, StyleSheet } from 'react-native';

const categories = ['Tech', 'Design', 'Marketing', 'Finance', 'Crypto', 'AI'];

export function HorizontalCategories() {
  return (
    <FlatList
      horizontal={true}
      showsHorizontalScrollIndicator={false}
      data={categories}
      keyExtractor={item => item}
      renderItem={({ item }) => (
        <View style={styles.card}>
          <Text style={styles.text}>{item}</Text>
        </View>
      )}
      contentContainerStyle={styles.container}
    />
  );
}

const styles = StyleSheet.create({
  container: { paddingVertical: 12, paddingHorizontal: 16 },
  card: {
    backgroundColor: '#3b82f6',
    paddingHorizontal: 16,
    paddingVertical: 10,
    borderRadius: 20,
    marginRight: 10
  },
  text: { color: '#fff', fontWeight: '600' }
});
```
