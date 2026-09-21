# 📱 React Native - Medium Questions

> **Topics Covered:** `FlatList` vs `ScrollView` vs `SectionList` (Virtualization & Pagination), `Pressable` vs `TouchableOpacity`, React Navigation (Stack, Tabs, Drawer), Local Storage (`AsyncStorage` vs `MMKV`), Platform-Specific Code (`Platform.OS`, `Platform.select`), Permissions & App Lifecycle.

---

### Q1: `FlatList` vs `ScrollView` vs `SectionList` ⭐⭐
**Question:** Compare `FlatList` and `ScrollView`. Why should you always use `FlatList` for long data lists?

**Answer:**
- **`ScrollView`**: Renders **all child components simultaneously** into memory upon mounting, regardless of whether they are visible on screen. For lists with 100+ items, this causes severe memory leaks and UI frame drops.
- **`FlatList`**: **Virtualized list**. Only renders the items currently visible in the screen's viewport (plus a small buffer). Recycles offscreen views to maintain low memory usage and 60 FPS scrolling.

```jsx
import { FlatList, Text, View, StyleSheet } from 'react-native';

const users = Array.from({ length: 1000 }, (_, i) => ({ id: `${i}`, name: `User ${i}` }));

export function UserList() {
  return (
    <FlatList
      data={users}
      keyExtractor={(item) => item.id}
      renderItem={({ item }) => (
        <View style={styles.card}>
          <Text>{item.name}</Text>
        </View>
      )}
      initialNumToRender={10}
      maxToRenderPerBatch={10}
      windowSize={5}
      onEndReached={() => console.log('Load more page...')}
      onEndReachedThreshold={0.5}
    />
  );
}

const styles = StyleSheet.create({
  card: { padding: 16, borderBottomWidth: 1, borderColor: '#eee' },
});
```

---

### Q2: Platform-Specific Code Handling
**Question:** What are the different ways to execute platform-specific code in React Native?

**Answer:**
1. **`Platform.OS` Check**:
   ```javascript
   import { Platform } from 'react-native';
   const headerHeight = Platform.OS === 'ios' ? 44 : 56;
   ```
2. **`Platform.select()`**:
   ```javascript
   const shadowStyle = Platform.select({
     ios: { shadowColor: '#000', shadowOffset: { width: 0, height: 2 }, shadowOpacity: 0.2 },
     android: { elevation: 4 },
   });
   ```
3. **Platform-Specific File Extensions**:
   - `HeaderComponent.ios.js`
   - `HeaderComponent.android.js`
   React Native automatically resolves the correct file extension during compilation.

---

### Q3: Client Storage: `AsyncStorage` vs `MMKV`
**Question:** Compare `AsyncStorage` and `react-native-mmkv`.

**Answer:**
- **`AsyncStorage`**:
  - Legacy asynchronous key-value storage.
  - Passes data over the asynchronous JSON bridge. Slow for frequent reads/writes.
- **`react-native-mmkv`**:
  - High-performance key-value storage written in C++ (by Tencent).
  - Uses **JSI (JavaScript Interface)** direct C++ bindings for **synchronous** instant reads/writes (up to 30x faster than AsyncStorage).
